# results exit-code

The `results exit-code` command is used to retrieve information about the completion status for a particular scan in Checkmarx One. It also returns detailed information about failures of specific scan engines.


## Usage
```
./cx results exit-code --scan-id <scan ID> [flags]
```


## Flags
**`--scan-id <string>` Required**

The unique identifier of the scan for which you would like to retrieve the exit code info.

**`--scan-types <string>` Default: Returns data for each scanner that failed**

The scanners for which you would like to retrieve exit code info. You can submit multiple scanners, separated by a comma. Possible values are: sast,sca,iac-security,api-security,aisc

**`--help, -h`**

Help for the results exit-code command.


## Examples
### Retrieving exit code info for a particular scanner
```
./cx results exit-code  --scan-id <scan ID> --scan-types <scanner type>
```

Sample command:

```
C:\ast-cli_2.0.53_windows_x64>cx results exit-code --scan-id df16d6b8-213c-4525-ad3d-36977d4f2b2d --scan-types sast
[
  {
    "Name": "sast".
    "Status": "Failed",
    "Details": "Failed to get preset",
    "ErrorCode": "1024100"
  }
]
```

