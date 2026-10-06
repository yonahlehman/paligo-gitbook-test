# project show

The `project show` command **provides information about a project** in Checkmarx One.


## Usage
```
./cx project show --project-id <project-id> [flags]
```


## Flags
**`--project-id <string>` Required**

Project ID to show.

**`--format <string>` Default: table**

The output format for the response. Possible values are `json`, `list` or `table`.

**`---help, -h`**

Help for the show command.


## Results
For each project, the following items are returned: Project ID, Project Name, Date that the project was created, and Tags and Groups associated with the project.

If the project configuration has been edited after the initial creation, then an additional item `updatedAt` is returned, giving the date of the most recent edit.

{% hint style="info" %}
The date given for `updatedAt` relates only to project configuration and not to running of scans, generating reports or other activities.
{% endhint %}


## Workflow Examples
<details>

<summary>Retrieve Project IDs</summary>

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project list --format table

Project ID                           Name                                   Created at Tags    Groups                                 
----------                           ----                                   ---------- ----    ------                                 
ce46df28-7f33-49fe-88cb-337fe8eb2c39 Test1                                  09-29-21   []      []                                     
d7b56888-8407-4e9b-ae5b-7fc43233a497 Test111                                08-25-21   []      []                                     
d6fe8ab4-becd-49ff-987f-ec5ee02cc614 EffProj                                09-22-21   []      []
```

</details>

### Use the project show command with various format flags
```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project show --project-id ce46df28-7f33-49fe-88cb-337fe8eb2c39 --format table

Project ID                           Name  Created at Tags Groups 
----------                           ----  ---------- ---- ------ 
ce46df28-7f33-49fe-88cb-337fe8eb2c39 Test1 09-29-21   []   []
```

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project show --project-id ce46df28-7f33-49fe-88cb-337fe8eb2c39 --format list

Project ID : ce46df28-7f33-49fe-88cb-337fe8eb2c39
Name       : Test1
Created at : 09-29-21
Tags       : []
Groups     : []
```

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project show --project-id ce46df28-7f33-49fe-88cb-337fe8eb2c39 --format json
{"ID":"ce46df28-7f33-49fe-88cb-337fe8eb2c39","Name":"Test1","CreatedAt":"2021-09-29T11:52:15.924297Z","UpdatedAt":"2021-09-29T11:52:15.924297Z","Tags":{},"Groups":[]}
```

