# results codebashing

The `results codebashing` command is used to **retrieve Codebashing links** from Checkmarx One.


{% hint style="warning" %}
In order to use this command, you need to have a Codebashing account that has been linked to your Checkmarx One account. Please contact your Checkmarx support representative for assistance.
{% endhint %}


## Usage
```
./cx results codebashing [flags]
```


## Flags
**`--help, -h`**

Help for the results command.

**`--cwe-id <string>` Required**

CWE ID for the vulnerability.

**`--format <string>` Default: json**

The output format for the response. Possible values are `json`, `list` or `table`.

**`--language <string>` Required**

Language of the vulnerability.

**`--vulnerability-type <string>` Required**

Vulnerability type.


## Examples
### Retrieving codebashing link
```
./cx results codebashing  --language <language> --vulnerabity-type <vulnerability type> --cwe-id <cwe ID>
```

Sample command:

```
C:\ast-cli_2.0.53_windows_x64>cx results codebashing --language PHP --vulnerability-type Reflected XSS All Clients --cwe-id 79
```

