# scan cancel

The `cancel` command is used to **cancel one or more running** **scans** in Checkmarx One.


## Usage
```
./cx scan cancel --scan-id <scan ID> [flags]
```


## Flags
**`--help, -h`**

Help for the cancel command.

**`--scan-id <string>` Required**

One or more comma separated scan IDs to cancel.

For example: `<scan-id>, <scan-id>, ...`


## Workflow Examples
### Retrieving all the scan ID’s statuses
<details>

<summary>Retrieve a list of scans and their statuses</summary>

```
user@laptop:/AST$ ./cx.exe scan list

Scan ID                              Project ID                           Status    Created at Tags Initiator                    Origin             
-------                              ----------                           ------    ---------- ---- ---------                    ------             
29a2b1e6-87c9-43b9-9d38-2d8165b390e1 df277b49-f1ef-4b5e-8cc4-0b66a2d1414a Running   08-27-21   []   user                         ASTCLI 2.0.0-rc.21
```

</details>

### Cancel a running scan
```
user@laptop:/AST$ ./cx.exe scan cancel --scan-id 29a2b1e6-87c9-43b9-9d38-2d8165b390e1
```

<details>

<summary>Retrieve a list of scans and their statuses (after the cancellation)</summary>

```
user@laptop:/AST$ ./cx.exe scan list

Scan ID                              Project ID                           Status    Created at Tags Initiator                    Origin             
-------                              ----------                           ------    ---------- ---- ---------                    ------                               
29a2b1e6-87c9-43b9-9d38-2d8165b390e1 df277b49-f1ef-4b5e-8cc4-0b66a2d1414a Canceled   08-27-21   []   user                          ASTCLI 2.0.0-rc.21
```

</details>

### Canceling several running scans
You can specify several comma separated scan ids in order to cancel multiple scans.

```
user@laptop:/AST$ ./cx.exe scan cancel --scan-id <scan_id1>,<scan_id2>
```

