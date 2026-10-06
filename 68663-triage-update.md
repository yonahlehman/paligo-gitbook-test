# triage update

The **triage update** command is used to **triage the results** in Checkmarx One.


## Usage
```
./cx triage update [flags]
```


## Flags
**`--comment <string>`**

Optional comment.

{% hint style="success" %}
Depending on your account configuration, adding a comment may be mandatory when making certain state changes.
{% endhint %}

**`--project-id <string>` Required**

The project ID of the project for which this profile change will take effect.

**`--scan-type <string>` Required**

The type of scanner that identified the risk. Options are: sast or iac-security.

**`--severity <string>` Required**

Specify the severity of the vulnerability. Options are: critical, high, medium, low or info.

**`--similarity-id <string>` Required**

The unique identifier of a specific instance of a vulnerability.

**`--state <string>` Required**

Specify the current state of this vulnerability. Options are: to_verify, not_exploitable, proposed_not_exploitable, confirmed or urgent.

{% hint style="info" %}
The states mentioned above are pre-configured for all Checkmarx One accounts. In addition, you can create custom states in your account. Once they are created, you can assign those custom states to results.

Custom states is currently supported for SAST, SCA, IaC Security and Container Security results. It is not yet available for all tenant accounts. For more info, see [Custom States](https://docs.checkmarx.com/en/34965-378909-custom-states.html).
{% endhint %}

**`--help`**

Help for the update command.


## Examples
### Update result
```
./cx triage update --scan-type <scan-type> --project-id <project-id> --similarity-id <similarity-id> --state <state> --severity <severity>
```

```
user@laptop:~/ast-cli$ ./cx triage update --scan-type "sast" --project-id "885ca4ad-5926-4177-b51c-fa1d11248d84" --similarity-id "549106280"  --state "confirmed" --severity "low"
Predicate updated successfully.
```

