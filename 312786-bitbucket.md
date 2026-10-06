# bitbucket

The pr bitbucket command decorates pull requests in Bitbucket with results from Checkmarx One scans that were triggered by that pull request. The command must be submitted with a series of required attributes that specify the relevant repo and PR and provide the authentication credentials.


## Usage
**Managed Setup**

```
./cx utils pr bitbucket --scan-id <scan-id> --token <PAT> --namespace <username> --repo-name <repository-slug> --pr-id <pr number>
```

**Custom Setup**

```
./cx utils pr bitbucket --scan-id <scan-id> --token <PAT> --code-repository-url <bitbucket-server-url> --project-key <project-key> --repo-name <repository-slug> --pr-id <pr number>
```


## Flags
**`--code-repository-url` Required only for custom setup**

The URL of the custom setup instance.

**`--namespace` Required only for managed setup**

Bitbucket namespace for the organization.

**`--pr-id` Required**

The pull request ID for decoration PR.

**`--project-key` Required only for custom setup**

The key of the Bitbucket project containing the repository.

**`--repo-name` Required**

Bitbucket repository name.

**`--scan-id` Required**

The scan ID of the Checkmarx One scan that was triggered by this PR. This can be extracted from the scan result that is obtained after the pull request is scanned.

**`--token` Required**

Your Bitbucket personal access token (PAT).


## Examples
## pr bitbucket command
```
/cx.exe utils pr bitbucket --scan-id 00f383f6-c618-4973-a576-938a64cee4b5 --token TOKEN --namespace elchananaarbiv --repo-name decoration1 --pr-id 20 --token TOKEN
```

