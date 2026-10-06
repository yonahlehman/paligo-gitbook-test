# bitbucket

The `bitbucket` command retrieves the number of unique contributors for the provided Bitbucket repositories, projects and organizations.


{% hint style="info" %}
This command returns a breakdown of unique contributors per repo as well as the total number of unique contributors. When a particular user contributes to several different repos, this is counted as a single contributor for the total count. Therefore, the total count will not necessarily be equal to the sum of the individual repos.
{% endhint %}


## Usage
```
./cx utils contributor-count bitbucket [flags]
```


## Flags
**`--help, -h`**

Help for the Bitbucket command.

**`--workspaces <string>`**

List of workspaces to scan for contributors.

A Comma separated list.

**`--repos <string>`**

List of repositories to scan for contributors.

A Comma separated list.

**`--username <string>`**

Username for Bitbucket authentication.

**`--password <string>`**

App password for Bitbucket authentication. Requires read on "Workspace membership" and "Repositories" permissions.

**`--url-bitbucket <string>` Default: [https://api.bitbucket.org/2.0/](https://api.bitbucket.org/2.0/)**

API base URL.

**`--format <string>` Default: table**

The output format for the response. Possible values are `json`, `list` or `table`.


## Examples
## Using the bitbucket Command to Count Workspace Contributors
```
./cx utils contributor-count bitbucket --workspaces <workspaces> --username <username> --password <password> --debug
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count bitbucket --workspaces Checkmarx --username cx --password 12345678910

Name                                      UniqueContributors 
----                                      ------------------ 
Checkmarx/ast-cli                         2
Checkmarx/ast-java-wrapper                1                    
...                                       ...
Total unique contributors                 7       

Name                                      UniqueContributorsUsername 
----                                      -------------------------- 
Checkmarx/ast-cli                         User Checkmarx
Checkmarx/ast-java-wrapper                UserCheckmarx                
...

2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

## Using the bitbucket Command to Count Repositories Contributors
```
./cx utils contributor-count bitbucket --workspaces <workspaces> --repos <repos> --username <username> --password <password> --debug
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count bitbucket --orgs Checkmarx --repos ast-cli --username cx --password 12345678910

Name                                      UniqueContributors 
----                                      ------------------ 
Checkmarx/ast-cli                         2                  
Total unique contributors                 2        


Name                                      UniqueContributorsUsername 
----                                      -------------------------- 
Checkmarx/ast-cli                         User Checkmarx          


2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

