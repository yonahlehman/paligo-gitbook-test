# project delete

The `project delete` is used to **delete a project** in Checkmarx One.


## Usage
```
./cx project delete --project-id <project-id> [flags]
```


## Flags
**`--help, -h`**

Help for the delete command.

**`--project-id`**

Project ID to delete.


## Workflow Example
<details>

<summary>Retrieve the Checkmarx One Projects List</summary>

```
user@laptop:/AST$ ./cx.exe project list

Project ID                           Name                         Created at Tags Groups 
----------                           ----                         ---------- ---- ------ 
fa5eeaac-2ec7-4fa7-946e-ed2f2e5ff8cd test-proj-del                08-24-21   []   []
```

</details>

### Delete a Project
```
user@laptop:/AST$ ./cx.exe project delete --project-id fa5eeaac-2ec7-4fa7-946e-ed2f2e5ff8cd
```

<details>

<summary>Verify that the project doesn’t exist in the projects list</summary>

```
user@laptop:/AST$ ./cx.exe project list

Project ID                           Name                         Created at Tags Groups 
----------                           ----                         ---------- ---- ------
```

</details>

