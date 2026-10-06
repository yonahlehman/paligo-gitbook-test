# scan create

The `scan create` command enables users to **create and run new scans** in Checkmarx One.


## Usage
```
./cx scan create [flags]
```


## Scanning Source Code
The `scan create` command can be used to scan source code using the following methods:

- A compressed .zip archive
- A repository URL
- A local directory
   
   {% hint style="info" %}
   When you scan from a local directory, the CLI compresses the folder into a .zip archive and stores it in your system's temporary storage location until it is uploaded to Checkmarx One. When scanning from a local directory or ZIP file, the CLI supports multi-part uploads for compressed sources larger than 5 GB, up to a maximum of 6 GB. - Multi-part uploads are controlled by the `multipart_file_size` setting (chunk size in GB, range **1–5**, default **2 GB**). For configuration details, see [Checkmarx One CLI Config and Environment Variables](https://docs.checkmarx.com/en/34965-68624-checkmarx-one-cli-config-and-environment-variables.html#UUID-6c2fe558-13e9-31d8-738f-efd219cb8941_section-idm4554293728945633919364184784).
   
   - For sources larger than **5 GB**, it is recommended to increase the client timeout to reduce the risk of upload failures.
   {% endhint %}
- The full path to an SBOM file
   
   {% hint style="info" %}
   Relevant only for the SCA scanner, see [Scan using SCA Resolver](#scan-using-sca-resolver).
   {% endhint %}

{% hint style="info" %}
When a scan is run using multiple scanners, all scanners run in parallel.

When multiple scans are run in your account, the number of concurrent scans is specified in your account's license. This info is available under **Account Settings** > **License** > **License Plan Summary**. When the limit is exceeded, the scans are added to a queue which runs on a "first in first out" basis.
{% endhint %}

{% hint style="info" %}
When you scan a **folder** that contains files with unsupported file formats, those files aren't scanned.

However, you can include those files in the scan by using the **--file-include** flag.

For more details see [Scan with Inclusion of unsupported file formats](#scan-with-inclusion-of-unsupported-file-formats)
{% endhint %}

By default, scans include only supported files in the .zip archive submitted for scanning. The default file filters are applied to all scans.


The following is a list of the supported extensions and file names that are included by default in scans.


To include all files from the source location in the .zip archive, regardless of whether they are included in the supported files list, use the `--skip-default-filter` flag.


*.apex


*.apexp


*.asp


*.aspx


*.ascx


*.bas


*.build


*.c


*.cc


*.c++


*.cbl


*.cjs


*.cls


*.component


*.config


*.cpp


*.cs


*.cshtml


*.csproj


*.ctl


*.ctp


*.cts


*.cxx


*.dsr


*.dll


*.dart


*dock*


*Dockerfile*


*.eco


*.erb


*.frm


*.go


*.groovy


*.gsh


*.gvy


*.gy


*.h


*.hh


*.h++


*.hbs


*.hxx


*.htm


*.html


*.inc


*.java


*.javasln


*.jar


*.js


*.jsp


*.jspf


*.json


*.jsx


*.kt


*.kts


*.m


*.mjs


*.mts


*.object


*.page


*.php


*.php3


*.php4


*.php5


*.php56


*.phtm


*.phtml


*.pl


*.pm


*.plist


*.pkb


*.pck


*.pco


*.pks


*.pkh


*.plx


*.poetry.lock


*.project


*.properties


*.py


*.rb


*.report


*.requirement.txt


*.requirements.txt


*.rhtml


*.rjs


*.rs


*.rxml


*.scala


*.sc


*.sql


*.sln


*.sqb


*.swift


*.tag


*.tf


*.tfbacken


*.tfvars


*.tgr


*.tld


*.tpl


*.trigger


*.ts


*.tsx


*.twig


*.vb


*.vbs


*.vm


*.xml


*.xaml


*.xib


*.yaml


*.yarn.lock


build.gradle


build.sbt


composer.lock


Directory.Build.props


Directory.Packages.props


.dockerfile


go.mod


go.sum


Podfile


Podfile.lock


pyproject.toml

<details>

<summary>Excluded Folders</summary>

The following is a list of the folders that are automatically excluded from scans because their content is generally not relevant.

*.vs

*.vscode

*.idea

node_modules

</details>

## File Filters
There are three methods for applying filters to files and folders for Checkmarx One scans.

- [Filter Entire Scan: `--file-filter` & `--file-filter-ext`](#paligo-section-idm4646452074433633784700821514) - exclusions are applied during the pre-scan process, so that the excluded files aren't packaged into the .zip archive and are never uploaded to Checkmarx One.
- [Filters for Specific Scanners](#filters-for-specific-scanners) - apply filters for a specific scanner during the scan process, so that the specified scanner doesn't analyze the excluded files.
- [Apply `.gitignore` Exclusions](#apply-gitignore-exclusions) - exclude files and directories from the scan based on the patterns defined in the directory's .gitignore file

{% hint style="info" %}
File filtering mechanisms operate at different stages of the scan flow:

- `--file-filter` and `--file-filter-ext` affect which files are packaged in the .zip archive and uploaded to Checkmarx One. Files excluded by these filters are removed before the archive is created and are therefore not uploaded, are not available to any scanner, and cannot be restored by scanner-specific filters or filters applied in the web application (UI).
- Scanner-specific CLI filters, as well as filters applied in the project's settings via the web application (UI), only affect which uploaded files are analyzed by individual scanners.

Filters configured in the project's settings via the web application (UI) behave the same way as scanner-specific CLI filters: they only affect which files are analyzed by a scanner and do not affect the preparation of the .zip archive.

When filters are configured in the UI:

- if **Allow Override** is disabled, scanner-specific CLI filters do not take effect.
- If **Allow Override** is enabled, scanner-specific CLI filters override the UI filters.

UI filters do not override `--file-filter` or `--file-filter-ext`. If a file is excluded by either of these flags, it is removed before the .zip archive is created and cannot be scanned by any scanner, even if it is explicitly included by a UI filter.
{% endhint %}

<a id="paligo-section-idm4646452074433633784700821514"></a>

### Filter Entire Scan: `--file-filter` & `--file-filter-ext`
The `--file-filter` and `--file-filter-ext` flags provide the ability to filter the scanned file list as follows:

- Include files, file extensions.
- Exclude files, file extensions and folders.

The `scan create` command first applies the `--file-include` flag (or the default list of included file types) to establish the baseline of which files to include in the scan. It then further refines the file selection by applying the filters specified using `--file-filter` or `--file-filter-ext` .

**Limitation:** The `--file-filter` and `--file-filter-ext` flags work only if the scanned source code is a <u>directory</u> or a <u>ZIP file</u> (not a Git repository). However, this limitation does not apply when using the filter flags for specific scanners, see [Filters for Specific Scanners](#filters-for-specific-scanners).

The `--file-filter` flag supports wildcard-based filtering.


**Supported Functionality:**

- Use the `*` wildcard to match files.
   
   For example, `*.html` matches files with the `.html` extension.
- Use the `!` prefix to exclude files, file extensions, and folders.
   
   For example: `!*.html,!src*`
   
   {% hint style="info" %}
   When using `!` to exclude content, enclose the argument in single quotes.
   
   For example, `--file-filter '!mycompany.jar'`
   
   For more details see [Scan with Exclusion of Specific File or File Type](#scan-with-exclusion-of-specific-file-or-file-type)
   {% endhint %}
- Include files and file extensions.
   
   For example:
   
   - `t*` includes all files starting with `t`.
   - `*.txt` includes all files with the `.txt` extension.


**Limitations**


- Full paths are not supported. Therefore, you can only exclude an entire top-level folder, not a specific subfolder.
   
   For example, for the following file structure:
   
   `CxONE_TEST\apps\feature1\components\..`
   
   `CxONE_TEST\apps2\feature1\components\..`
   
   `CxONE_TEST\apps2\feature2\components\..`
   
   You can exclude all content under `apps2`, but you cannot exclude only the content under `feature2` or a specific component.
- `.git` folders and subfolders cannot be excluded.

### `--file-filter-ext`
The `--file-filter-ext` flag enables you to include or exclude files and folders using Apache Ant-style glob patterns. Ant-style glob patterns provide directory-aware, recursive matching across complex project structures.

For example:

- `**/*.java` — includes `.java` files recursively across directories.
- `!**/test/**` — excludes content under `test` directories recursively.

### Filters for Specific Scanners
The following flags are used to apply filters to SAST, IaC Security and SCA scanners respectively: `--sast-filter`, `--iac-security-filter`, `--sca-filter`. You can use these flags to specify file types.

{% hint style="info" %}
The filters for specific scanners **can** be used for all types of scans (directory, zip file or GIT repo), as opposed to `--file-filter` which does not work on GIT repositories.
{% endhint %}

{% hint style="info" %}
The `--sca-filter` flag is only used when the package resolution is done in the cloud (default). However, if you are using SCA Resolver to run package resolution locally, then file exclusion is done as follows: `--sca-resolver-params "--excludes <string>"`.
{% endhint %}

### Examples
The following are some examples of how these flags can be used:

- for inclusion - `--sast-filter *.java`,
- for exclusion - `--sast-filter !*.java` or `--sca-filter !**\Dockerfile`

The following are a few examples:

- **Exclude all java files:** !**/*.java
- **Exclude all files inside a folder Test:** `!**/Test/**`
- **Exclude all files under root folder Test:** !Test/**
- **Exclude just the files inside a folder leaving all subfolders content:** !**/Test/*
- **Exclude all JavaScript minified files:** !**/*.min.js

If you would like to include only files inside specific folders, you need to first do a global exclude and then you can specify the folders to include.

For example:

`--sast-filter  !**/**,**/Folder01/**,**/Folder02/**` would cause the SAST scanner to run only on files inside “Folder01” and “Folder02”.

{% hint style="info" %}
For additional details about the syntax used for these filters, see [Flags](#paligo-id_scancreate-Flags). Learn more about glob patterns syntax [here](https://en.wikipedia.org/wiki/Glob_(programming)).
{% endhint %}

### Filters for Container Security Scanner
Container Security has a specialized set of filter settings that enable users to configure their scans for precision and relevance. Filters can be applied to files, folders, packages and images. The following filter options are available:

- `--containers-package-filter` - Exclude packages by package name or file path using regex.
- `--containers-file-folder-filter` - Specify files and folders to be included or excluded from scans.
- `--containers-image-tag-filter` - Exclude images by image name and/or tag.
- `--containers-exclude-non-final-stages` - Scan only the final deployable image.

For additional details about the usage and syntax for these filters, see [Filters for Container Security Scanner](#filters-for-container-security-scanner).

### Apply ".gitignore" Exclusions
When the flag `--use-gitignore` is submitted, Checkmarx One excludes files and directories from the scan based on the patterns defined in the directory's .gitignore file.

You can also pass the `use-gitignore` option using the global [`--optional-flags`](https://docs.checkmarx.com/en/34965-68626-global-flags.html) parameter.

### Requirements
- Relevant only when scanning from a .zip file or a local directory, not when scanning from a code repository URL.
- There must be a .gitignore file present in the root directory of the repository.

<details>

<summary>Supported Patterns</summary>

The following patterns are currently supported when using the `--use-gitignore` flag:

| Pattern | Description |
| --- | --- |
| - `src/`<br>- `**/src`<br>- `src/**` | Each of these patterns ignores any directory named 'src' regardless of its location or contents. |
| application-jira.yml | Ignores a specific file named application-jira.yml |
| *.yml | Ignores all files ending with .yml extension |
| LoginController[0-3].java | Ignore files has names with a single digit 0 to 3 at the end, like LoginController0.java or LoginController1.java |
| LoginController[!0-3].java | Ignore files has names with a single digit except 0 to 3 at the end, like LoginController4.java or LoginController5.java |
| LoginController[01].java | Ignore files has names with a single digit 0 or 1 at the end, like LoginController0.java or LoginController1.java |
| LoginController[!456].java | Ignore files has names with a single digit except 4,5 or 6 at the end, like LoginController0.java or LoginController1.java |
| ?pplication-jira.yml | Ignores files with any single character prefix before pplication-jira.yml |
| `a*cation-jira.yml` | Ignores files starting with a and ending with cation-jira.yml |

</details>

<details>

<summary>Not Supported Patterns</summary>

The following patterns are not supported due to limitations in relative or recursive path handling, such as recursive wildcards (**) or relative paths:

{% hint style="info" %}
All patterns that are not supported via .gitignore are also not supported using `--file-filter`.
{% endhint %}

| Pattern | Description |
| --- | --- |
| /webapp/.jsp | Ignores .jsp files inside any webapp folder |
| `main_modules/**/temp/` | Ignores all files inside any temp folder under main_modules |
| `main_modules/**/.js` | Ignores all .js files under main_modules at any depth |
| /application-jira.yml | Ignores only the root-level application-jira.yml |
| /config/.yml | Ignores .yml files inside the root-level config folder |

</details>

## Checkmarx SCA Resolver
[Checkmarx SCA Resolver](https://docs.checkmarx.com/en/34965-581793-using-sca-resolver-in-checkmarx-one.html) is an on-prem utility that enables you to resolve and extract dependencies and fingerprints from your source code and send them to the Checkmarx One SCA scanner for risk analysis. This enables you to run a comprehensive SCA scan without the need to send your actual source code to the cloud. It also enables you to scan private (local) dependencies that aren’t accessible to the Checkmarx SCA cloud platform. For Checkmarx One users, Resolver is used in Offline mode for dependency resolution and the results file is then sent for analysis via your Checkmarx One account.

In order to use the SCA Resolver with the Checkmarx One CLI, you need to download the Checkmarx SCA Resolver separately in a location that the Checkmarx One CLI can find. Find the latest download at [Checkmarx SCA Resolver Download and Installation](https://docs.checkmarx.com/en/34965-19197-checkmarx-sca-resolver-download-and-installation.html).

To use the SCA Resolver, you need to add the **--sca-resolver** flag to your command line with an argument with the path to your local installation of the Resolver executable. See example below, [Scan using SCA Resolver](#scan-using-sca-resolver).

{% hint style="warning" %}
When running a CLI scan that uses SCA Resolver, the source code must be in a local folder, not in a zip archive or a code repository.
{% endhint %}

The Delta Scan feature will run by default on the CxOne CLI (since version 2.3.44) scans using SCAResolver (since version 2.13.3). To disable this feature, use the **--sca-resolver-params** flag with the argument **--disable-delta-scan**. For more information on this feature, see [Delta Scans](https://docs.checkmarx.com/en/34965-322318-sca-scanner.html#delta-scans).

To add additional arguments to Checkmarx SCA Resolver, use the flag **--sca-resolver-params** with any additional arguments that you need. If necessary to use spaces and/or quotes, wrap the arguments in double quotes and use single quotes inside the value. For a complete list of SCA Resolver configuration arguments, see [Checkmarx SCA Resolver Configuration Arguments](https://docs.checkmarx.com/en/34965-132888-checkmarx-sca-resolver-configuration-arguments.html).

{% hint style="info" %}
Only arguments that can be used in **Offline** mode can be applied to scans run via the Checkmarx One CLI Tool and plugins.
{% endhint %}

<details>

<summary>Alternative Method</summary>

There is an alternative method that offers maximum control over the files being sent to the cloud for analysis. This is done by first running a scan using Resolver in offline mode on-prem. You can then run the scan create command in Checkmarx One and provide only the results file for upload. The following procedure describes this method.

1. Run SCA Resolver in offline mode and save the results to a file named `.cxsca-results.json` (precise name required) in the root path of your Checkmarx One CLI.
   
   ```
   ./ScaResolver offline -r "./cx-results/.cxsca-results.json" -s "%LOCATION_PATH%"
   ```
1. Run the `scan create` command in Checkmarx One, with the `-s` argument pointing to the folder where the Resolver results file was saved. For `--scan-types`, specify only `sca`.
   
   ```
   ./cx scan create -s "./cx-results/" --project-name "DemoProject" --branch "DemoBranch" --scan-types "sca"
   ```

</details>

For more information about using SCA Resolver in Checkmarx One CI/CD integrations, see [Using SCA Resolver in Checkmarx One CI/CD Integrations](https://docs.checkmarx.com/en/34965-68725-using-sca-resolver-in-checkmarx-one-ci-cd-integrations.html).


## Threshold
Configuring thresholds enables users to specify a threshold of vulnerability severities that, when found in a scan, will cause Checkmarx One to return a fail code for the scan. Users can then configure pipelines to break builds upon scan failure, so that scans that hit the threshold will break the build.

The threshold option supports a shorthand syntax with the format being a semi-colon separated list of key-value pairs.

The format for thresholds is **`<engine>-<severity>=<limit>`**

- Options for **engine**: sast, iac-security, sca, api-security, containers, sscs-secret-detection, sscs-scorecard
- Options for **severity**: Critical, High, Medium, Low, Info (Info is only for SAST engine)
- Options for **limit**: A number equal to or greater than 1

More than one threshold can be defined for each engine and thresholds can be set for multiple engines. Multiple thresholds should be separated by a semi-colon. An OR operator is applied, so that if any one of the thresholds is reached the scan will fail.

For example, to set the threshold for SAST as 10 high severity or 20 medium severity vulnerabilities, and for SCA as 10 high severity vulnerabilities, use the following syntax:

```
--threshold "sast-high=10; sast-medium=20; sca-high=10; containers-high=5"
```

{% hint style="info" %}
If a `--filter <string>` is applied to the `scan create` command, then the threshold applies with respect to the filtered vulnerability count.

**For example**:

If recurrent vulnerabilities are not a concern, you can set the filter to `status=NEW`, so that only `NEW` vulnerabilities are counted when determining whether the threshold was reached.
{% endhint %}


## Reports
You can generate reports for the scan results as part of the `scan create` command.

{% hint style="info" %}
You can also generate reports for previous scans using the [results show](68641-results-show.md) command.
{% endhint %}

There are two main types of reports:

- **Scan summary report** - gives a summary of the scan results, including the number of risks of various types and severity levels that were identified by the scan. This type of report is available in HTML, json, console and markdown format.
- **Complete scan report** - a comprehensive report showing details about each of the risks identified in the scan. This type of report can be generated in json, sarif or sonar format.
   
   {% hint style="info" %}
   Reports generated via the CLI use the standard scan report format. There is a newer type of customized scan report that can be generated via [API](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/ci2py4oc7hlt3-improved-reports-service-rest-api) or from the [web application](https://docs.checkmarx.com/en/34965-182434-checkmarx-one-reporting.html).
   {% endhint %}

You can also generate PDF reports, for which you can specify which sections you would like to include in the report. In addition, for PDF reports, you can specify one or more email recipients who will receive an email with a download link for the report.

To generate a report as part of the `scan create` command, add the `--report-format` flag, specifying the format you would like to generate.

For PDF reports, use the following flags to specify email recipients and to specify which sections to include in the report.

```
./cx scan create --project-name <Project Name> -s <path> --branch <branch name> --report-format pdf --report-pdf-email <recipient_email> --report-pdf-options <specify_sections>
```

For information about the content of scan reports, see [Scan Reports](https://docs.checkmarx.com/en/34965-182434-checkmarx-one-reporting.html).

### SBOM Reports
You can generate SBOM reports for the open source packages identified in your project by the SCA scanner. Reports can be generated in [CycloneDX](https://cyclonedx.org/specification/overview/) and [SPDX](https://spdx.dev/about/) formats, with additional “property” fields showing supplemental risk data. The reports can be exported in XML (for CycloneDX only) or JSON format. You can generate SBOM reports for Checkmarx One projects on which the SCA scanner has run. For more info about Checkmarx SBOMs, see [SBOM Reports](#sbom-reports).

Example for generating a CycloneDX SBOM report in JSON format:

```
./cx scan create --project-name <Project Name> -s <path> --branch <branch name> --report-format sbom --report-sbom-format CycloneDxJson
```

### Generating an SBOM During Dependency Resolution
As an alternative to generating an SBOM from a completed SCA scan, you can use SCA Resolver together with the `--sbom-first` argument under `--sca-resolver-params` to generate a CycloneDX 1.7 SBOM immediately after dependency resolution completes. This approach can significantly reduce the time required to produce an SBOM because it does not require waiting for scan results.

{% hint style="info" %}
**Version requirements**: This capability is supported in Checkmarx One CLI version 2.3.54 and later, together with SCA Resolver version 2.14.3 and later.
{% endhint %}

To generate an SBOM while performing dependency resolution:

```
./cx scan create --project-name <Project Name> --scan-types sast,sca -s <path> --branch <branch name> --sca-resolver <path-to-resolver> --sca-resolver-params "--sbom-first"
```

The generated SBOM includes both manifest-resolved and binary-detected components and is written to the configured output directory.

{% hint style="info" %}
You can customize the generated SBOM file name and output location using the `--sbom-output-name` and `--sbom-output-path` SCA Resolver optional arguments. For more information, see [Optional Arguments](https://docs.checkmarx.com/en/34965-132888-checkmarx-sca-resolver-configuration-arguments.html#optional-arguments).
{% endhint %}

You can also generate an SBOM without running a scan by combining the `--sbom-first` argument with the `--no-scan` flag:

```
./cx scan create --project-name <Project Name> --scan-types sast,sca -s <path> --branch <branch name> --no-scan --sca-resolver <path-to-resolver> --sca-resolver-params "--sbom-first"
```

This command performs dependency resolution and generates an SBOM without submitting a scan to Checkmarx One.


## Container Security Scans
When running scans via the CLI you can choose to scan the project files in order to analyze the Dockerfile in your project or you can submit specific images for scanning.

### Authentication for Scanning Private Repos
In order to access private repos you need to be authenticated in your container repo at the time that you run the scan via Checkmarx One CLI.

{% hint style="info" %}
In addition, even when using public repos in DockerHub there is an advantage to authenticating your user in order to avoid the limits that apply to anonymous requests to public repos.
{% endhint %}

Authentication can be done via Docker or Podman.

Before running the scan, it is recommended to verify that you are able to access the image on your local machine.

For details about authentication for specific registries, see [Authentication for Scanning Private Repos](#authentication-for-scanning-private-repos).

<details>

<summary>Example - DockerHub Authentication</summary>

For DockerHub authentication make sure that your environment variables are set as:

- *DockerhubUsername* - your username
- *DockerhubToken* - your password or authorization token

</details>

### Scan Procedure
1. Run the `scan create` command with all required parameters, and specify `container-security` in the `--scan-types`.
   
   ```
   ./cx scan create --project-name <Project Name> -s <Repository URL> --branch <branch name> --scan-types container-security
   ```
1. If you want to scan only specific images (not an entire project), do the following:
   
   1. Create a "dummy" folder in your project (for use in the `-s` parameter) and give it a name that indicates that it is used for scanning images, e.g., scan_ecr_image.
   1. In the CLI scan command, for the `-s` parameter give the path to the "dummy" folder that you created, e.g., `/Users/DemoUser/scan_ecr_image`.
1. Add the `--container-images` flag followed by a comma separated list of images. Specify each image using the following syntax {image_name}:{image_tag}.
   
   ```
   ./cx scan create --project-name <Project Name> -s <Repository URL> --branch <branch name> --scan-types container-security --container-images "mycompany/myimage:myimagetag"
   ```
   
   {% hint style="info" %}
   For additional details about precise syntax for container references, see [Authentication for Scanning Private Repos](#authentication-for-scanning-private-repos) and [Scanning Container Images via Checkmarx One CLI - Flag Validation and Best Practices](https://docs.checkmarx.com/en/34965-515429-scanning-container-images-via-checkmarx-one-cli---flag-validation-and-best-practices.html).
   {% endhint %}


## Running Secret Detection and Repository Health Scans
When running a scan via the CLI tool, the [Secret Detection](https://docs.checkmarx.com/en/34965-387021-secret-detection-results-viewer.html) and [Repository Health (OSSF)](https://docs.checkmarx.com/en/34965-387022-repository-health--scorecard--results-viewer.html) scanners are grouped together under Software Supply Chain Security (SCS) scanner.

{% hint style="info" %}
When running the Scorecard scanner, it is mandatory to submit the repo url and an access token with at least read permissions for that repo.
{% endhint %}

**To run a Secret Detection and Repository Health scan:**

1. Prepare the command to run a scan, using the `scan create` command and specifying the project name, branch and zip file location or repository URL using the `--project-name` , `--branch` and `-s` flags.
   
   ```
   ./cx scan create --project-name <Project name> --branch <branch name> -s <path to zip archive>
   ```
1. By default, all licensed scanners are run, including SCS (assuming that all mandatory SCS parameters are specified). If you are using the `--scan-types` flag to specify the scanners that run, you need to explicitly include the `scs` scanner, e.g., `--scan-types sast,scs`.
1. By default, when scs is included, both Secret Detection and OSSF Scorecard are run. If you would like to run only one of these scanners, add the `--scs-engines` flag and specify the engine that you want to run: `secret-detection`, or `scorecard`.
1. Add `--git-commit-history=<true|false>` to enable or disable scanning Git commit history for Secret Detection. Default: false. Applies only when running `--scan-types scs` with `--scs-engines secret-detection`.
   
   Example:
   
   ```
   # Run Secret Detection (default: commit history disabled)
   cx scan create \
    --project-name demo --branch main -s . \
    --scan-types scs --scs-engines secret-detection
   # Run Secret Detection with commit history explicitly enabled
   cx scan create \
    --project-name demo --branch main -s . \
    --scan-types scs --scs-engines secret-detection \
    --git-commit-history=true
   ```
1. When running the scorecard scanner, it is mandatory to add the following flags:
   
   - `--scs-repo-url <string>` - specifying the URL of the repo that you are scanning.
      
      {% hint style="warning" %}
      Even when `-s` specifies a repo url, you still need to use this flag to submit the URL for the SCS scanner.
      {% endhint %}
   - `--scs-repo-token <string>` - specifying a token with read permission on the specified repo.
      
      {% hint style="info" %}
      This flag is required for both private and public repos.
      {% endhint %}
1. If you would like to generate a scan report (optional), add the `--report-format` flag, specifying the desired format (e.g., `--report-format json`). For more information about scan reports, see [here](https://docs.checkmarx.com/en/34965-68643-scan.html#UUID-a0bb20d5-5182-3fb4-3da0-0e263344ffe7_section-idm4631465209593633552409907579).
   
   {% hint style="warning" %}
   PDF format is not supported for the SCS scanner.
   {% endhint %}
1. Run the scan command.
   
   The following is an example of a command to run SAST on a zip archive and run Scorecard on the project's repo.
   
   ```
   user@laptop:~/ast-cli$ ./cx scan create -s . --branch master --project-name Test111 --scan-types sast,scs --scs-engines scorecard --scs-repo-url https://github.com/juice-shop/juice-shop --scs-repo-token <TOKEN> --report-format json
   ```


## Scanning SBOMs
You can run an SCA scan on an SBOM file. The scan is run as a Checkmarx One project, with the source specified as an SBOM file. The SCA scanner returns comprehensive results of all risks associated with your open source packages. This enables customers who don’t want to submit their actual code, to obtain comprehensive SCA results for their project and manage the remediation via Checkmarx One.

Requirements:

- Supported file formats: json or xml following CycloneDX (v1.0-1.7) or SPDX (v2.3)
- It is mandatory to include the Package URL (purl) for each package in the SBOM. For more information about purl syntax, see [here](https://spdx.github.io/spdx-spec/v3.0/model/Software/Properties/packageUrl/).
- Only the SCA scanner can run on an SBOM

{% hint style="info" %}
For complete documentation of SBOM scanning, see [Scanning SBOMs](https://docs.checkmarx.com/en/34965-728599-scanning-sboms.html)
{% endhint %}

**To scan an SBOM:**

1. For the `-s` parameter, submit the full path to the SBOM file.
1. For `--scan-types`, specify `sca`.
1. Add the `--sbom-only` flag.

```
./cx scan create --project-name <Project Name> -s <path_to_SBOM_file> --scan-types sca --sbom-only
```


### Exit Codes
When a scan finishes, it generates an exit code indicating whether or not the scan completed successfully. In case of failure, the exit code also indicates which scanner in particular failed.

These exit codes can be retrieved using a standard command in your shell, for example:

- Powershell - `$LastExitCode`
- CMD - `echo %ErrorLevel%`
- MAC - `echo $?`

The following is a list of possible exit codes:

<details>

<summary>Exit code - possible values</summary>

| Code | Explanation |
| --- | --- |
| 0 | All scanners completed successfully |
| 1 | Multiple scanners failed |
| 2 | SAST scanner failed |
| 3 | SCA scanner failed |
| 4 | IAC Security scanner failed |
| 5 | API Security scanner failed |

</details>

In addition, Checkmarx One provides a dedicated command, `results exit-code`, that retrieves detailed information about scan failures.


<a id="paligo-id_scancreate-Flags"></a>

## Flags
{% hint style="warning" %}
Whenever a parameter value (e.g., project name, file location etc.) has a space or other special character in it, it needs to be escaped either by enclosing it in double quotes (and using only single quotes within the value) or by using an escape character. The specific syntax for escaping characters will vary depending on the command-line interface or programming language you are using.
{% endhint %}

**`--apisec-swagger-filter <string>`**

Allow users to select specific folders or files that they want to include or exclude from the code scanning process. This setting applies only to the api-security scanner. Example: ./swagger.json

**`--async`**

Do not wait for scan completion.

**`--application-name <string>`**

Specify an application to which this project will be assigned.

{% hint style="info" %}
This is effective both when creating a new project as well when scanning an existing project. For existing projects, the new application is added but does not overwrite previously associated applications.
{% endhint %}

{% hint style="warning" %}
Adding an application to an existing project requires the permission `update-application`.
{% endhint %}

**`--branch <string>, -b <string>` Required**

Branch to scan.

This is a required flag even when scanning from a zip archive. If the zip archive doesn't represent a specific branch, you can submit `.unknown` as the value and it will be shown in the UI as "N/A". (You should not enter `N/A` as the value, as this will be misinterpreted by the system.)

**`--branch-primary`**

This flag sets the branch specified in `--branch` as the PRIMARY branch for the project.

**`--container-images <string>`**

If you would like to scan specific images, submit a comma separated list of images to be scanned. Specify each image using the following syntax {image_name}:{image_tag}. For the syntax for images in specific registries, see [Authentication for Scanning Private Repos](#authentication-for-scanning-private-repos).

{% hint style="warning" %}
This flag can only be used when the `container-security` scanner is running, see [--scan-types](#paligo-N6495b17deeb13).
{% endhint %}

**`--containers-exclude-non-final-stages`=boolean**

Exclude all images that are not from the final stage of the build process, so that only the final deployable image is scanned.

{% hint style="warning" %}
Only supported for Dockerfile images.
{% endhint %}

**`--containers-file-folder-filter <string>`**

Specify **files and folders** to be included (allow list) or excluded from (block list) scans.

Syntax:

- Including a file type - *.java
- Excluding a file type - !*.java
- Use “,” sign to chain file types
   
   for example: `*.java,*.js`
- The parameter also supports including/excluding folders.
- Regex is not supported.

**`--containers-image-tag-filter <string>`**

Exclude **images** by image name and/or tag.

Syntax:

- `image-name:image-tag` - exclude by image name and tag
- `image-name` - exclude by image name
- `:image-tag` - exclude by image tag

{% hint style="info" %}
You can use wildcard (*) at the beginning, end or both.
{% endhint %}

**`--containers-local-resolution`**

Use this flag to run the Container Security scanner locally. By default it runs in the cloud.

This flag should be used when you need to pull images from private registries that aren't integrated with your Checkmarx One account.

**`--containers-package-filter <string>`**

Prevent sensitive private **packages** from being sent to the cloud for analysis. Exclude packages by package name or file path using regex.

Syntax: Regex

**`--exlude-git-folder`**

Excludes the .git folder from the scan source upload ZIP.

You can also pass the `exclude-git-folder` option using the global [`--optional-flags`](https://docs.checkmarx.com/en/34965-68626-global-flags.html) parameter.

**`--file-filter <string>, -f <string>`**

Source file filtering pattern for including or excluding files and folders. Refer to [File Filters](#file-filters).

**`--file-filter-ext <string>`**

Source file filtering pattern using Apache Ant-style glob patterns for directory-aware and recursive matching. Refer to [File Filters](#file-filters).

**`--file-include <string>`**

Comma separated list of additional file extensions to be included in the scan.

For example: *.java2,file.txt

**`--file-source <string>, -s <string>` Required**

The path to the compressed zip file, the path to the folder, or the repository URL to scan.

When scanning a private repository, a PAT for the repo should be provided using the following format:

`https:/<username>:<pat>@github.com/<org>/<repo>.git`

**`--filter <string>`**

Filter the list of results.

- Use ',' to separate between multiple filters
- Use ';' as to separate between multiple values for a given filter
- Available filters are:
   
   project-names, scan-ids, tags-keys, tags-values, branches, statuses, initiators, source-origins, source-types.
- Options for **severity**, **state**, and **status**:
   
   - **severity** - Critical, High, Medium, Low, Info.
   - **state** - TO_VERIFY, NOT_EXPLOITABLE, PROPOSED_NOT_EXPLOITABLE, CONFIRMED, URGENT, EXCLUDE_NOT_EXPLOITABLE.
      
      {% hint style="info" %}
      The state filter can be applied either by submitting a separate value for each state to **include,** or by submitting the value `EXCLUDE_NOT_EXPLOITABLE` in order to exclude only `NOT_EXPLOITABLE`.
      {% endhint %}
   - **status** - NEW, RECURRENT, FIXED.

For examples of proper filter syntax, see [below](#paligo-section-idm33494586774988)

**`--help, -h`**

Help for the create command.

**`--iac-security-filter <string>`**

Filter option specific to IaC Security scan

- Including a file type - *.java
- Excluding a file type - !*.java
- Use "," sign to chain filter types.
   
   For example: `*.java,*.js`
- The parameter also supports including/excluding folders.

**`--iac-security-platforms <string>, <string>`**

Specify the platforms that you would like the IaC Security scan to run on.

When this flag is used, it overrides your account's default settings.

**`--iac-security-preset-id`**

This flag received a string (UUID) corresponding to the ID of the IaC Security Preset that can be extracted from the UI on the IaC Preset table.

**`--ignore-policy`**

Ignore policy violations, so that they will not break the build.

{% hint style="warning" %}
Requires `override-policy-management` permission, otherwise the policies will be enforced even when the flag is sent.
{% endhint %}

**`--no-scan`**

Prevents CxOne scan from running after SBOM is generated locally.

{% hint style="info" %}
Relevant only when --sbom-first is submitted under --sca-resolver-params. Submitting this flag without --sbom-first causes an error.
{% endhint %}

**`--output-name <string>` Default: "cx_result"**

Output file name.

**`--output-path <string>` Default: "."**

Output path.

**`--project-groups <string>`**

List of groups associated with projects.

For example: (groupA,groupB).

Limitation: This flag only works when creating a new project. For an existing project, it won't update the groups.

**`--project-name <string>` Required**

Name of the project.

When using the `--project-name` flag, the Project name must be written in **quotes** if there is a space in the project name.

For example: Test, Test1, "Test 1".

**`--project-private-package` NOT FULLY SUPPORTED YET Default: false**

You can designate a scan as a "Private Package" and assign a package version to it. Once a private package has been scanned, info about the risks affecting that package will be identified by SCA when that package version is used in any of you projects. You can download an article about private packages [here](https://checkmarx.atlassian.net/wiki/spaces/CR/pages/6594035713/Checkmarx+SCA+Resources#Private-Packages).

True = designate as private package.

False = not a private package.

When using this flag, you should also specify the package version using `--sca-private-package-version`.

**`--project-tags <string>`**

List of tags to associate to projects.

For example: (tagA,tagB:val, etc)

{% hint style="warning" %}
When this flag is used, the tags that are submitted overwrite any existing tags that were assigned to the project.
{% endhint %}

**`--proxy str <string>` Optional**

Proxy server to route Checkmarx One CLI network communication through.

Format: `http://<proxy_ip>:<port>` or `http://<username>:<password>@<proxy_ip>:<port>`.

When specified, the protocol prefix (`http://` or `https://`) is required.

<a id="paligo-N64959fc01f899"></a>

**`--report-format <string>` Default: summaryConsole**

Report output format.

Specify one of the following:

json, json-v2, summaryHTML, summaryJSON, summaryCONSOLE, sarif, gl-sast, gl-sca, sonar, markdown or PDF, SBOM

{% hint style="info" %}
json-v2 is similar to the original json report. The main difference being that v2 is identical to the json report generated via the UI.
{% endhint %}

Report formats json, sarif, gl-sast and sonar generate complete scan reports (gl-sast returns only sast results and gl-sca returns only SCA results).

Report formats summaryHTML, summaryJSON, summaryCONSOLE and markdown generate summary reports.

For SBOM reports, you need to add the `--report-sbom-format` flag to specify the SBOM standard and output format.

**`--report-pdf-email <string>`**

Specify email recipients who will receive the pdf report. Multiple emails are separated by a ",".

This flag can only be used when `--report-format` is set as `pdf`.

**`--report-pdf-options <string>` Default: All Sections**

Specify the sections that will be included in the pdf format report.

This flag can only be used when `--report-format` is set as `pdf`.

Available sections are: `Sast`, `Sca`, `Iac-Security`, `ScanSummary`, `ExecutiveSummary`, and `ScanResults`.

`ScanResults` includes results for all scanners (IaC-Security, Sast and Sca).

**`--report-sbom-format` Default: CycloneDxJson**

The type of SBOM standard ([CycloneDX](https://cyclonedx.org/specification/overview/) or [SPDX](https://spdx.dev/about/)) as well as the output format.

Specify one of the following:

CycloneDxJson, CycloneDxXml, SpdxJson

This needs to be specified when the `--report-format` is set to "SBOM".

**`--resubmit`**

Apply the configurations used in the most recent scan in this project branch to the current scan.

Even when this flag is used, if an argument in the current scan differs from the configuration of the previous scan, the argument in the current scan takes precedence.

**`--sast-fast-scan`=boolean**

`true` - Run SAST scan using [Fast Scan mode](https://docs.checkmarx.com/en/34965-68538-configuring-projects.html#fast-scan) mode.

`false` - Do not run SAST scan using Fast Scan mode.

{% hint style="info" %}
If this flag is sent with no value (not recommended), then it is interpreted as `true`. If the flag is not sent then the default project or account settings are applied.
{% endhint %}

**`--sast-filter <string>`**

Filter option specific to SAST engine or scan.

- Including a file type - *.java
- Excluding a file type - !*.java
- Use "," sign to chain filter types.
   
   For example: `*.java,*.js`
- The parameter also supports including/excluding folders.

**`--sast-incremental`=boolean**

`true` - Run SAST scan as an [Incremental](https://docs.checkmarx.com/en/34965-68557-scanning-projects.html#incremental-scans) scan.

`false` - Do not run SAST scan as Incremental (i.e., run full scan).

{% hint style="info" %}
If this flag is sent with no value (not recommended), then it is interpreted as `true`. If the flag is not sent then the default project or account settings are applied.
{% endhint %}

**`--sast-light-queries`=boolean**

`true` - Run SAST scan as a [Light Queries](https://docs.checkmarx.com/en/34965-324470-sast-scanner.html#light-queries) scan.

`false` - Do not run SAST scan as LIght Queries (i.e., run standard queries).

{% hint style="info" %}
If this flag is not sent then the default project or account settings are applied.
{% endhint %}

**`--sast-preset-name <string>`**

The name of the Checkmarx preset to use.

**`--sast-recommended-exclusions`=boolean**

`true` - Run SAST scan using predefined exclusion rules.

`false` - Run SAST scan including all files and directories in the scan.

{% hint style="info" %}
If this flag is not sent then the default project or account settings are applied.
{% endhint %}

**`--sbom-only`**

Use this flag to run a scan only on the sbom at the specified file path.

Supported for CycloneDX (v1.0-1.7) and SPDX (v2.3) in xml or json format. For more information, see [SBOM documentation](https://docs.checkmarx.com/en/34965-322318-sca-scanner.html).

{% hint style="success" %}
Relevant only when running scans using the SCA scanner.
{% endhint %}

**`--sca-hide-dev-test-dependencies`**

Adding this flag filters out dev and test dependencies from SCA results shown in scan reports.

Note: This flag is only relevant when running a scan with the SCA scanner and using the [--report-format](#paligo-N64959fc01f899) flag to generate a report. Currently, this is not supported for PDF or SBOM reports.

**`--sca-exploitable-path <string>`**

Enable/disable the Exploitable Path feature for this scan.

`true` = enabled

`false` = disabled

{% hint style="info" %}
This flag must be sent with a value of `true` or `false`. If the flag is not sent, then the default project or account settings are applied.
{% endhint %}

Learn more about [Exploitable Path](https://docs.checkmarx.com/en/34965-19120-exploitable-path.html).

**`--sca-filter <string>`**

Filter option specific to SCA engine or scan.

{% hint style="info" %}
This flag is only used when the package resolution is done in the cloud (default). However, if you are using SCA Resolver to run package resolution locally, then file exclusion is done as follows: `--sca-resolver-params "--excludes <string>"`.
{% endhint %}

- Including a file type - *.java
- Excluding a file type - !*.java
- Use "," sign to chain file types.
   
   For example: `*.java,*.js`
- The parameter also supports including/excluding folders.

**`--sca-last-sast-scan-time <integer>` Default: 1**

Specify the number of days that SAST scan results are considered valid for use in Exploitable Path (i.e., if there is no current SAST scan, how many days prior to the current SCA scan will Checkmarx One look for a SAST scan to use for analyzing Exploitable Path).

Options: integer ≥ 1

{% hint style="success" %}
Only **full** SAST scans are used for Expoitable Path, results from incremental scans aren't considered.
{% endhint %}

{% hint style="warning" %}
The `--sca-last-sast-scan-time` flag is only supported for single-tenant environments, not for multi-tenant.
{% endhint %}

**`--scan-info-format <string>` Default: list**

- Selects the scan info output format.
- Select one of the follwoing formats:
   
   list, table, json

**`--scan-timeout <int>`**

Cancel the scan and fail after the timeout in minutes.

<a id="paligo-N6495b17deeb13"></a>

**`--scan-types <string>` Default: all scanners licensed for your account**

Scan engines to be run for this scan.

For example: (sast,iac-security,sca,api-security,container-security,scs,aisc).

**`--sca-private-package-version` NOT FULLY SUPPORTED YET Default: False**

When you designate a scan as a private package using the `--project-private-package` flag, you should also specify the package version using this flag.

e.g., 0.1.1

You can download an article about private packages [here](https://checkmarx.atlassian.net/wiki/spaces/CR/pages/6594035713/Checkmarx+SCA+Resources#Private-Packages).

**`--sca-resolver-params <string>`**

Additional arguments to use with CxSCA Resolver. The arguments can be found [here](https://docs.checkmarx.com/en/34965-132888-checkmarx-sca-resolver-configuration-arguments.html). The SCA Resolver runs in **offline mode**, only arguments compatible with this mode will work. The resolver params must be enclosed in quotes "", see example below.

**`--sca-resolver <string>`**

Use Checkmarx SCA Resolver to locally resolve SCA project dependencies. Specify the path to your local installation of SCA Resolver binary (executable).

When running a CLI scan that uses SCA Resolver, the source code must be in a local folder, not in a zip archive or a code repository.

**`--scs-engines <string>` Default: All supported SCS scanners**

SCS scan engines to run for this scan. Options: `secret-detection`,`scorecard`

This flag can only be used when the scs scanner is used for the scan (either by default or by specifying it in `--scan-types`).

**`--git-commit-history <boolean>` Default: false**

Enable/disable Git commit history scanning for Secret Detection.

- `true` = scans source code + Git commit history
- `false` = scans source code only

{% hint style="info" %}
This flag is only relevant when running the scs scanner with `--scs-engines secret-detection`.
{% endhint %}

**`--scs-repo-url <string>`**

Specify the URL of the repo that you are scanning.

{% hint style="warning" %}
Even when `-s` specifies a repo url, you still need to use this flag to submit the URL for the SCS scanner.
{% endhint %}

**`--scs-repo-token <string>`**

Submit a token with read permission on the specified repo.

{% hint style="info" %}
This flag is required for both private and public repos.
{% endhint %}

**`--skip-default-filter`**

Includes all files from the source location in the .zip archive, regardless of whether they are included in the supported files list.

**`--ssh-key <string>`**

Path to ssh private key.

**`--tags <string>`**

List of tags associated to scans.

For example: (tagA,tagB:val,etc)

**`--threshold <string>`**

Threshold count of severity of scan results based on the engine.

The threshold format is:

`<engine>-<severity>=<limit>`

For more information, see [Threshold](#threshold).

**`--use-gitignore`**

Adding this flag excludes files and directories from the scan based on the patterns defined in the directory's `.gitignore` file. For more information, see [Apply `.gitignore` Exclusions](#apply-gitignore-exclusions).

**`--wait-delay <int>` Default: 5 seconds**

Polling wait time (seconds) to get scan status.


## Examples
### Scan from a Git repository
```
./cx scan create --project-name <Project Name> -s <Repository URL> --branch <branch name>
```

Sample command:

```
C:\ast-cli_2.0.53_windows_x64>cx scan create  --project-name elidemo -s https://github.com/juice-shop/juice-shop --branch master
```

Sample response:

```
Scan ID      : 492e1626-9489-4ee9-ac1b-628de56c5e33
Project ID   : a1b1b151-d763-4f34-bfbc-de8c1422c02c
Project Name : elidemo
Status       : Running
Created at   : 08-07-23
Branch       : master
Tags         : []
Type         : Full
Timeout      : NONE
Initiator    : eli
Origin       : ASTCLI 2.0.53
Engines      : [ sast kics sca apisec]

2023/08/07 22:14:02 Scan Finished with status:  Completed
            Scan Summary:
              Created At: 2023-08-07, 22:07:57
              Project Name: elidemo
              Scan ID: 492e1626-9489-4ee9-ac1b-628de56c5e33

            Results Summary:
              Risk Level: High Risk

              -----------------------------------
              API Security - Total Detected APIs: 0
              -----------------------------------

            Policy Management Violation:
              Policy: DemoHigh | Break Build: false | Violated Rules: highVulnerability;

              Total Results: 170
              -----------------------------------
              |             High: 90            |
              |           Medium: 66            |
              |              Low: 13            |
              |             Info: 1             |
              -----------------------------------
              |     IAC-SECURITY: 41            |
              |             SAST: 0             |
              |   APIS WITH RISK: 0             |
              |              SCA: 129           |

              Checkmarx One - Scan Summary & Details: https://eu.ast.checkmarx.net/projects/a1b1b151-d763-4f34-bfbc-de8c1422c02c/scans?id=492e1626-9489-4ee9-ac1b-628de56c5e33&branch=master
```

### Scan from a private Git repository
```
./cx scan create --project-name <Project Name> -s <https:/<username>:<pat>@github.com/<org>/<repo>.git> --branch <branch name>
```

Sample command:

```
C:\ast-cli_2.0.53_windows_x64>cx scan create  --project-name elidemo -s https://myPrivateRepo:1234567abcde@github.com/demoOrg/demoRepo --branch master
```

### Scan from a source directory
```
./cx scan create -s <path> --branch <branch name> --project-name <Project Name>
```

Sample command:

```
user@laptop:~/ast-cli$ ./cx scan create -s . --branch main --project-name Test111
```

### Scan in asynchronous mode
```
./cx scan create --project-name <Project Name> -s <Repository URL> --branch <branch name> --async
```

Sample command:

```
user@laptop:/AST$ ./cx scan create --project-name demo -s . --branch main --async
```

### Scan using specific scanners
```
./cx scan create --project-name <Project Name> -s <Repository URL> --branch <branch name> --scan-types <scan types>
```

Sample command:

```
user@laptop:/AST$ ./cx scan create --project-name demo -s . --branch main --scan-types iac-security
```

### Scan using SCA Resolver
```
./cx scan create --project-name <Project Name> -s <path> --branch <branch name> --sca-resolver <path-to-resolver> --sca-resolver-params <additional-resolver-arguments>
```

Sample command:

```
user@laptop:/AST$ ./cx scan create --project-name demo --scan-types sast,sca -s . --sca-resolver /sca/scaResolver --sca-resolver-params "-q -e my_file" --async
```

### Scan with Inclusion of unsupported file formats
```
./cx scan create -s <path> --branch <branch name> --project-name <Project Name> --file-include <string>
```

Sample command:

```
user@laptop:~/ast-cli$ ./cx scan create -s ./Source-Folder/ --branch main --project-name Test111 --file-include sample.txt,*.myextension
```

### Scan with exclusion of specific file or file type
```
./cx scan create -s <path> --branch <branch name> --project-name <Project Name> --file-filter <string>
```

Sample command:

```
user@laptop:~/ast-cli$ ./cx scan create -s scan_files/ --branch main --project-name Test111 --file-filter !*mycompany*.jar
```

### Scan with exclusion of a specific folder
```
./cx scan create -s <path> --branch <branch name> --project-name <Project Name> --file-filter <folder name>
```

Sample command:

```
user@laptop:~/ast-cli$ ./cx scan create -s scan_files/ --branch main --project-name Test111 --file-filter !main
```

### Scan with threshold
```
./cx scan create --project-name <Project Name> -s <path> --branch <branch name> --threshold <engine>-<severity>=<limit>
```

Sample command:

```
user@laptop:/ast-cli$ ./cx scan create --project-name myproject -s my_file.zip --branch main --threshold sast-high=1
```

Sample response:

```
Created At: 2022-01-26, 11:24:20
               Risk: High Risk
         Project ID: 49e6d565-933b-4a55-8d08-ec026ddcd7e2
            Scan ID: bdab6a9e-eb90-4cab-8783-5c3a2a052b31
       Total Issues: 28
        High Issues: 3
      Medium Issues: 11
         Low Issues: 14
IaC Security Issues: 18
      CxSAST Issues: 9
       CxSCA Issues: 1
2022/01/26 11:25:14 Threshold check finished with status Failed : sast-high: Limit = 1, Current = 2 |
```

### Scan and send report to email recipient
```
./cx scan create --project-name <Project Name> -s <path> --branch <branch name> --report-format pdf --report-pdf-email <recipient_email> <specify_sections>
```

Sample command:

```
user@laptop:/ast-cli$ ./cx scan create --project-name EliCLIDemo -s . --branch main --report-format pdf --report-pdf-email demo@example.com ExecutiveSummary
```

Sample response:

```
2023/08/07 22:30:45 Scan Finished with status:  Completed
2023/08/07 22:30:56 Sending PDF report to:  [demo@example.com]
            Scan Summary:
              Created At: 2023-08-07, 22:24:56
              Project Name: elidemo
              Scan ID: 861ce408-f355-4692-9bff-3d35a6c17170

            Results Summary:
              Risk Level: High Risk

              -----------------------------------
              API Security - Total Detected APIs: 0
              -----------------------------------

            Policy Management Violation:
              Policy: EliHigh | Break Build: false | Violated Rules: high;

              Total Results: 170
              -----------------------------------
              |             High: 90            |
              |           Medium: 66            |
              |              Low: 13            |
              |             Info: 1             |
              -----------------------------------
              |     IAC-SECURITY: 41            |
              |             SAST: 0             |
              |   APIS WITH RISK: 0             |
              |              SCA: 129           |

              Checkmarx One - Scan Summary & Details: https://eu.ast.checkmarx.net/projects/a1b1b151-d763-4f34-bfbc-de8c1422c02c/scans?id=861ce408-f355-4692-9bff-3d35a6c17170&branch=master
```

<a id="paligo-section-idm33494586774988"></a>

### Scan and generate report with filtered content
```
./cx scan create --project-name <Project Name> -s <path> --branch <branch name> --report-format <format> --filter <filter_type>=<value>;<value>
```

Sample command:

```
user@laptop:/ast-cli$ ./cx scan create --project-name EliCLIDemo -s . --branch main --report-format json --filter state=TO_VERIFY;CONFIRMED;URGENT --filter status=NEW --filter severity=critical;high
```

