# gitlab

The `gitlab` command retrieves the number of unique contributors for the provided GitLab groups or projects.


{% hint style="info" %}
This command returns a breakdown of unique contributors per repo as well as the total number of unique contributors. When a particular user contributes to several different repos, this is counted as a single contributor for the total count. Therefore, the total count will not necessarily be equal to the sum of the individual repos.
{% endhint %}


## Usage
```
.\cx.exe utils contributor-count gitlab [flags]
```


## Flags
**`--format <string>` Default: table**

The output format for the response. Possible values are `json`, `list` or `table`.

**`--help, -h`**

Help for the github command.

**`--token <string>`**

GitLab OAuth token with at least '**read_api**' and '**read_repository**' permissions.

**`--groups <strings>`**

List of group names to scan for contributors.

Comma separated list for more than one names.

If a subgroup is being used, the full path of subgroup is required. Full path includes the names of the parent groups and can be copied from the gitlab urls when the group is opened in the browser.

**`--projects <strings>`**

List of project names to scan for contributors.

Project names should be full path/namespace.

Comma separated list for using more than one project names.

**`--url-gitlab <string>` Default: [https://gitlab.com](https://gitlab.com)**

API base URL.


## Examples
## Using the gitlab Command to Count an Organization
```
C:\Users\ast-cli> .\cx.exe utils contributor-count gitlab --token <token> --groups Checkmarx-ts/cxlite

Name                               UniqueContributors 
----                               ------------------ 
...
Checkmarx/CxLite/CxDemo            1                  
...      
Total unique contributors          1
```

## Using the gitlab Command to Count Specific Repositories
```
C:\Users\ast-cli>.\cx.exe utils contributor-count gitlab --token <token> --projects Checkmarx/CxLite/CxDemo

Name                               UniqueContributors 
----                               ------------------ 
Checkmarx/CxLite/CxDemo            1                           
Total unique contributors          1
```

