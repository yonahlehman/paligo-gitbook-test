# bitbucket-server

The `bitbucket-server` command retrieves the number of unique contributors for the provided Bitbucket Server repositories and projects.


{% hint style="info" %}
This command returns a breakdown of unique contributors per repo as well as the total number of unique contributors. When a particular user contributes to several different repos, this is counted as a single contributor for the total count. Therefore, the total count will not necessarily be equal to the sum of the individual repos.
{% endhint %}


## Usage
```
./cx utils contributor-count bitbucket-server [flags]
```


## Flags
**`--help, -h`**

Help for the `bitbucket-server` command.

**`--projects <string>` Default: all**

{% hint style="success" %}
Not required. However, when you submit `--repos`, it is required to also submit `--projects`.
{% endhint %}

List of projects to scan for contributors.

A comma separated list.

**`--repos <string>` Default: all**

List of repositories to scan for contributors.

A comma separated list.

**`--token <string>` Default: if no token is provided, then only public projects are searched**

The **HTTP access token** that you generated in Bitbucket. To learn how to genearte a token, see the section "Create HTTP access tokens" [here](https://confluence.atlassian.com/bitbucketserver/http-access-tokens-939515499.html).

{% hint style="success" %}
On older versions of Bitbucket Server this is referred to as a "Personal access token".
{% endhint %}

For **Permissions** select, at a minimum:

- **Project read**, and
- **Repository read**.

**`--server-url <string>` Required**

The URL of your Bitbucket Server instance.

**`--format <string>` Default: table**

The output format for the response. Possible values are `json`, `list` or `table`.


## Examples
## Using the bitbucket-server Command to Count All Contributors
```
./cx utils contributor-count bitbucket-server --server-url <server-url> --token <token>
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count bitbucket-server --server-url bitbucket.my.com --token MYTOKEN

Name                                      UniqueContributors 
----                                      ------------------ 
CX/ast-cli                                2
...
AS/my-project                             1                    
...                                       ...
Total unique contributors                 7     

2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

**With Debug**

```
./cx utils contributor-count bitbucket-server --server-url <server-url> --token <token> --debug
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count bitbucket-server --server-url bitbucket.my.com --token MYTOKEN --debug

Name                                      UniqueContributors 
----                                      ------------------ 
CX/ast-cli                                2
...
AS/my-project                             1
...                                       ...
Total unique contributors                 7       

Name                                      UniqueContributorsUsername 
----                                      -------------------------- 
CX/ast-cli                                user - user.name@checkmarx.com
...
AS/my-project                             user2 - user2.name@checkmarx.com
...

2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

## Using the bitbucket-server Command to Count Projects' Contributors
```
./cx utils contributor-count bitbucket-server --projects <projects> --server-url <server-url> --token <token>
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count bitbucket-server --projects CX --server-url bitbucket.my.com --token MYTOKEN

Name                                      UniqueContributors 
----                                      ------------------ 
CX/ast-cli                                2
CX/ast-java-wrapper                       1                    
...                                       ...
Total unique contributors                 7     

2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

**With Debug**

```
./cx utils contributor-count bitbucket-server --projects <projects> --server-url <server-url> --token <token> --debug
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count bitbucket-server --projects CX --server-url bitbucket.my.com --token MYTOKEN --debug

Name                                      UniqueContributors 
----                                      ------------------ 
CX/ast-cli                                2
CX/ast-java-wrapper                       1
...                                       ...
Total unique contributors                 7       

Name                                      UniqueContributorsUsername 
----                                      -------------------------- 
CX/ast-cli                                user - user.name@checkmarx.com
CX/ast-java-wrapper                       user2 - user2.name@checkmarx.com
...

2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

## Using the bitbucket-server Command to Count Repositories' Contributors
```
./cx utils contributor-count bitbucket-server --projects <projects> --repos <repos> --server-url <server-url> --token <token>
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count bitbucket-server --projects CX --repos ast-cli --server-url bitbucket.my.com --token MYTOKEN

Name                                      UniqueContributors 
----                                      ------------------ 
CX/ast-cli                                2                  
Total unique contributors                 2     

2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

**With Debug**

```
./cx utils contributor-count bitbucket-server --projects <projects> --repos <repos> --server-url <server-url> --token <token> --debug
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count bitbucket-server --projects CX --repos ast-cli --server-url bitbucket.my.com --token MYTOKEN --debug

Name                                      UniqueContributors 
----                                      ------------------ 
CX/ast-cli                                2
Total unique contributors                 2        


Name                                      UniqueContributorsUsername 
----                                      -------------------------- 
CX/ast-cli                                user - user.name@checkmarx.com 


2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

