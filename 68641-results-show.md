# results show

The `results show` command is used to **retrieve scan results** (i.e., generate reports) in Checkmarx One.


{% hint style="info" %}
Reports generated via the CLI use the standard scan report format. There is a newer type of customized scan report that can be generated via [API](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/ci2py4oc7hlt3-improved-reports-service-rest-api) or from the [web application](https://docs.checkmarx.com/en/34965-182434-checkmarx-one-reporting.html).
{% endhint %}


## Usage
```
./cx results show [flags]
```


## Flags
**`--scan-id <string>` Required**

Scan ID.

**`--filter <strings>` Default: All results are included**

Specify filters, pagination and sortin for the data that will be included in the report that is generated.

Filters aren't applied to PDF reports. You can specify which sections to include in a PDF report using `--report-pdf-options`.

- Use "**;**" to separate between multiple values for a particular filter.
- Use "," to separate between multiple filters.
- Available filters are: `limit`, `offset`, `sort`, `severity`, `state`, `status`.
- Enum values:
   
   - **severity** - Critical, High, Medium, Low, Info.
   - **state** - TO_VERIFY, NOT_EXPLOITABLE, PROPOSED_NOT_EXPLOITABLE, CONFIRMED, URGENT, EXCLUDE_NOT_EXPLOITABLE.
      
      {% hint style="info" %}
      The state filter can be applied either by submitting a separate value for each state to **include,** or by submitting the value `EXCLUDE_NOT_EXPLOITABLE` in order to exclude only `NOT_EXPLOITABLE` results.
      {% endhint %}
   - **status** - NEW, RECURRENT, FIXED.
   - **sort** - -severity, +severity, -status, +status, -state, +state, -type, +type, -firstfoundat, +firstfoundat, -foundat, +foundat, -firstscanid, +firstscanid.
      
      Default sorting: +status, +severity.
      
      {% hint style="success" %}
      "+" = ascending order
      
      "-" = descending order
      {% endhint %}

For an explanation of correct filter syntax, see [below](#paligo-section-idm33359135477006)

**`--help, -h`**

Help for the results command.

**`--output-name <string>` Default: cx_result**

Specify a name for the output file.

**`--output-path <string>` Default: "."**

Specify the file path for the output file.

**`--report-format <string>` Default: json**

Specify the format for the report that is generated.

Options are: `summaryHTML`, `summaryJSON`, `summaryConsole`, `sarif`, `gl-sast`, `gl-sca`, `json`, `json-v2`, `sonar`, `markdown`, `PDF`, or `SBOM`

{% hint style="info" %}
json-v2 is similar to the original json report. The main difference being that v2 is identical to the json report generated via the UI.
{% endhint %}

Json, json-v2, sarif, gl-sast, and sonar formats generate a detailed list of risks identified in the project (gl-sast returns only sast results and gl-sca returns only SCA results). SummaryHTML, summaryJSON, summaryConsole and markdown formats generate summary reports with aggregated risk data. PDF format reports by default generate a complete report including both a summary of risks as wel as a detailed list of risks. You can specify which sections to include in the report using `--report-pdf-options`.

{% hint style="success" %}
For SBOM reports, you need to add the `--report-sbom-format` flag to specify the SBOM standard and output format.
{% endhint %}

**`--report-pdf-email <string>`**

Specify email recipients who will receive the pdf report. Multiple emails are separated by a ",".

This flag can only be used when `--report-format` is set as `pdf`.

**`--report-pdf-options <string>` Default: All Sections**

Specify the sections that will be included in the pdf format report.

This flag can only be used when `--report-format` is set as `pdf`.

Available sections are: `Sast`, `Sca`, `Iac-Security`, `ScanSummary`, `ExecutiveSummary`, and `ScanResults`.

`ScanResults` includes results for all scanners (IaC-Security, Sast and Sca).

**`--report-sbom-format` Default: CycloneDxJson**

Specify the type of SBOM standard ([CycloneDX](https://cyclonedx.org/specification/overview/) or [SPDX](https://spdx.dev/about/)) as well as the output format.

Options are: `CycloneDxJson`, `CycloneDxXml`, or `SpdxJson`.

**`--sast-redundancy`**

Checkmarx identifies vulnerabilities with matching sub-flows, which enables prioritization of fixes that will resolve multiple vulnerabilities with a single fix.

When this flag is used, a new field `data.redundancy` is shown for each vulnerability, indicating which vulnerability should be prioritized as `fix` and which ones should be considered `redundant`.

**`--sca-hide-dev-test-dependencies`**

Adding this flag filters out dev and test dependencies from SCA results shown in scan reports.

Note: This flag is only relevant scans that ran the SCA scanner. Currently, this is not supported for PDF or SBOM reports.


## Pagination
By default all results are included in the report (up to 10k). You can use `limit` to adjust the maximum number of results to return and `offset` to specify the number of results to skip before starting to return results.

**Example:** The following command generates a report for records 21-30.

```
./cx results show --filter "limit=10,offset=20"
```


<a id="paligo-section-idm33359135477006"></a>

## Applying Filters and Sorting
You can filter the results included in the report by specifying various parameters such as severity, state and status. These filters apply both to the list of risks that is returned as well as to the summary data that is given. You can also specify how the list of risks is sorted in the report.

When multiple filter attributes are used, an AND operator is applied between attributes. When multiple values are given for an attribute, an OR operator is used between values.

Filters are applied using the following syntax:

```
./cx results show --filter "attributeA=value1,attributeB=value1;value2;value3,..."
```

**Example:** The following command returns a report that includes data for all risks with a severity level "high" or "medium" and the status "new". The results are sorted by "first found at" in descending order.

```
./cx results show --filter "severity=high;medium,status=new,sort=-firstfoundat+queryname"
```


## Workflow Examples
<details>

<summary>Retrieve a list of scan ID’s</summary>

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx scan list

Scan ID                              Project ID                           Status    Created at Tags    Initiator                      Origin                 
-------                              ----------                           ------    ---------- ----    ---------                      ------                 
3c028677-5df7-4bd9-8a10-7214ced45670 683c51da-8644-4e27-990f-1128ab911a1b Completed 09-10-21   []      service-account Github                 
c0507cb4-c68a-4db8-9565-5308d409a931 683c51da-8644-4e27-990f-1128ab911a1b Completed 09-10-21   []      service-account Github                 
5ee3482e-b068-4bc5-9671-1c98098b3062 683c51da-8644-4e27-990f-1128ab911a1b Completed 09-09-21   []      service-account Github
```

</details>

### Retrieve scan results for a specific scan ID using default settings
```
./cx results show --scan-id <scan ID>
```

```
user@laptop:~/ast-cli$ ./cx results show --scan-id 3c028677-5df7-4bd9-8a10-7214ced45670
2023/08/03 22:33:32 Creating JSON Report:  cx_result.jsonCreating JSON Report:  cx_result.json
```

### Retrieve scan results for a specific scan ID using several flags
```
./cx results show --scan-id <scan ID> --report-format sarif --output-name <file name> --output-path <output file location>
```

```
user@laptop:~/ast-cli$ ./cx results show --scan-id aca72f5d-1b58-4821-b7f0-508f857a9d4b --report-format sarif --output-name Demo_Sarif_Report --output-path "."
2023/08/04 12:17:38 Creating SARIF Report:  Demo_Sarif_Report.sarif
```

### Generate a PDF report of SAST vulnerabilities and send it to an email recipient
```
./cx results show --scan-id <scan ID> --report-format pdf --report-pdf-email <recipient_email> --report-pdf-options <specify_sections>
```

```
user@laptop:~/ast-cli$ ./cx results show --scan-id aca72f5d-1b58-4821-b7f0-508f857a9d4b --report-format pdf --report-pdf-email demo@example.com --report-pdf-options sast
2023/08/04 12:25:52 Sending PDF report to:  [demo@example.com]
```

