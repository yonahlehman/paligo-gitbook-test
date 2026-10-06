# scan list

The `scan list` command provides a **list of all the scans** in your Checkmarx One account.


## Usage
```
./cx scan list [flags]
```


## Flags
**`--filter <string>`**

Filter the results returned by this command.

All filters, sorting and pagination options that are available for the **GET /scans** REST API can also be sent with this flag. See our [API documentation](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/1wnhzwk5inwup-retrieve-list-of-scans) for more details.

- Use "**;**" to separate between multiple values for a particular filter.
- Use "," to separate between multiple filters.
- Supported filters (including pagination and sorting): `limit`, `offset`, `branch`, `branches`, `from-date`, `to-date`, `groups`, `initiators`, `project-id`, `project-ids`, `project-names`, `scan-ids`, `search`, `source-origins`, `source-types`, `statuses`, `tags-keys`, `tags-values`, `sort`.

**`--fromat <string>` Default: table**

The output format for the response. Possible values are `json`, `list` or `table`.

**`---help, -h`**

Help for the list command.


## Pagination
This command uses pagination. By default it returns the first 20 results (i.e., `limit=20,offset=0`). Use `limit` to adjust the maximum number of results to return and `offset` to specify the number of results to skip before starting to return results. You can use `offset=0` and `limit=0` to get all results.

**Example:** The following command returns records 21-30

```
./cx scan list --filter "limit=10,offset=20"
```


## Applying Filters
You can limit results by filtering by various scan attributes such as scan IDs, project ID, scan tags, scan status and date range.

Filters are applied using the following syntax:

```
./cx scan list --filter "attributeA=value1,attributeB=value1;value2;value3,..."
```

**Example:** The following command returns records for all scans run on specific projects, based on project ID.

```
./cx scan list --filter "project-id=f761f24b-fbcc-4502-acef-7fa3f2de38ed"
```

When multiple filter attributes are used, an AND operator is applied between attributes. When multiple values are given for an attribute, an OR operator is used between values.

**Example:** The following command returns records for all scans with the tag key "product" and a tag value of either "AppA", "AppB" or "AppC" that were run since Jan 1, 2023.

```
./cx scan list --filter "tags-keys=product,tags-values=AppA;AppB;AppC,from-date=2023-01-01T00:00:00Z,limit=0"
```


## Examples
### Using the scan list command with format flags
```
user@laptop:/AST$ ./cx scan list --format table

Scan ID                              Project ID                           Status    Created at Tags Initiator Origin             
-------                              ----------                           ------    ---------- ---- --------- ------             
a2f45c91-18ba-4d69-a748-972d0ecc1453 9f47d3d7-76f2-418b-9513-e3e02cc5cbb9 Completed 08-27-21   []   org_admin ASTCLI 2.0.0-rc.21
```

```
user@laptop:/AST$ ./cx scan list --format list

Scan ID    : a2f45c91-18ba-4d69-a748-972d0ecc1453
Project ID : 9f47d3d7-76f2-418b-9513-e3e02cc5cbb9
Status     : Completed
Created at : 08-27-21
Tags       : []
Initiator  : org_admin
Origin     : ASTCLI 2.0.0-rc.21
```

