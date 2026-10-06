# project list

The `project list` command provides a **list of all the projects** in Checkmarx One.


## Usage
```
./cx project list [flags]
```


## Flags
**`--filter <string>`**

Filter the list of projects returned.

All filter and pagination options that are available for the **GET /projects** REST API can also be sent with this flag. See our [API documentation](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/j4vd1fubv8m4z-retrieve-list-of-projects) for more details.

{% hint style="success" %}
By default, the first 20 records are returned. You can set the `limit` value as 0 in order to return all records.
{% endhint %}

- Use "**;**" to separate between multiple values for a particular filter.
- Use "," to separate between multiple filters.
- Supported filters (including pagination): `limit`, `offset`, `groups`, `ids`, `name`, `name-regex`, `names`, `repo-url`, `tags-keys`, and `tags-values`.
   
   {% hint style="info" %}
   You can filter for projects with no tags by specifying `NONE` for both `tags-keys` and `tags-values`, i.e., `--filter tags-keys=NONE,tags-values=NONE`.
   {% endhint %}

**`--format <string>` Default: table**

The output format for the response.

Possible values are `json`, `list` or `table`.

**`--help, -h`**

Help for the list command.


## Pagination
This command uses pagination. By default it returns the first 20 results (i.e., `limit=20,offset=0`). Use `limit` to adjust the maximum number of results to return and `offset` to specify the number of results to skip before starting to return results. You can use `offset=0` and `limit=0` to get all results.

**Example:** The following command returns records 21-30

```
./cx project list --filter "limit=10,offset=20"
```


## Applying Filters
You can limit results by using pagination and/or by filtering by various project attributes such as project IDs and project tags.

Filters are applied using the following syntax:

```
./cx project list --filter "attributeA=value1,attributeB=value1;value2;value3,..."
```

**Example:** The following command returns records for specific projects, based on project IDs.

```
./cx project list --filter "ids=7b70e4b6-4288-467b-8fa2-9c6c0ad0bd08;e231cf6d-f031-4290-b014-7c6ec343f793"
```

When multiple filter attributes are used, an AND operator is applied between attributes. When multiple values are given for an attribute, an OR operator is used between values.

**Example:** The following command returns records for all projects that have the tag key "product" and a tag value of either "AppA", "AppB" or "AppC".

```
./cx project list --filter "tags-keys=product,tags-values=AppA;AppB;AppC,limit=0"
```


## Results
For each project, the following items are returned: Project ID, Project Name, Date that the project was created, and Tags and Groups associated with the project.

When results are returned in json format, an additional item `updatedAt` is returned, giving the date of the most recent edit of the project settings.

{% hint style="info" %}
The date given for `updatedAt` relates only to editing the project settings and not to running scans, generating reports or other activities on the project.
{% endhint %}


## Examples
**Using the `project list` command with various `--format` flags**

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project list --format table

Project ID                           Name                                   Created at Tags    Groups                                 
----------                           ----                                   ---------- ----    ------                                 
ce46df28-7f33-49fe-88cb-337fe8eb2c39 Test1                                  09-29-21   []      []                                     
d7b56888-8407-4e9b-ae5b-7fc43233a497 Test111                                08-25-21   []      []                                     
d6fe8ab4-becd-49ff-987f-ec5ee02cc614 EffProj                                09-22-21   []      []
```

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project list --format list

Project ID : ce46df28-7f33-49fe-88cb-337fe8eb2c39
Name       : Test1
Created at : 09-29-21
Tags       : []
Groups     : []

Project ID : d7b56888-8407-4e9b-ae5b-7fc43233a497
Name       : Test111
Created at : 08-25-21
Tags       : []
Groups     : []

Project ID : d6fe8ab4-becd-49ff-987f-ec5ee02cc614
Name       : EffProj
Created at : 09-22-21
Tags       : []
Groups     : []
```

