# project create

The `project create` command enables the ability to **create a new project** in Checkmarx One.


## Usage
```
./cx project create [flags]
```


## Flags
**`--application-name <string>`**

Specify an application to which this project will be assigned.

Note: This flag can only be used to assign a project to an application that already exists, not to create a new application.

**`--branch <string>`**

The name of the branch.

The branch specified in this flag is set as the PRIMARY branch for the project.

**`--format <string>` Default: table**

The output format for the response. Possible values are `json`, `list` or `table`.

**`--tags <string>`**

List of tags. For example: tagA, tagB:value

**`--groups`**

List of groups.

**`--help`**

Help for the create command.

**`--project-name <string>`**

Name of the project.

**`--repo-url <string>`**

Project Repository URL.

**`--ssh-key <string>`**

Path to ssh private key.


## Workflow Examples
### Create a New Project
```
./cx project create --project-name <Project Name>
```

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project create --project-name "Test1"

Project ID                           Name  Created at Tags Groups 
----------                           ----  ---------- ---- ------ 
ce46df28-7f33-49fe-88cb-337fe8eb2c39 Test1 09-29-21   []   []
```

<details>

<summary>Verify that the Project Exists in the Projects List</summary>

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project list

Project ID                           Name                                   Created at Tags    Groups                                 
----------                           ----                                   ---------- ----    ------                                 
ce46df28-7f33-49fe-88cb-337fe8eb2c39 Test1                                  09-29-21   []      []                                     
d7b56888-8407-4e9b-ae5b-7fc43233a497 Test111                                08-25-21   []      []                                     
d6fe8ab4-becd-49ff-987f-ec5ee02cc614 EffProj                                09-22-21   []      []
```

</details>

