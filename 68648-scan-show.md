# scan show

The `show` command is used to **retrieve information about a scan** in Checkmarx One.


## Usage
```
./cx scan show --scan-id <scan id> [flags]
```


## Flags
**`--format <string>` Default: table**

The output format for the response. Possible values are `json`, `list` or `table`.

**`--scan-id <string>` Required**

Scan ID to show.

**`--help, -h`**

Help for the show command.


## Examples
### Using the scan show command with default settings
```
C:\ast-cli_2.0.53_windows_x64>cx scan show --scan-id 0f405e10-10c4-4fe9-a356-86253a52ab20

Scan ID                              Project ID                           Project Name Status  Created at Branch Tags Type Timeout Initiator Origin        Engines                
-------                              ----------                           ------------ ------  ---------- ------ ---- ---- ------- --------- ------        -------                
0f405e10-10c4-4fe9-a356-86253a52ab20 a1b1b151-d763-4f34-bfbc-de8c1422c02c elidemo      Partial 08-05-23   master []   Full NONE    eli       ASTCLI 2.0.53 [sast kics sca apisec]
```

### Using the scan show command with format flag
```
C:\ast-cli_2.0.53_windows_x64>cx scan show --format json --scan-id 0f405e10-10c4-4fe9-a356-86253a52ab20
{"ID":"0f405e10-10c4-4fe9-a356-86253a52ab20","ProjectID":"a1b1b151-d763-4f34-bfbc-de8c1422c02c","ProjectName":"elidemo","Status":"Partial","CreatedAt":"2023-08-05T23:25:06.290004+03:00","UpdatedAt":"2023-08-05T20:28:43.918848Z","Branch":"master","Tags":{},"SastIncremental":"Full","Timeout":"NONE","Initiator":"eli","Origin":"ASTCLI 2.0.53","Engines":["sast","kics","sca","apisec"]}
```

