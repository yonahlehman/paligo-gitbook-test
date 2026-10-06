# triage show

The **triage show** command is used to retrieve a list of all changes made to the predicate of a specific risk instance.


## Usage
```
./cx triage show [flags]
```


## Flags
**`--project-id <string>` Required**

The project ID of the project for which you want to see the changes.

**`--scan-type <string>` Required**

The type of scanner that identified the risk. Options are: sast, sca, scs or iac-security.

**`--similarity-id <string>` Required**

The unique identifier of the specific risk instance.

**`--format <string>` Default: list**

The output format for the response. Possible values are `json`, `list` or `table`.

**`--help`**

Help for the triage show command.


## Examples
Sample command:

```
./cx triage show --scan-type <scan-type> --project-id <project-id> --similarity-id <similarity-id>
```

Sample response:

```
user@laptop:~/ast-cli$ ./cx.exe triage show --scan-type "sast" --project-id "885ca4ad-5926-4177-b51c-fa1d11248d84" --similarity-id "549106280"
Fetching the predicate history for SimilarityId : 549106280

ID            : d10e7acd-d59a-4cbf-afd1-146e0253f23e
Project ID    : 885ca4ad-5926-4177-b51c-fa1d11248d84
Similarity ID : 549106280
Severity      : LOW
State         : CONFIRMED
Comment       : Can wait till Q3
CreatedBy     : service-account-user_client
Created at    : 01-03-22

ID            : 5147c12a-9021-4c25-97c7-b0cc27a6a449
Project ID    : 885ca4ad-5926-4177-b51c-fa1d11248d84
Similarity ID : 549106280
Severity      : MEDIUM
State         : TO_VERIFY
Comment       : assigned to appsec team A
CreatedBy     : user
Created at    : 01-03-22

ID            : f590fdb8-1a1a-492f-ab3d-8e3693e59359
Project ID    : 885ca4ad-5926-4177-b51c-fa1d11248d84
Similarity ID : 549106280
Severity      : HIGH
State         : TO_VERIFY
Comment       :
CreatedBy     : user
Created at    : 01-03-22
```

