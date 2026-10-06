# scan delete

The `delete` command is used to **delete one or more scans** in Checkmarx One.


## Usage
```
./cx scan delete --scan-id <scan ID>
```


## Flags
**`--help, -h`**

Help for the delete command.

**`--scan-id` Required**

One or more comma separated scan IDs to delete.

For example: `<scan-id>,<scan-id>,...`


## Workflow Examples
<details>

<summary>Retrieve a list of scans</summary>

```
user@laptop:/AST$ ./cx scan list

Scan ID                              Project ID                           Status    Created at Tags Initiator Origin             
-------                              ----------                           ------    ---------- ---- --------- ------             
7eb83ed3-5734-4428-92a2-4819fc6c490f 9f47d3d7-76f2-418b-9513-e3e02cc5cbb9 Completed 08-27-21   []   org_admin ASTCLI 2.0.0-rc.21
```

</details>

### Delete a scan
```
user@laptop:/AST$ ./cx scan delete --scan-id 7eb83ed3-5734-4428-92a2-4819fc6c490f
```

<details>

<summary>Verify that the scan isn't shown in the scan list</summary>

```
user@laptop:/AST$ ./cx scan list

Scan ID                              Project ID                           Status    Created at Tags Initiator Origin             
-------                              ----------                           ------    ---------- ---- --------- ------
```

</details>

### Delete several scans
You can specify several comma separated scan ids in order to delete multiple scans.

```
./cx scan delete --scan-id 7eb83ed3-5734-4428-92a2-4819fc6c490f,a2f45c91-18ba-4d69-a748-972d0ecc1453
```

