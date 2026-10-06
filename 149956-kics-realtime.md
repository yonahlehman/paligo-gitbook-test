# kics-realtime

The `scan kics-realtime` command is used to **create and run a new IaC Security (KICS) scan** locally using a container. The SCA realtime scan is a free feature which does not require a Checkmarx account. Anyone can download the CLI tool and run this command without need for authentication. The results are returned in the response body as a JSON object.


{% hint style="warning" %}
Even for users with a Checkmarx account, the realtime scan results are not synced with the user's Checkmarx account.
{% endhint %}


## Usage
```
./cx scan kics-realtime [flags]
```


## Prerequisites
You must have a supported container engine (Docker or Podman) installed and running in your environment.


## Supported scan files extensions / technologies
The `scan kics-realtime` command provides the ability to scan individual files that are supported by the KICS tool (mentioned in the list below).

`kics-realtime` supports scanning multiple technologies, namely :

- Ansible
- Azure Resource Manager
- CDK
- CloudFormation
- Azure Blueprints
- Docker
- Docker Compose
- gRPC
- Helm
- Kubernetes
- OpenAPI
- Google Deployment Manager
- SAM
- Terraform

<details>

<summary>Supported File Extensions and File Names</summary>

*.yaml

*.tf

*.yml

*.json

*.auto.tfvars

*.terraform.tfvars

Dockerfile

*.proto

*.dockerfile

</details>

{% hint style="info" %}
For more details please check KICS official documentation [https://docs.kics.io/latest/platforms/](https://docs.kics.io/latest/platforms/)
{% endhint %}


## Additional Parameters
**--additional-params** flag provides the ability to send additional scan options supported by KICS. Should follow comma separated format.

{% hint style="info" %}
More information about the additional scan options/flags supported by KICS in their official documentation

[https://docs.kics.io/latest/commands/](https://docs.kics.io/latest/commands/)
{% endhint %}

{% hint style="warning" %}
The report format and output path cannot be overridden, even by explicitly setting those flags in the `additional-params`.
{% endhint %}


## Flags
**`--file <string>` Required**

Path to input file.

**`--engine <string>` Default: docker**

Name for the container engine to run KICS.

**`--additional-params <string>,<string>`**

Comma separated additional scan options supported by KICS. See [https://docs.kics.io/latest/commands/](https://docs.kics.io/latest/commands/)


## Examples
### Scanning a file
```
./cx scan kics-realtime --file <FILE PATH>
```

**Sample command**

```
C:\ast-cli_2.0.53_windows_x64>cx scan kics-realtime --file .\juice-shop-master\test\smoke\Dockerfile
```

<details>

<summary>Sample Response</summary>

```
{
  "kics_version": "v1.5.14",
  "total_counter": 5,
  "queries": [
    {
      "query_name": "Missing User Instruction",
      "query_id": "fd54f200-402c-4333-a5a4-36ef6709af2f",
      "severity": "HIGH",
      "platform": "Dockerfile",
      "category": "Build Process",
      "description": "A user should be specified in the dockerfile, otherwise the image will run as root",
      "query_url": "https://docs.docker.com/engine/reference/builder/#user",
      "files": [
        {
          "file_name": "../../path/Dockerfile",
          "similarity_id": "fe16c75adab39dd64ef3a270b71172d7901de1a59061ba753edc85357234278a",
          "line": 1,
          "issue_type": "MissingAttribute",
          "search_key": "FROM={{alpine}}",
          "search_line": 0,
          "search_value": "",
          "expected_value": "The 'Dockerfile' contains the 'USER' instruction",
          "actual_value": "The 'Dockerfile' does not contain any 'USER' instruction",
          "remediation": "",
          "remediation_type": ""
        }
      ]
    },
    {
      "query_name": "Image Version Not Explicit",
      "query_id": "9efb0b2d-89c9-41a3-91ca-dcc0aec911fd",
      "severity": "MEDIUM",
      "platform": "Dockerfile",
      "category": "Supply-Chain",
      "description": "Always tag the version of an image explicitly",
      "query_url": "https://docs.docker.com/engine/reference/builder/#from",
      "files": [
        {
          "file_name": "../../path/Dockerfile",
          "similarity_id": "2b13cdcc185b86e71995c052b3e5847e66e9d5db29eec74a500834fa5f87aa84",
          "line": 1,
          "issue_type": "MissingAttribute",
          "search_key": "FROM={{alpine}}",
          "search_line": 0,
          "search_value": "",
          "expected_value": "FROM alpine:'version'",
          "actual_value": "FROM alpine'",
          "remediation": "",
          "remediation_type": ""
        }
      ]
    },
    {
      "query_name": "Unpinned Package Version in Apk Add",
      "query_id": "d3499f6d-1651-41bb-a9a7-de925fea487b",
      "severity": "MEDIUM",
      "platform": "Dockerfile",
      "category": "Supply-Chain",
      "description": "Package version pinning reduces the range of versions that can be installed, reducing the chances of failure due to unanticipated changes",
      "query_url": "https://docs.docker.com/develop/develop-images/dockerfile_best-practices/",
      "files": [
        {
          "file_name": "../../path/Dockerfile",
          "similarity_id": "3ab664eadb801fca368324714512c482fc78571396f997dfd1848b758c2dffca",
          "line": 3,
          "issue_type": "IncorrectValue",
          "search_key": "FROM={{alpine}}.{{RUN apk add curl}}",
          "search_line": 0,
          "search_value": "",
          "expected_value": "RUN instruction with 'apk add <package>' should use package pinning form 'apk add <package>=<version>'",
          "actual_value": "RUN instruction apk add curl does not use package pinning form",
          "remediation": "",
          "remediation_type": ""
        }
      ]
    },
    {
      "query_name": "Healthcheck Instruction Missing",
      "query_id": "b03a748a-542d-44f4-bb86-9199ab4fd2d5",
      "severity": "LOW",
      "platform": "Dockerfile",
      "category": "Insecure Configurations",
      "description": "Ensure that HEALTHCHECK is being used. The HEALTHCHECK instruction tells Docker how to test a container to check that it is still working",
      "query_url": "https://docs.docker.com/engine/reference/builder/#healthcheck",
      "files": [
        {
          "file_name": "../../path/Dockerfile",
          "similarity_id": "f960191733e882417f359dec84ced77cb6b01d92c87d1137293e51facc245ef7",
          "line": 1,
          "issue_type": "MissingAttribute",
          "search_key": "FROM={{alpine}}",
          "search_line": 0,
          "search_value": "",
          "expected_value": "Dockerfile contains instruction 'HEALTHCHECK'",
          "actual_value": "Dockerfile doesn't contain instruction 'HEALTHCHECK'",
          "remediation": "",
          "remediation_type": ""
        }
      ]
    },
    {
      "query_name": "Apk Add Using Local Cache Path",
      "query_id": "ae9c56a6-3ed1-4ac0-9b54-31267f51151d",
      "severity": "INFO",
      "platform": "Dockerfile",
      "category": "Supply-Chain",
      "description": "When installing packages, use the '--no-cache' switch to avoid the need to use '--update' and remove '/var/cache/apk/*'",
      "query_url": "https://docs.docker.com/engine/reference/builder/#run",
      "files": [
        {
          "file_name": "../../path/Dockerfile",
          "similarity_id": "800985afc56b3f71ae48cdf8b2bce43b7920ec72f2c6c62bc02073b7b7997a8c",
          "line": 3,
          "issue_type": "IncorrectValue",
          "search_key": "FROM={{alpine}}.{{RUN apk add curl}}",
          "search_line": 0,
          "search_value": "",
          "expected_value": "'RUN' does not contain 'apk add' command without '--no-cache' switch",
          "actual_value": "'RUN' contains 'apk add' command without '--no-cache' switch",
          "remediation": "",
          "remediation_type": ""
        }
      ]
    }
  ],
  "severity_counters": {
    "HIGH": 1,
    "INFO": 1,
    "LOW": 1,
    "MEDIUM": 2
  }
}
```

</details>

### Scanning a file with a specific engine
```
./cx scan kics-realtime --file <FILE PATH> --engine <ENGINE NAME>
```

**Sample command**

```
C:\ast-cli_2.0.53_windows_x64>cx scan kics-realtime --file .\juice-shop-master\test\smoke\Dockerfile --engine podman
```

### Scanning a file with additional parameters
```
./cx scan kics-realtime --file <FILE PATH> --additional-params <KICS_COMMANDS>
```

**Sample command**

```
C:\ast-cli_2.0.53_windows_x64>cx scan kics-realtime --file .\juice-shop-master\test\smoke\Dockerfile --additional-params -v, --exclude-results,fec62a97d569662093dbb9739360942f
```

### Scanning a file in debug mode
```
./cx scan kics-realtime --file <FILE PATH> --debug
```

**Sample command**

```
C:\ast-cli_2.0.53_windows_x64>cx scan kics-realtime --file .\juice-shop-master\test\smoke\Dockerfile --debug
```

<details>

<summary>Sample response</summary>

```
2022/07/06 10:33:06 CLI Configuration:
2022/07/06 10:33:06               cx_client_secret: 
2022/07/06 10:33:06                      cx_apikey: 
2022/07/06 10:33:06                      cx_branch: 
2022/07/06 10:33:06                      cx_tenant: organization
2022/07/06 10:33:06                     http_proxy: 
2022/07/06 10:33:06                   cx_client_id: 
2022/07/06 10:33:06                     cx_timeout: 5
2022/07/06 10:33:06                    cx_base_uri: 
2022/07/06 10:33:06               cx_base_auth_uri: 
2022/07/06 10:33:06             cx_proxy_auth_type: basic
2022/07/06 10:33:06 Starting kics container
2022/07/06 10:33:06 The report format and output path cannot be overridden.
2022/07/06 10:33:08 
                   .0MO.                                    
                   OMMMx                                    
                   ;NMX;                                    
                    ...           ...              ....     
WMMMd     cWMMM0.  KMMMO      ;xKWMMMMNOc.     ,xXMMMMMWXkc.
WMMMd   .0MMMN:    KMMMO    :XMMMMMMMMMMMWl   xMMMMMWMMMMMMl
WMMMd  lWMMMO.     KMMMO   xMMMMKc...'lXMk   ,MMMMx   .;dXx 
WMMMd.0MMMX;       KMMMO  cMMMMd        '    'MMMMNl'       
WMMMNWMMMMl        KMMMO  0MMMN               oMMMMMMMXkl.  
WMMMMMMMMMMo       KMMMO  0MMMX                .ckKWMMMMMM0.
WMMMMWokMMMMk      KMMMO  oMMMMc              .     .:OMMMM0
WMMMK.  dMMMM0.    KMMMO   KMMMMx'    ,kNc   :WOc.    .NMMMX
WMMMd    cWMMMX.   KMMMO    kMMMMMWXNMMMMMd .WMMMMWKO0NMMMMl
WMMMd     ,NMMMN,  KMMMO     'xNMMMMMMMNx,   .l0WMMMMMMMWk, 
xkkk:      ,kkkkx  okkkl        ;xKXKx;          ;dOKKkc    


Scanning with Keeping Infrastructure as Code Secure v1.5.6


Preparing Scan Assets: DoneExecuting queries: [-------------------------------------------->___________________________] 62.03%Executing queries: [------------------------------------------------------------->__________] 84.81%Executing queries: [-----------------------------------------------------------------------] 100.00%
Files scanned: 1
Parsed files: 1
Queries loaded: 48
Queries failed to execute: 0

------------------------------------

Healthcheck Instruction Missing, Severity: LOW, Results: 1
Description: Ensure that HEALTHCHECK is being used. The HEALTHCHECK instruction tells Docker how to test a container to check that it is still working
Platform: Dockerfile

        [1]: ../../path/d.dockerfile:1

                001: FROM openjdk:11.0.1-jre-slim-stretch
                002: 


Missing User Instruction, Severity: HIGH, Results: 1
Description: A user should be specified in the dockerfile, otherwise the image will run as root
Platform: Dockerfile

        [1]: ../../path/d.dockerfile:1

                001: FROM openjdk:11.0.1-jre-slim-stretch
                002: 


Results Summary:
HIGH: 1
MEDIUM: 0
LOW: 1
INFO: 0
TOTAL: 2

Results saved to file /path/results.json
Scan duration: 975.245001ms
A new version 'v1.5.11' of KICS is available, please consider updating
Generating Reports: Done
{"kics_version":"v1.5.6","total_counter":2,"queries":[{"query_name":"Missing User Instruction","query_id":"fd54f200-402c-4333-a5a4-36ef6709af2f","severity":"HIGH","platform":"Dockerfile","category":"Build Process","description":"A user should be specified in the dockerfile, otherwise the image will run as root","query_url":"https://docs.docker.com/engine/reference/builder/#user","files":[{"file_name":"../../path/d.dockerfile","similarity_id":"07841372d54f621706540de0f41d702dc8598f681a44bc19f55feb4cdce61e76","line":1,"issue_type":"MissingAttribute","search_key":"FROM={{openjdk:11.0.1-jre-slim-stretch}}","search_line":0,"search_value":"","expected_value":"The 'Dockerfile' contains the 'USER' instruction","actual_value":"The 'Dockerfile' does not contain any 'USER' instruction"}]},{"query_name":"Healthcheck Instruction Missing","query_id":"b03a748a-542d-44f4-bb86-9199ab4fd2d5","severity":"LOW","platform":"Dockerfile","category":"Insecure Configurations","description":"Ensure that HEALTHCHECK is being used. The HEALTHCHECK instruction tells Docker how to test a container to check that it is still working","query_url":"https://docs.docker.com/engine/reference/builder/#healthcheck","files":[{"file_name":"../../path/d.dockerfile","similarity_id":"5c3e1823b979a8cb04a5293f368fa8134175da78011f4d144c19f45177aa65e9","line":1,"issue_type":"MissingAttribute","search_key":"FROM={{openjdk:11.0.1-jre-slim-stretch}}","search_line":0,"search_value":"","expected_value":"Dockerfile contains instruction 'HEALTHCHECK'","actual_value":"Dockerfile doesn't contain instruction 'HEALTHCHECK'"}]}],"severity_counters":{"HIGH":1,"INFO":0,"LOW":1,"MEDIUM":0}}
2022/07/06 10:33:08 Removing folder in temp
```

</details>

