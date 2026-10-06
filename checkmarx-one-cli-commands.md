# Checkmarx One CLI Commands

This section includes all the Checkmarx CLI commands.

## Global Flags

The CLI tool supports a set of global flags.


The Global flags are optional for every CLI command/Sub-command.


The following list includes all the global flags that can be added to the CLI commands.


**`--agent <string>` Default - "ASTCLI"**

Scan origin name.

**`--apikey <string>`**

The API Key to login to Checkmarx One with.

**`--base-auth-uri <string>`**

The Checkmarx One User Management URI.

**`--base-uri <string>`**

The Checkmarx One server URI.

**`--client-id <string>`**

The OAuth client ID.

**`--client-secret <string>`**

The OAuth client secret.

**`--config-file-path`**

Specify the path to the config file to be used for the current command.

{% hint style="info" %}
By default the config file is stored at ($HOME/.checkmarx).

An alternative location can be specified using the environment variable CX_CONFIG_FILE_PATH. This flag overrides the default and the environment variable.
{% endhint %}

{% hint style="warning" %}
When you submit your credentials using the `configure` command, the config file automatically created at the default location. If you want to use this flag, you need to first manually add the config file at the specified location.
{% endhint %}

**`--debug`**

Debug mode with detailed logs.

**`--help, -h`**

Help for every cx command/sub-command

**`--ignore-proxy`**

Ignore the proxy that is configured in your system, so that all Checkmarx One CLI commands are run from your local machine.

Note: Alternatively, this can be done setting the environment variable CX_IGNORE_PROXY as true.

**`--insecure`**

Ignore TLS certificate validations.

**`--log-file <string>`**

Saves logs to the specified file path only (not to the console).

**`--log-file-console <string>`**

Saves logs to the specified file path as well as to the console.

**`--optional-flags <string>`**

A global parameter that allows you to pass command-specific flags indirectly by supplying them as key-value pairs. This option is useful in environments where direct command flags cannot be provided, such as IDE integrations or CI/CD plugins.

**Example 1:** `scan create --optional-flags="asca-location=/home/custom/path"` can be used to run the ASCA scanner from a custom installation location.

**Example 2:** `scan create --optional-flags="use-gitignore=true"` passes the`--use-gitignore` flag to the `scan create` command, excluding files and directories based on patterns defined in the directory's `.gitignore` file.

**Example 3:** `scan create --optional-flags="exclude-git-folder=true"` passes the `--exclude-git-folder` flag to the `scan create` command, exluding the `.git` folder from the scan source upload ZIP.

**`--proxy <string>`**

Proxy server to send communication through.

{% hint style="info" %}
You need to include the `http://` prefix. The format should be `http://<proxy_ip>:<port_number>`. If authentication is required, then the format should be `http://<username>:<password>@<proxy_ip>:<port_number>`.
{% endhint %}

**`--proxy-auth-type <string>`**

Proxy authentication type, (basic, ntlm, kerberos, or kerberos-native). `kerberos` for [MIT kereberos](https://web.mit.edu/kerberos/dist/) and `kerberos-native` for [SSPI](https://learn.microsoft.com/en-us/windows-server/security/windows-authentication/security-support-provider-interface-architecture).

{% hint style="info" %}
Required when using the `--proxy` flag.
{% endhint %}

**`--proxy-kerberos-ccache <string>` Default - KRB5CCNAME env or OS default**

Path to Kerberos credential cache.

{% hint style="info" %}
This optional flag is relevant only when `--proxy-auth-type` is set as `kerberos`, i.e., for MIT Kerberos authentication.
{% endhint %}

**`--proxy-kerberos-krb5-conf <string>` Default - Linux - /etc/krb5.conf, Windows - C:\Windows\krb5.ini on windows**

Path to Kerberos configuration file.

{% hint style="info" %}
This optional flag is relevant only when `--proxy-auth-type` is set as `kerberos`, i.e., for MIT Kerberos authentication.
{% endhint %}

**`--proxy-kerberos-spn <string>`**

Service Principal Name (SPN) for Kerberos proxy authentication.

{% hint style="info" %}
Required when `--proxy-auth-type` is set as `kerberos` or `kerberos-native`.
{% endhint %}

**`--proxy-ntlm-domain <string>`**

Window domain when using NTLM proxy.

**`--retry <unit>` Default - 3 times**

Retry requests to Checkmarx One on connection failure.

**`--retry-delay <unit>` Default - 3 seconds**

Time between retries in seconds, use with `--retry`.

**`--tenant <string>` Default - "organization"**

The tenant name of the Checkmarx One Server.

**`--timeout <string>` Default - 5 seconds**

Timeout for network activity.


### Example

```
C:\Users\elip.DM\Downloads\ast-cli_windows_x64>cx.exe --help
The Checkmarx One CLI is a fully functional Command Line Interface (CLI) that interacts with the Checkmarx One server.

USAGE
  cx <command> <subcommand> [flags]

COMMANDS
  auth:       Validate authentication and create OAuth2 credentials
  chat:       Interact with OpenAI models
  completion: Generate the autocompletion script for the specified shell
  configure:  Configure authentication and global properties
  help:       Help about any command
  project:    Manage projects
  results:    Retrieve results
  scan:       Manage scans
  triage:     Manage results
  utils:      Utility functions
  version:    Prints the version number

FLAGS
      --agent string               Scan origin name (default "ASTCLI")
      --apikey string              The API Key to login to Checkmarx One
      --base-auth-uri string       The base system IAM URI
      --base-uri string            The base system URI
      --client-id string           The OAuth2 client ID
      --client-secret string       The OAuth2 client secret
      --debug                      Debug mode with detailed logs
  -h, --help                       help for cx
      --insecure                   Ignore TLS certificate validations
      --profile string             The default configuration profile (default "default")
      --proxy string               Proxy server to send communication through
      --proxy-auth-type string     Proxy authentication type, (basic or ntlm)
      --proxy-ntlm-domain string   Window domain when using NTLM proxy
      --retry uint                 Retry requests to Checkmarx One on connection failure (default 3)
      --retry-delay uint           Time between retries in seconds, use with --retry (default 20)
      --tenant string              Checkmarx tenant
      --timeout string             Timeout for network activity, (default 5 seconds)

EXAMPLES
  $ cx configure
  $ cx scan create -s . --project-name my_project_name
  $ cx scan list

DOCUMENTATION
  https://checkmarx.com/resource/documents/en/34965-68620-checkmarx-one-cli-tool.html

QUICK START GUIDE
  https://checkmarx.com/resource/documents/en/34965-68621-checkmarx-one-cli-quick-start-guide.html

LEARN MORE
  Use 'cx <command> <subcommand> --help' for more information about a command.
  Read the manual at https://checkmarx.com/resource/documents/en/34965-68620-checkmarx-one-cli-tool.html
```

## auth

The `auth` command is used for validating the OAuth Clients against Checkmarx One.

### Auth Commands

`auth` can be used with the following commands:

#### auth register

{% hint style="warning" %}
The `auth register` command is no longer supported.
{% endhint %}


The `auth register` command was originally used to create OAuth2 clients through the CLI. However, this flow is no longer in use due to MFA (Multi-Factor Authentication) requirements.


OAuth2 client creation is now only supported through the UI, where the MFA process can be completed properly.

#### auth validate

The `auth validate` command is used for validating a client authentication against Checkmarx One.


##### Usage

```
./cx auth validate [flags]
```


##### Flags

**`--help, -h`**

Help for the validate command.


##### Examples

###### Validating Client Authentication

```
./cx auth validate
```

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx auth validate
Successfully authenticated to Checkmarx One server!
```

#### auth login

The `auth login` command is used for authenticating with Checkmarx One.


Opens your default web browser and guides you through the Checkmarx One sign-in process, including multi-factor authentication (MFA). After you sign in, the CLI stores a refresh token, allowing future CLI commands to authenticate without requiring you to sign in again.


By default, the refresh token is stored in the CLI configuration file. Use the optional `--session` flag to instead store the token for the current shell (`local`) or in a dedicated file shared across shells (`global`).


Signing in automatically revokes any previously issued refresh token and replaces it with a new one.


{% hint style="info" %}
If `--tenant` or `--base-auth-uri` are not specified, the CLI uses the values stored in the current CLI configuration. Specify these options to authenticate against a different tenant or IAM environment.
{% endhint %}


##### Usage

```
./cx auth login [flags]
```


##### Flags

**`--help, -h`**

Help for the login command.

**`--no-browser`**

Prints the authorization URL instead of opening a browser

**`--port` <int>**

Local port for the OAuth callback listener (0 = pick a free port)

**`--session` <string>**

Controls how the refresh token is stored. If omitted, the CLI uses the default configuration file.

- `local` – Stores the refresh token in the `CX_APIKEY` environment variable for the current shell session only. In **PowerShell**, pipe the login and logout commands through `Invoke-Expression`; in **Bash** or **Zsh**, use `eval`. This executes the generated command that sets or clears the environment variable in the current shell.
- `global` – Stores the refresh token in a persistent location that is shared across shell sessions. Unlike local, no `Invoke-Expression` or `eval` wrapper is required.


##### Examples

###### Default Session

```
./cx auth login --tenant my-tenant
```

###### Authenticating against a non-default environment

```
./cx auth login --tenant my-tenant --base-auth-uri <my-IAM-URL>
```

###### Local session in PowerShell and Bash

```
Invoke-Expression (cx auth login --tenant my-tenant --session local)
```

```
eval "$(cx auth login --tenant my-tenant --session local)"
```

###### Global Session

```
./cx auth login --tenant my-tenant --session global
```

#### auth logout

The `auth logout` command signs you out of Checkmarx One by revoking the current refresh token and removing any locally stored authentication credentials.


The command automatically detects how you authenticated and cleans up the appropriate storage location. If you authenticated using `--session local`, run the command through `Invoke-Expression` (PowerShell) or `eval` (Bash/Zsh) to clear the CX_APIKEY environment variable in the current shell.


No `--session` option is required when logging out.


##### Usage

```
./cx auth logout [flags]
```


##### Flags

**`--help, -h`**

Help for the logout command.


##### Examples

###### Default logout

```
cx auth logout
```

###### Local session (PowerShell)

```
Invoke-Expression (cx auth logout)
```

###### Local session (Bash/Zsh

```
eval "$(cx auth logout)"
```

## configure

The `configure` command is used for **Managing Checkmarx One scan configurations**.


The `configure` command can be used by itself or with a sub-command. When used by itself, it initiates a series of prompts which ask you to submit the authentication parameters.


### Usage

```
./cx configure [command] [flags]
```

#### Help

**`--help, -h`**

Help for the configure command.

### Configure Commands

`configure` can be used with the following commands:

#### configure (prompt)

The `configure` command initiates a series of prompts for configuring the CLI authentication credentials. The configurations are saved in a config file in the user's home directory under a subdirectory named ($HOME/.checkmarx).


{% hint style="info" %}
If you would like to set additional configuration parameters that are not related to authentication, then you need to use the `configure set` command.
{% endhint %}


##### Required Parameters

The following parameters are required for authentication, depending on the method being used. When the CLI prompts for values that aren't required for your authentication method, you can just hit ENTER.

- cx_apikey

{% hint style="info" %}
The CLI automatically extracts all relevant account info (Base URL, Auth URL, Tenant name) from the API Key. You can use arguments to submit these values explicitly, overriding the extracted values. However, this is generally not recommended.
{% endhint %}

- cx_base_uri
- cx_base_auth_uri
- cx_tenant
- cx_client_id
- cx_client_secret


##### CLI Authentication Parameters

The configure command prompts for the following authentication parameters

- AST Base URI - The base URL of your Checkmarx One environment.
   
   <details>
   
   <summary>Checkmarx One Server Base URLs</summary>
   
   - US Environment - https://ast.checkmarx.net
   - US2 Environment - https://us.ast.checkmarx.net
   - EU Environment - https://eu.ast.checkmarx.net
   - EU2 Environment - https://eu-2.ast.checkmarx.net
   - DEU Environment - https://deu.ast.checkmarx.net
   - Australia & New Zealand – https://anz.ast.checkmarx.net
   - India - https://ind.ast.checkmarx.net
   - India 2 - https://ind-2.ast.checkmarx.net/
   - Singapore - https://sng.ast.checkmarx.net
   - UAE - https://mea.ast.checkmarx.net
   - Israel - https://gov-il.ast.checkmarx.net
   
   </details>
- AST Base Auth URI - The base URI of the authentication server for you Checkmarx One environment.
   
   <details>
   
   <summary>Checkmarx One Authentication URLs</summary>
   
   - US Environment - https://iam.checkmarx.net
   - US2 Environment - https://us.iam.checkmarx.net
   - EU Environment - https://eu.iam.checkmarx.net
   - EU2 Environment - https://eu-2.iam.checkmarx.net
   - DEU Environment - https://deu.iam.checkmarx.net
   - Australia & New Zealand – https://anz.iam.checkmarx.net
   - India - https://ind.iam.checkmarx.net
   - Singapore - https://sng.iam.checkmarx.net
   - UAE - https://mea.iam.checkmarx.net
   - Israel - https://gov-il.iam.checkmarx.net
   
   </details>
- AST Tenant - The name of you Checkmarx One tenant account.
- Do you want to use API Key authentication? - Specify your authentication method. Y = API Key, N = OAuth client
- AST API Key - Your Checkmarx One API Key. See [Creating API Keys](https://docs.checkmarx.com/en/34965-188712-creating-api-keys.html)
- Checkmarx One Client ID - Your Checkmarx One OAuth client ID. See [Creating an OAuth Client](https://docs.checkmarx.com/en/34965-188033-creating-an-oauth-client-for-checkmarx-one-integrations.html)
- Client Secret - Your Checkmarx One OAuth secret.


##### Usage Example

```
C:\ast-cli_2.0.55_windows_x64>cx configure
Setup guide: https://checkmarx.com/resource/documents/en/34965-68621-checkmarx-one-cli-quick-start-guide.html

AST Base URI [https://eu.ast.checkmarx.net/]: https://ast.checkmarx.net/
AST Base Auth URI (IAM) [https://eu.iam.checkmarx.net/]: https://iam.checkmarx.net/
AST Tenant [ast_integration_tenant_eu]: myTenant
Do you want to use API Key authentication? (Y/N): n
Checkmarx One Client ID []: myOAuthClient
Client Secret []: myOAuthSecretuser@laptop:/ast$ ./cx.exe configure
Setup guide: https://checkmarx.atlassian.net/wiki/x/mIKctw
```

#### configure set

The `configure set` command is used for setting configuration properties. For each parameter (property) that you would like to set, you need to specify the property name and the value that you would like to assign to that property.


##### Usage

```
./cx configure set --prop-name <property name> --prop-value <property value>
```


##### Flags

**`---help, -h`**

Help for the configure command.

**`--prop-name <string>`**

Name of property set.

**`--prop-value <string>`**

Value of property set.


##### Properties

The following is a list of properties that can be set. Certain authentication properties are required, depending on your authentication method (API Key or OAuth client), see [Configuring the Checkmarx One CLI](https://docs.checkmarx.com/en/34965-118315-authentication-for-checkmarx-one-cli.html).

**`cx_apikey`**

An API Key to login to the Checkmarx One server.

**`cx_base_auth_uri`**

The URL of the Checkmarx One User Management server.

**`cx_base_uri`**

The URL of the Checkmarx One server.

**`cx_client_id`**

The client ID that is used for client authentication.

**`cx_client_secret`**

The client secret that is used for client authentication.

**`cx_http_proxy`**

An alternative method for specifying an optional proxy server. This enables users to designate a specialized proxy for use with Checkmarx One that doesn't affect the proxy used for other applications. When this is used it overrides the value of `http_proxy`.

**`cx_ignore_proxy`**

Set this environment variable as `true` in order to ignore any proxies configured in your system, so that all Checkmarx One CLI commands run directly from your local machine. Alternatively, this can be done by using the global flag `--ignore-proxy`.

**`cx_tenant`**

The customer's tenant name.

**`http_proxy`**

An optional proxy server configuration.

**`sca-resolver`**

The path to a correctly configured SCA resolver executable.


##### Examples

###### Setting the cx_base_uri Property

```
# Setting the Checkmarx One server URI
user@laptop:~/ast-cli$ ./cx configure set --prop-name cx_base_uri --prop-value https://eu.ast.checkmarx.net/
Setting property [ cx_base_uri ] to value [ https://eu.ast.checkmarx.net/ ]
```

#### configure show

The `configure show` command is used for retreiving the **configuration properties** for the current profile.


##### Usage

```
./cx configure show [flags]
```


##### Flags

**`---help, -h`**

Help for the configure command.


##### Examples

###### Presenting all the Configuration Parameters Values

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx configure show
Current Effective Configuration
                     BaseURI: https://eu.ast.checkmarx.net/
              BaseAuthURIKey: https://eu.iam.checkmarx.net/
                  Checkmarx One Tenant: MyTenant
                   Client ID: MyClientID
               Client Secret: ******cert
                      APIKey:
                       Proxy:
```

## help

The `help` command **provides a help menu** for **every CLI command/Sub-command** (Path for the command).


### Usage

```
./cx help [command] [flags]
```


### Available Commands

```
auth
configure
help
project
result
scan
utils
version
```


### Flags

**`--help, -h`**

Help for the help command.


### Examples

#### Using the help Command

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx --help
The Checkmarx One CLI is a fully functional Command Line Interface (CLI) that interacts with the Checkmarx One server.

USAGE
  cx <command> <subcommand> [flags]

COMMANDS
  auth:       Validate authentication and create OAuth2 credentials
  chat:       Interact with OpenAI models
  completion: Generate the autocompletion script for the specified shell
  configure:  Configure authentication and global properties
  help:       Help about any command
  project:    Manage projects
  results:    Retrieve results
  scan:       Manage scans
  triage:     Manage results
  utils:      Utility functions
  version:    Prints the version number

FLAGS
      --agent string               Scan origin name (default "ASTCLI")
      --apikey string              The API Key to login to Checkmarx One
      --base-auth-uri string       The base system IAM URI
      --base-uri string            The base system URI
      --client-id string           The OAuth2 client ID
      --client-secret string       The OAuth2 client secret
      --debug                      Debug mode with detailed logs
  -h, --help                       help for cx
      --insecure                   Ignore TLS certificate validations
      --profile string             The default configuration profile (default "default")
      --proxy string               Proxy server to send communication through
      --proxy-auth-type string     Proxy authentication type, (basic or ntlm)
      --proxy-ntlm-domain string   Window domain when using NTLM proxy
      --retry uint                 Retry requests to Checkmarx One on connection failure (default 3)
      --retry-delay uint           Time between retries in seconds, use with --retry (default 20)
      --tenant string              Checkmarx tenant
      --timeout string             Timeout for network activity, (default 5 seconds)


EXAMPLES
  $ cx configure
  $ cx scan create -s . --project-name my_project_name
  $ cx scan list

DOCUMENTATION
  https://checkmarx.com/resource/documents/en/34965-68620-checkmarx-one-cli-tool.html

QUICK START GUIDE
  https://checkmarx.com/resource/documents/en/34965-68621-checkmarx-one-cli-quick-start-guide.html

LEARN MORE
  Use 'cx <command> <subcommand> --help' for more information about a command.
  Read the manual at https://checkmarx.com/resource/documents/en/34965-68620-checkmarx-one-cli-tool.htmlcx.
```

Using the `--help` flag for the `project` command

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project --help
The project command enables the ability to manage projects in Checkmarx One.

USAGE
  cx project [flags]

COMMANDS
  create:     Creates a new project
  delete:     Delete a project
  list:       List all projects in the system
  show:       Show information about a project
  tags:       Get a list of all available tags

FLAGS
  -h, --help   help for project

ead the manual at https://checkmarx.atlassian.net/wiki/x/MYDCkQ
```

Using the `--help` command for the `project create` sub-command

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project create --help
The project create command enables the ability to create a new project in Checkmarx One.

USAGE
  cx project create [flags]

FLAGS
      --branch string         Main branch
      --format string         Format for the output. One of [json list table] (default "table")
      --groups string         List of groups, ex: (PowerUsers,etc)
  -h, --help                  help for create
      --project-name string   Name of project
      --tags string           List of tags, ex: (tagA,tagB:val,etc)

GLOBAL FLAGS
  --agent string               Scan origin name (default "ASTCLI")
  --apikey string              The API Key to login to Checkmarx One
  --base-auth-uri string       The base system IAM URI
  --base-uri string            The base system URI
  --client-id string           The OAuth2 client ID
  --client-secret string       The OAuth2 client secret
  --debug                      Debug mode with detailed logs
  --insecure                   Ignore TLS certificate validations
  --profile string             The default configuration profile (default "default")
  --proxy string               Proxy server to send communication through
  --proxy-auth-type string     Proxy authentication type, (basic or ntlm)
  --proxy-ntlm-domain string   Window domain when using NTLM proxy
  --retry uint                 Retry requests to Checkmarx One on connection failure (default 3)
  --retry-delay uint           Time between retries in seconds, use with --retry (default 20)
  --tenant string              Checkmarx tenant
  --timeout string             Timeout for network activity, (default 5 seconds)

DOCUMENTATION
  https://checkmarx.com/resource/documents/en/34965-68634-project.html

QUICK START GUIDE
  https://checkmarx.com/resource/documents/en/34965-68621-checkmarx-one-cli-quick-start-guide.html

LEARN MORE
  Use 'cx <command> <subcommand> --help' for more information about a command.
  Read the manual at https://checkmarx.com/resource/documents/en/34965-68620-checkmarx-one-cli-tool.html
```

## hooks

The `hooks` command is used for creating git hooks for use by Checkmarx One.


### Usage

```
./cx hooks [command][sub-command][flags]
```

### Hooks Commands

`hooks` is currently used on only with the `pre-commit` command.

#### hooks pre-commit

The **pre-commit** command is used to configure and run pre-commit secret detection scans.


For detailed information about usage and workflows, see [Pre-Commit Secret Scanning](https://docs.checkmarx.com/en/34965-364702-pre-commit-secret-scanning.html).


##### Usage

```
./cx hooks pre-commit [sub-command][flags]
```


##### sub-commands

**`secrets-help`**

Help for pre-commit secret detection.

**`secrets-ignore [flag]<string>`**

Add detected secrets to the ignore list so they won't be flagged in future scans. Either add the flag `--all` to ignore all detected secrets, or the flag `--resultIds` to ignore specific secrets, specified in a comma separated list.

**`secrets-install-git-hook`**

Install the the pre-commit hook for secret detection. By default the installation is done locally on the current repository. You can add the `--global` flag to install the hook globally for all of your Git repos.

**`secrets-scan`**

Trigger a secret detection scan of your current project.

**`secrets-uninstall-git-hook`**

Uninstall the pre-commit hook. If the pre-commit was installed globally, then the `--global` flag must be added to the uninstall command.

**`secrets-update-git-hook`**

Update the pre-commit hook for secret detection to the latest version. If the pre-commit was installed globally, then the `--global` flag must be added to the update command.


##### Flags

**`--all`**

Used with `secrets-ignore` sub-command to ignore all detected secrets.

**`--global`**

For global installation of hooks, add this flag to all sub-commands for installing, uninstalling or updating the hooks.

**`--resultIds <string>`**

Used with `secrets-ignore` sub-command to ignore specific secrets. Submit a comma separated list of result IDs of the secretst that will be ignored.

**`--help`**

Help for the hook commands.


##### Examples

###### Install locally

```
./cx hooks pre-commit secrets-install-git-hook
Installing local pre-commit hooks...
pre-commit installed at .git\hooks\pre-committriage show --scan-type <scan-type> --project-id <project-id> --similarity-id <similarity-id>
```

###### Install Globally

```
./cx hooks pre-commit secrets-install-git-hook --global
Installing global pre-commit hook...
Global pre-commit hook installed successfully.
```

###### Commit File With Secrets

```
./ git commit
Commit scanned for secrets: Detected 1 secret in 1 file #1 File: demo1
1 Secret detected in file
        Secret detected: github-refresh-token
        Result ID: 2c5e6579f07616bc5a6fbef2eba5d3cc7aaac59d
        Risk Score: 10.0
        Location: Line 1
                   1 | ghr_************************************
                   2 | Options for proceeding with the commit:
   - Remediate detected secrets using the following workflow (recommended):
      1. Remove detected secrets from files and store them securely. Options:
         - Use environmental variables
         - Use a secret management service
         - Use a configuration management tool
         - Encrypt files containing secrets (least secure method)
      2. Commit fixed code.   
   - Ignore detected secrets (not recommended):
      Use one of the following commands:
          cx hooks pre-commit secrets-ignore --all
          cx hooks pre-commit secrets-ignore --resultIds=id1,id2
   - Bypass the pre-commit secret detection scanner (not recommended):
      Use one of the following commands based on your OS:
         Bash/Zsh:
          SKIP=cx-secret-detection git commit -m "<your message>"
         Windows CMD:
          set SKIP=cx-secret-detection && git commit -m "<your message>"
         PowerShell:
          $env:SKIP="cx-secret-detection"
          git commit -m "<your message>"
```

## project

The `project` command is used for managing your Checkmarx One projects.


### Usage

```
./cx project [command] [flags]
```

#### Help

**`--help, -h`**

Help for the project command.

### Project Commands

`project` can be used with the following commands:

#### project create

The `project create` command enables the ability to **create a new project** in Checkmarx One.


##### Usage

```
./cx project create [flags]
```


##### Flags

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


##### Workflow Examples

###### Create a New Project

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

#### project delete

The `project delete` is used to **delete a project** in Checkmarx One.


##### Usage

```
./cx project delete --project-id <project-id> [flags]
```


##### Flags

**`--help, -h`**

Help for the delete command.

**`--project-id`**

Project ID to delete.


##### Workflow Example

<details>

<summary>Retrieve the Checkmarx One Projects List</summary>

```
user@laptop:/AST$ ./cx.exe project list

Project ID                           Name                         Created at Tags Groups 
----------                           ----                         ---------- ---- ------ 
fa5eeaac-2ec7-4fa7-946e-ed2f2e5ff8cd test-proj-del                08-24-21   []   []
```

</details>

###### Delete a Project

```
user@laptop:/AST$ ./cx.exe project delete --project-id fa5eeaac-2ec7-4fa7-946e-ed2f2e5ff8cd
```

<details>

<summary>Verify that the project doesn’t exist in the projects list</summary>

```
user@laptop:/AST$ ./cx.exe project list

Project ID                           Name                         Created at Tags Groups 
----------                           ----                         ---------- ---- ------
```

</details>

#### project list

The `project list` command provides a **list of all the projects** in Checkmarx One.


##### Usage

```
./cx project list [flags]
```


##### Flags

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


##### Pagination

This command uses pagination. By default it returns the first 20 results (i.e., `limit=20,offset=0`). Use `limit` to adjust the maximum number of results to return and `offset` to specify the number of results to skip before starting to return results. You can use `offset=0` and `limit=0` to get all results.

**Example: **The following command returns records 21-30

```
./cx project list --filter "limit=10,offset=20"
```


##### Applying Filters

You can limit results by using pagination and/or by filtering by various project attributes such as project IDs and project tags.

Filters are applied using the following syntax:

```
./cx project list --filter "attributeA=value1,attributeB=value1;value2;value3,..."
```

**Example: **The following command returns records for specific projects, based on project IDs.

```
./cx project list --filter "ids=7b70e4b6-4288-467b-8fa2-9c6c0ad0bd08;e231cf6d-f031-4290-b014-7c6ec343f793"
```

When multiple filter attributes are used, an AND operator is applied between attributes. When multiple values are given for an attribute, an OR operator is used between values.

**Example:** The following command returns records for all projects that have the tag key "product" and a tag value of either "AppA", "AppB" or "AppC".

```
./cx project list --filter "tags-keys=product,tags-values=AppA;AppB;AppC,limit=0"
```


##### Results

For each project, the following items are returned: Project ID, Project Name, Date that the project was created, and Tags and Groups associated with the project.

When results are returned in json format, an additional item `updatedAt` is returned, giving the date of the most recent edit of the project settings.

{% hint style="info" %}
The date given for `updatedAt` relates only to editing the project settings and not to running scans, generating reports or other activities on the project.
{% endhint %}


##### Examples

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

#### project show

The `project show` command **provides information about a project** in Checkmarx One.


##### Usage

```
./cx project show --project-id <project-id> [flags]
```


##### Flags

**`--project-id <string>` Required**

Project ID to show.

**`--format <string>` Default: table**

The output format for the response. Possible values are `json`, `list` or `table`.

**`---help, -h`**

Help for the show command.


##### Results

For each project, the following items are returned: Project ID, Project Name, Date that the project was created, and Tags and Groups associated with the project.

If the project configuration has been edited after the initial creation, then an additional item `updatedAt` is returned, giving the date of the most recent edit.

{% hint style="info" %}
The date given for `updatedAt` relates only to project configuration and not to running of scans, generating reports or other activities.
{% endhint %}


##### Workflow Examples

<details>

<summary>Retrieve Project IDs</summary>

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project list --format table

Project ID                           Name                                   Created at Tags    Groups                                 
----------                           ----                                   ---------- ----    ------                                 
ce46df28-7f33-49fe-88cb-337fe8eb2c39 Test1                                  09-29-21   []      []                                     
d7b56888-8407-4e9b-ae5b-7fc43233a497 Test111                                08-25-21   []      []                                     
d6fe8ab4-becd-49ff-987f-ec5ee02cc614 EffProj                                09-22-21   []      []
```

</details>

###### Use the project show command with various format flags

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project show --project-id ce46df28-7f33-49fe-88cb-337fe8eb2c39 --format table

Project ID                           Name  Created at Tags Groups 
----------                           ----  ---------- ---- ------ 
ce46df28-7f33-49fe-88cb-337fe8eb2c39 Test1 09-29-21   []   []
```

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project show --project-id ce46df28-7f33-49fe-88cb-337fe8eb2c39 --format list

Project ID : ce46df28-7f33-49fe-88cb-337fe8eb2c39
Name       : Test1
Created at : 09-29-21
Tags       : []
Groups     : []
```

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project show --project-id ce46df28-7f33-49fe-88cb-337fe8eb2c39 --format json
{"ID":"ce46df28-7f33-49fe-88cb-337fe8eb2c39","Name":"Test1","CreatedAt":"2021-09-29T11:52:15.924297Z","UpdatedAt":"2021-09-29T11:52:15.924297Z","Tags":{},"Groups":[]}
```

#### project tags

The `tags` command **provides a list of all the available tags** in your tenant.


Tags are also used for overriding **Jira feedback apps** fields values. For additional information see:


[Fields Override](https://docs.checkmarx.com/en/34965-68752-jira.html#fields-override)


##### Usage

```
./cx project tags [flags]
```


##### Flags

**`---help, -h`**

Help for the tags command.


##### Examples

###### Using the tags Command

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project tags
{"Demo":[""],"QA":["Automation","Manual"],"test":[""]}{"insecure-bank":[""],"insecure-bank-app":[""],"rwwr":[""],"wrwr":[""]}
```

#### project branches

The `branches` command **provides a list of all the available branches** in Checkmarx One.


##### Usage

```
./cx project branches [flags]
```


##### Flags

**`---help, -h`**

Help for the branches command.

**`--project-id <string>` Required**

Project ID of the project for which you would like to retrieve the branches.

**`--filter <string>` Default: return the first 20 records.**

{% hint style="success" %}
You can set the `limit` value as 0 in order to return all records.
{% endhint %}

Filter the branches returned within the specified project. Options are: `branch-name`, `limit`, and `offset`

- Use the "**;**" sign as the delimiter for arrays.
- Available filters are: `branch-name`, `limit`, and `offset`


##### Example

###### Using the project branches command

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project branches --project-id 5a529813-62bc-4d56-89a0-11ffc37b3bc6
["dev","main"]
```

## results

The `results` command is used to **retrieve scan results** in Checkmarx One.


### Usage

```
./cx results[command] [flags]
```

#### Help

**`--help, -h`**

Help for the results command.

### Results Commands

`results` can be used with the following commands:

#### results show

The `results show` command is used to **retrieve scan results** (i.e., generate reports) in Checkmarx One.


{% hint style="info" %}
Reports generated via the CLI use the standard scan report format. There is a newer type of customized scan report that can be generated via [API](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/ci2py4oc7hlt3-improved-reports-service-rest-api) or from the web application.
{% endhint %}


##### Usage

```
./cx results show [flags]
```


##### Flags

**`--scan-id <string>` Required**

Scan ID.

**`--filter <strings>` Default: All results are included**

Specify filters, pagination and sortin for the data that will be included in the report that is generated.

Filters aren't applied to PDF reports. You can specify which sections to include in a PDF report using `--report-pdf-options`.

- Use "**;**" to separate between multiple values for a particular filter.
- Use "," to separate between multiple filters.
- Available filters are: `limit`, `offset`, `sort`, `severity`, `state`, `status`.
- Enum values:
   
   - **severity** - Critical, High, Medium, Low, Info.
   - **state** - TO_VERIFY, NOT_EXPLOITABLE, PROPOSED_NOT_EXPLOITABLE, CONFIRMED, URGENT, EXCLUDE_NOT_EXPLOITABLE.
      
      {% hint style="info" %}
      The state filter can be applied either by submitting a separate value for each state to **include,** or by submitting the value `EXCLUDE_NOT_EXPLOITABLE` in order to exclude only `NOT_EXPLOITABLE` results.
      {% endhint %}
   - **status** - NEW, RECURRENT, FIXED.
   - **sort** - -severity, +severity, -status, +status, -state, +state, -type, +type, -firstfoundat, +firstfoundat, -foundat, +foundat, -firstscanid, +firstscanid.
      
      Default sorting: +status, +severity.
      
      {% hint style="success" %}
      "+" = ascending order
      
      "-" = descending order
      {% endhint %}

For an explanation of correct filter syntax, see [below](#below)

**`--help, -h`**

Help for the results command.

**`--output-name <string>` Default: cx_result**

Specify a name for the output file.

**`--output-path <string>` Default: "."**

Specify the file path for the output file.

**`--report-format <string>` Default: json**

Specify the format for the report that is generated.

Options are: `summaryHTML`, `summaryJSON`, `summaryConsole`, `sarif`, `gl-sast`, `gl-sca`, `json`, `json-v2`, `sonar`, `markdown`, `PDF`, or `SBOM`

{% hint style="info" %}
json-v2 is similar to the original json report. The main difference being that v2 is identical to the json report generated via the UI.
{% endhint %}

Json, json-v2, sarif, gl-sast, and sonar formats generate a detailed list of risks identified in the project (gl-sast returns only sast results and gl-sca returns only SCA results). SummaryHTML, summaryJSON, summaryConsole and markdown formats generate summary reports with aggregated risk data. PDF format reports by default generate a complete report including both a summary of risks as wel as a detailed list of risks. You can specify which sections to include in the report using `--report-pdf-options`.

{% hint style="success" %}
For SBOM reports, you need to add the `--report-sbom-format` flag to specify the SBOM standard and output format.
{% endhint %}

**`--report-pdf-email <string>`**

Specify email recipients who will receive the pdf report. Multiple emails are separated by a ",".

This flag can only be used when `--report-format` is set as `pdf`.

**`--report-pdf-options <string>` Default: All Sections**

Specify the sections that will be included in the pdf format report.

This flag can only be used when `--report-format` is set as `pdf`.

Available sections are: `Sast`, `Sca`, `Iac-Security`, `ScanSummary`, `ExecutiveSummary`, and `ScanResults`.

`ScanResults` includes results for all scanners (IaC-Security, Sast and Sca).

**`--report-sbom-format` Default: CycloneDxJson**

Specify the type of SBOM standard ([CycloneDX](https://cyclonedx.org/specification/overview/) or [SPDX](https://spdx.dev/about/)) as well as the output format.

Options are: `CycloneDxJson`, `CycloneDxXml`, or `SpdxJson`.

**`--sast-redundancy`**

Checkmarx identifies vulnerabilities with matching sub-flows, which enables prioritization of fixes that will resolve multiple vulnerabilities with a single fix.

When this flag is used, a new field `data.redundancy` is shown for each vulnerability, indicating which vulnerability should be prioritized as `fix` and which ones should be considered `redundant`.

**`--sca-hide-dev-test-dependencies`**

Adding this flag filters out dev and test dependencies from SCA results shown in scan reports.

Note: This flag is only relevant scans that ran the SCA scanner. Currently, this is not supported for PDF or SBOM reports.


##### Pagination

By default all results are included in the report (up to 10k). You can use `limit` to adjust the maximum number of results to return and `offset` to specify the number of results to skip before starting to return results.

**Example: **The following command generates a report for records 21-30.

```
./cx results show --filter "limit=10,offset=20"
```


##### Applying Filters and Sorting

You can filter the results included in the report by specifying various parameters such as severity, state and status. These filters apply both to the list of risks that is returned as well as to the summary data that is given. You can also specify how the list of risks is sorted in the report.

When multiple filter attributes are used, an AND operator is applied between attributes. When multiple values are given for an attribute, an OR operator is used between values.

Filters are applied using the following syntax:

```
./cx results show --filter "attributeA=value1,attributeB=value1;value2;value3,..."
```

**Example:** The following command returns a report that includes data for all risks with a severity level "high" or "medium" and the status "new". The results are sorted by "first found at" in descending order.

```
./cx results show --filter "severity=high;medium,status=new,sort=-firstfoundat+queryname"
```


##### Workflow Examples

<details>

<summary>Retrieve a list of scan ID’s</summary>

```
ophir@OphirS-Laptop:~/ast-cli$ ./cx scan list

Scan ID                              Project ID                           Status    Created at Tags    Initiator                      Origin                 
-------                              ----------                           ------    ---------- ----    ---------                      ------                 
3c028677-5df7-4bd9-8a10-7214ced45670 683c51da-8644-4e27-990f-1128ab911a1b Completed 09-10-21   []      service-account Github                 
c0507cb4-c68a-4db8-9565-5308d409a931 683c51da-8644-4e27-990f-1128ab911a1b Completed 09-10-21   []      service-account Github                 
5ee3482e-b068-4bc5-9671-1c98098b3062 683c51da-8644-4e27-990f-1128ab911a1b Completed 09-09-21   []      service-account Github
```

</details>

###### Retrieve scan results for a specific scan ID using default settings

```
./cx results show --scan-id <scan ID>
```

```
user@laptop:~/ast-cli$ ./cx results show --scan-id 3c028677-5df7-4bd9-8a10-7214ced45670
2023/08/03 22:33:32 Creating JSON Report:  cx_result.jsonCreating JSON Report:  cx_result.json
```

###### Retrieve scan results for a specific scan ID using several flags

```
./cx results show --scan-id <scan ID> --report-format sarif --output-name <file name> --output-path <output file location>
```

```
user@laptop:~/ast-cli$ ./cx results show --scan-id aca72f5d-1b58-4821-b7f0-508f857a9d4b --report-format sarif --output-name Demo_Sarif_Report --output-path "."
2023/08/04 12:17:38 Creating SARIF Report:  Demo_Sarif_Report.sarif
```

###### Generate a PDF report of SAST vulnerabilities and send it to an email recipient

```
./cx results show --scan-id <scan ID> --report-format pdf --report-pdf-email <recipient_email> --report-pdf-options <specify_sections>
```

```
user@laptop:~/ast-cli$ ./cx results show --scan-id aca72f5d-1b58-4821-b7f0-508f857a9d4b --report-format pdf --report-pdf-email demo@example.com --report-pdf-options sast
2023/08/04 12:25:52 Sending PDF report to:  [demo@example.com]
```

#### results codebashing

The `results codebashing` command is used to **retrieve Codebashing links** from Checkmarx One.


{% hint style="warning" %}
In order to use this command, you need to have a Codebashing account that has been linked to your Checkmarx One account. Please contact your Checkmarx support representative for assistance.
{% endhint %}


##### Usage

```
./cx results codebashing [flags]
```


##### Flags

**`--help, -h`**

Help for the results command.

**`--cwe-id <string>` Required**

CWE ID for the vulnerability.

**`--format <string>` Default: json**

The output format for the response. Possible values are `json`, `list` or `table`.

**`--language <string>` Required**

Language of the vulnerability.

**`--vulnerability-type <string>` Required**

Vulnerability type.


##### Examples

###### Retrieving codebashing link

```
./cx results codebashing  --language <language> --vulnerabity-type <vulnerability type> --cwe-id <cwe ID>
```

Sample command:

```
C:\ast-cli_2.0.53_windows_x64>cx results codebashing --language PHP --vulnerability-type Reflected XSS All Clients --cwe-id 79
```

#### results exit-code

The `results exit-code` command is used to retrieve information about the completion status for a particular scan in Checkmarx One. It also returns detailed information about failures of specific scan engines.


##### Usage

```
./cx results exit-code --scan-id <scan ID> [flags]
```


##### Flags

**`--scan-id <string>` Required**

The unique identifier of the scan for which you would like to retrieve the exit code info.

**`--scan-types <string>` Default: Returns data for each scanner that failed**

The scanners for which you would like to retrieve exit code info. You can submit multiple scanners, separated by a comma. Possible values are: sast,sca,iac-security,api-security,aisc

**`--help, -h`**

Help for the results exit-code command.


##### Examples

###### Retrieving exit code info for a particular scanner

```
./cx results exit-code  --scan-id <scan ID> --scan-types <scanner type>
```

Sample command:

```
C:\ast-cli_2.0.53_windows_x64>cx results exit-code --scan-id df16d6b8-213c-4525-ad3d-36977d4f2b2d --scan-types sast
[
  {
    "Name": "sast".
    "Status": "Failed",
    "Details": "Failed to get preset",
    "ErrorCode": "1024100"
  }
]
```

## scan

The `scan` command is used to **run and manage scans** in Checkmarx One.


### Usage

```
./cx scan [command] [flags]
```

{% hint style="info" %}
**--scan-timeout** flag can't be used with the **--async** flag.

When a scan is initiated in <u>asynchronous</u> mode using **--async** flag, Checkmarx One CLI does not wait for the result and completes the scan.
{% endhint %}

### Scan Commands

`scan` can be used with the following commands:

#### scan cancel

The `cancel` command is used to **cancel one or more running** **scans** in Checkmarx One.


##### Usage

```
./cx scan cancel --scan-id <scan ID> [flags]
```


##### Flags

**`--help, -h`**

Help for the cancel command.

**`--scan-id <string>` Required**

One or more comma separated scan IDs to cancel.

For example: <scan-id>, <scan-id>, ...


##### Workflow Examples

###### Retrieving all the scan ID’s statuses

<details>

<summary>Retrieve a list of scans and their statuses</summary>

```
user@laptop:/AST$ ./cx.exe scan list

Scan ID                              Project ID                           Status    Created at Tags Initiator                    Origin             
-------                              ----------                           ------    ---------- ---- ---------                    ------             
29a2b1e6-87c9-43b9-9d38-2d8165b390e1 df277b49-f1ef-4b5e-8cc4-0b66a2d1414a Running   08-27-21   []   user                         ASTCLI 2.0.0-rc.21
```

</details>

###### Cancel a running scan

```
user@laptop:/AST$ ./cx.exe scan cancel --scan-id 29a2b1e6-87c9-43b9-9d38-2d8165b390e1
```

<details>

<summary>Retrieve a list of scans and their statuses (after the cancellation)</summary>

```
user@laptop:/AST$ ./cx.exe scan list

Scan ID                              Project ID                           Status    Created at Tags Initiator                    Origin             
-------                              ----------                           ------    ---------- ---- ---------                    ------                               
29a2b1e6-87c9-43b9-9d38-2d8165b390e1 df277b49-f1ef-4b5e-8cc4-0b66a2d1414a Canceled   08-27-21   []   user                          ASTCLI 2.0.0-rc.21
```

</details>

###### Canceling several running scans

You can specify several comma separated scan ids in order to cancel multiple scans.

```
user@laptop:/AST$ ./cx.exe scan cancel --scan-id <scan_id1>,<scan_id2>
```

#### scan create

The `scan create` command enables users to **create and run new scans** in Checkmarx One.


##### Usage

```
./cx scan create [flags]
```


##### Scanning Source Code

The `scan create` command can be used to scan source code using the following methods:

- A compressed .zip archive
- A repository URL
- A local directory
   
   {% hint style="info" %}
   When you scan from a local directory, the CLI compresses the folder into a .zip archive and stores it in your system's temporary storage location until it is uploaded to Checkmarx One. When scanning from a local directory or ZIP file, the CLI supports multi-part uploads for compressed sources larger than 5 GB, up to a maximum of 6 GB. - Multi-part uploads are controlled by the `multipart_file_size` setting (chunk size in GB, range **1–5**, default **2 GB**). For configuration details, see [Checkmarx One CLI Config and Environment Variables](https://docs.checkmarx.com/en/34965-68624-checkmarx-one-cli-config-and-environment-variables.html#UUID-6c2fe558-13e9-31d8-738f-efd219cb8941_section-idm4554293728945633919364184784).
   
   - For sources larger than **5 GB**, it is recommended to increase the client timeout to reduce the risk of upload failures.
   {% endhint %}
- The full path to an SBOM file
   
   {% hint style="info" %}
   Relevant only for the SCA scanner, see [Scan using SCA Resolver](#scan-using-sca-resolver).
   {% endhint %}

{% hint style="info" %}
When a scan is run using multiple scanners, all scanners run in parallel.

When multiple scans are run in your account, the number of concurrent scans is specified in your account's license. This info is available under **Account Settings** > **License** > **License Plan Summary**. When the limit is exceeded, the scans are added to a queue which runs on a "first in first out" basis.
{% endhint %}

{% hint style="info" %}
When you scan a **folder** that contains files with unsupported file formats, those files aren't scanned.

However, you can include those files in the scan by using the **--file-include** flag.

For more details see [Scan with Inclusion of unsupported file formats](#scan-with-inclusion-of-unsupported-file-formats)
{% endhint %}

By default, scans include only supported files in the .zip archive submitted for scanning. The default file filters are applied to all scans.


The following is a list of the supported extensions and file names that are included by default in scans.


To include all files from the source location in the .zip archive, regardless of whether they are included in the supported files list, use the `--skip-default-filter` flag.


*.apex


*.apexp


*.asp


*.aspx


*.ascx


*.bas


*.build


*.c


*.cc


*.c++


*.cbl


*.cjs


*.cls


*.component


*.config


*.cpp


*.cs


*.cshtml


*.csproj


*.ctl


*.ctp


*.cts


*.cxx


*.dsr


*.dll


*.dart


*dock*


*Dockerfile*


*.eco


*.erb


*.frm


*.go


*.groovy


*.gsh


*.gvy


*.gy


*.h


*.hh


*.h++


*.hbs


*.hxx


*.htm


*.html


*.inc


*.java


*.javasln


*.jar


*.js


*.jsp


*.jspf


*.json


*.jsx


*.kt


*.kts


*.m


*.mjs


*.mts


*.object


*.page


*.php


*.php3


*.php4


*.php5


*.php56


*.phtm


*.phtml


*.pl


*.pm


*.plist


*.pkb


*.pck


*.pco


*.pks


*.pkh


*.plx


*.poetry.lock


*.project


*.properties


*.py


*.rb


*.report


*.requirement.txt


*.requirements.txt


*.rhtml


*.rjs


*.rs


*.rxml


*.scala


*.sc


*.sql


*.sln


*.sqb


*.swift


*.tag


*.tf


*.tfbacken


*.tfvars


*.tgr


*.tld


*.tpl


*.trigger


*.ts


*.tsx


*.twig


*.vb


*.vbs


*.vm


*.xml


*.xaml


*.xib


*.yaml


*.yarn.lock


build.gradle


build.sbt


composer.lock


Directory.Build.props


Directory.Packages.props


.dockerfile


go.mod


go.sum


Podfile


Podfile.lock


pyproject.toml

###### Excluded Folders

The following is a list of the folders that are automatically excluded from scans because their content is generally not relevant.

*.vs

*.vscode

*.idea

node_modules


##### File Filters

There are three methods for applying filters to files and folders for Checkmarx One scans.

- [Filter Entire Scan: `--file-filter` & `--file-filter-ext`](#filter-entire-scan-file-filter-file-filter-ext) - exclusions are applied during the pre-scan process, so that the excluded files aren't packaged into the .zip archive and are never uploaded to Checkmarx One.
- [Filters for Specific Scanners](#filters-for-specific-scanners) - apply filters for a specific scanner during the scan process, so that the specified scanner doesn't analyze the excluded files.
- [Apply `.gitignore` Exclusions](#apply-gitignore-exclusions) - exclude files and directories from the scan based on the patterns defined in the directory's .gitignore file

{% hint style="info" %}
File filtering mechanisms operate at different stages of the scan flow:

- `--file-filter` and `--file-filter-ext` affect which files are packaged in the .zip archive and uploaded to Checkmarx One. Files excluded by these filters are removed before the archive is created and are therefore not uploaded, are not available to any scanner, and cannot be restored by scanner-specific filters or filters applied in the web application (UI).
- Scanner-specific CLI filters, as well as filters applied in the project's settings via the web application (UI), only affect which uploaded files are analyzed by individual scanners.

Filters configured in the project's settings via the web application (UI) behave the same way as scanner-specific CLI filters: they only affect which files are analyzed by a scanner and do not affect the preparation of the .zip archive.

When filters are configured in the UI:

- if **Allow Override** is disabled, scanner-specific CLI filters do not take effect.
- If **Allow Override** is enabled, scanner-specific CLI filters override the UI filters.

UI filters do not override `--file-filter` or`--file-filter-ext`. If a file is excluded by either of these flags, it is removed before the .zip archive is created and cannot be scanned by any scanner, even if it is explicitly included by a UI filter.
{% endhint %}

###### Filter Entire Scan: `--file-filter` & `--file-filter-ext`

The `--file-filter` and `--file-filter-ext` flags provide the ability to filter the scanned file list as follows:

- Include files, file extensions.
- Exclude files, file extensions and folders.

The `scan create` command first applies the `--file-include` flag (or the default list of included file types) to establish the baseline of which files to include in the scan. It then further refines the file selection by applying the filters specified using `--file-filter` or `--file-filter-ext` .

**Limitation:** The `--file-filter` and `--file-filter-ext` flags work only if the scanned source code is a <u>directory</u> or a <u>ZIP file</u> (not a Git repository). However, this limitation does not apply when using the filter flags for specific scanners, see [Filters for Specific Scanners](#filters-for-specific-scanners).

The `--file-filter` flag supports wildcard-based filtering.


Supported Functionality:

- Use the `*` wildcard to match files.
   
   For example, `*.html` matches files with the `.html` extension.
- Use the `!` prefix to exclude files, file extensions, and folders.
   
   For example: `!*.html,!src*`
   
   {% hint style="info" %}
   When using `!` to exclude content, enclose the argument in single quotes.
   
   For example, `--file-filter '!mycompany.jar'`
   
   For more details see [Scan with Exclusion of Specific File or File Type](#scan-with-exclusion-of-specific-file-or-file-type)
   {% endhint %}
- Include files and file extensions.
   
   For example:
   
   - `t*` includes all files starting with `t`.
   - `*.txt` includes all files with the `.txt` extension.


**Limitations**


- Full paths are not supported. Therefore, you can only exclude an entire top-level folder, not a specific subfolder.
   
   For example, for the following file structure:
   
   `CxONE_TEST\apps\feature1\components\..`
   
   `CxONE_TEST\apps2\feature1\components\..`
   
   `CxONE_TEST\apps2\feature2\components\..`
   
   You can exclude all content under `apps2`, but you cannot exclude only the content under `feature2` or a specific component.
- `.git` folders and subfolders cannot be excluded.

###### `--file-filter-ext`

The `--file-filter-ext` flag enables you to include or exclude files and folders using Apache Ant-style glob patterns. Ant-style glob patterns provide directory-aware, recursive matching across complex project structures.

For example:

- `**/*.java` — includes `.java` files recursively across directories.
- `!**/test/**` — excludes content under `test` directories recursively.

###### Filters for Specific Scanners

The following flags are used to apply filters to SAST, IaC Security and SCA scanners respectively: `--sast-filter`, `--iac-security-filter`, `--sca-filter`. You can use these flags to specify file types.

{% hint style="info" %}
The filters for specific scanners **can** be used for all types of scans (directory, zip file or GIT repo), as opposed to `--file-filter` which does not work on GIT repositories.
{% endhint %}

{% hint style="info" %}
The `--sca-filter` flag is only used when the package resolution is done in the cloud (default). However, if you are using SCA Resolver to run package resolution locally, then file exclusion is done as follows: `--sca-resolver-params "--excludes <string>"`.
{% endhint %}

###### Examples

The following are some examples of how these flags can be used:

- for inclusion - `--sast-filter *.java`,
- for exclusion - `--sast-filter !*.java` or `--sca-filter !**\Dockerfile`

The following are a few examples:

- **Exclude all java files:** !**/*.java
- **Exclude all files inside a folder Test: **!**/Test/**
- **Exclude all files under root folder Test:** !Test/**
- **Exclude just the files inside a folder leaving all subfolders content:** !**/Test/*
- **Exclude all JavaScript minified files:** !**/*.min.js

If you would like to include only files inside specific folders, you need to first do a global exclude and then you can specify the folders to include.

For example:

`--sast-filter  !**/**,**/Folder01/**,**/Folder02/**` would cause the SAST scanner to run only on files inside “Folder01” and “Folder02”.

{% hint style="info" %}
For additional details about the syntax used for these filters, see [Flags](#flags). Learn more about glob patterns syntax [here](https://en.wikipedia.org/wiki/Glob_(programming)).
{% endhint %}

###### Filters for Container Security Scanner

Container Security has a specialized set of filter settings that enable users to configure their scans for precision and relevance. Filters can be applied to files, folders, packages and images. The following filter options are available:

- `--containers-package-filter` - Exclude packages by package name or file path using regex.
- `--containers-file-folder-filter` - Specify files and folders to be included or excluded from scans.
- `--containers-image-tag-filter` - Exclude images by image name and/or tag.
- `--containers-exclude-non-final-stages` - Scan only the final deployable image.

For additional details about the usage and syntax for these filters, see [Filters for Container Security Scanner](#filters-for-container-security-scanner).

###### Apply ".gitignore" Exclusions

When the flag `--use-gitignore` is submitted, Checkmarx One excludes files and directories from the scan based on the patterns defined in the directory's .gitignore file.

You can also pass the `use-gitignore` option using the global [`--optional-flags`](https://docs.checkmarx.com/en/34965-68626-global-flags.html) parameter.

###### Requirements

- Relevant only when scanning from a .zip file or a local directory, not when scanning from a code repository URL.
- There must be a .gitignore file present in the root directory of the repository.

###### Supported Patterns

The following patterns are currently supported when using the `--use-gitignore` flag:

| Pattern | Description |
| --- | --- |
| - src/<br>- **/src<br>- src/** | Each of these patterns ignores any directory named 'src' regardless of its location or contents. |
| application-jira.yml | Ignores a specific file named application-jira.yml |
| *.yml | Ignores all files ending with .yml extension |
| LoginController[0-3].java | Ignore files has names with a single digit 0 to 3 at the end, like LoginController0.java or LoginController1.java |
| LoginController[!0-3].java | Ignore files has names with a single digit except 0 to 3 at the end, like LoginController4.java or LoginController5.java |
| LoginController[01].java | Ignore files has names with a single digit 0 or 1 at the end, like LoginController0.java or LoginController1.java |
| LoginController[!456].java | Ignore files has names with a single digit except 4,5 or 6 at the end, like LoginController0.java or LoginController1.java |
| ?pplication-jira.yml | Ignores files with any single character prefix before pplication-jira.yml |
| a*cation-jira.yml | Ignores files starting with a and ending with cation-jira.yml |

###### Not Supported Patterns

The following patterns are not supported due to limitations in relative or recursive path handling, such as recursive wildcards (**) or relative paths:

{% hint style="info" %}
All patterns that are not supported via .gitignore are also not supported using `--file-filter`.
{% endhint %}

| Pattern | Description |
| --- | --- |
| /webapp/.jsp | Ignores .jsp files inside any webapp folder |
| main_modules/**/temp/ | Ignores all files inside any temp folder under main_modules |
| main_modules/**/.js | Ignores all .js files under main_modules at any depth |
| /application-jira.yml | Ignores only the root-level application-jira.yml |
| /config/.yml | Ignores .yml files inside the root-level config folder |


##### Checkmarx SCA Resolver

[Checkmarx SCA Resolver](https://docs.checkmarx.com/en/34965-581793-using-sca-resolver-in-checkmarx-one.html) is an on-prem utility that enables you to resolve and extract dependencies and fingerprints from your source code and send them to the Checkmarx One SCA scanner for risk analysis. This enables you to run a comprehensive SCA scan without the need to send your actual source code to the cloud. It also enables you to scan private (local) dependencies that aren’t accessible to the Checkmarx SCA cloud platform. For Checkmarx One users, Resolver is used in Offline mode for dependency resolution and the results file is then sent for analysis via your Checkmarx One account.

In order to use the SCA Resolver with the Checkmarx One CLI, you need to download the Checkmarx SCA Resolver separately in a location that the Checkmarx One CLI can find. Find the latest download at [Checkmarx SCA Resolver Download and Installation](https://docs.checkmarx.com/en/34965-19197-checkmarx-sca-resolver-download-and-installation.html).

To use the SCA Resolver, you need to add the **--sca-resolver** flag to your command line with an argument with the path to your local installation of the Resolver executable. See example below, [Scan using SCA Resolver](#scan-using-sca-resolver).

{% hint style="warning" %}
When running a CLI scan that uses SCA Resolver, the source code must be in a local folder, not in a zip archive or a code repository.
{% endhint %}

The Delta Scan feature will run by default on the CxOne CLI (since version 2.3.44) scans using SCAResolver (since version 2.13.3). To disable this feature, use the **--sca-resolver-params** flag with the argument **--disable-delta-scan**. For more information on this feature, see Delta Scans.

To add additional arguments to Checkmarx SCA Resolver, use the flag **--sca-resolver-params** with any additional arguments that you need. If necessary to use spaces and/or quotes, wrap the arguments in double quotes and use single quotes inside the value. For a complete list of SCA Resolver configuration arguments, see [Checkmarx SCA Resolver Configuration Arguments](https://docs.checkmarx.com/en/34965-132888-checkmarx-sca-resolver-configuration-arguments.html).

{% hint style="info" %}
Only arguments that can be used in **Offline** mode can be applied to scans run via the Checkmarx One CLI Tool and plugins.
{% endhint %}

<details>

<summary>Alternative Method</summary>

There is an alternative method that offers maximum control over the files being sent to the cloud for analysis. This is done by first running a scan using Resolver in offline mode on-prem. You can then run the scan create command in Checkmarx One and provide only the results file for upload. The following procedure describes this method.

1. Run SCA Resolver in offline mode and save the results to a file named `.cxsca-results.json` (precise name required) in the root path of your Checkmarx One CLI.
   
   ```
   ./ScaResolver offline -r "./cx-results/.cxsca-results.json" -s "%LOCATION_PATH%"
   ```
1. Run the `scan create` command in Checkmarx One, with the `-s` argument pointing to the folder where the Resolver results file was saved. For `--scan-types`, specify only `sca`.
   
   ```
   ./cx scan create -s "./cx-results/" --project-name "DemoProject" --branch "DemoBranch" --scan-types "sca"
   ```

</details>

For more information about using SCA Resolver in Checkmarx One CI/CD integrations, see Using SCA Resolver in Checkmarx One CI/CD Integrations.


##### Threshold

Configuring thresholds enables users to specify a threshold of vulnerability severities that, when found in a scan, will cause Checkmarx One to return a fail code for the scan. Users can then configure pipelines to break builds upon scan failure, so that scans that hit the threshold will break the build.

The threshold option supports a shorthand syntax with the format being a semi-colon separated list of key-value pairs.

The format for thresholds is **<engine>-<severity>=<limit>**

- Options for **engine**: sast, iac-security, sca, api-security, containers, sscs-secret-detection, sscs-scorecard
- Options for **severity**: Critical, High, Medium, Low, Info (Info is only for SAST engine)
- Options for **limit**: A number equal to or greater than 1

More than one threshold can be defined for each engine and thresholds can be set for multiple engines. Multiple thresholds should be separated by a semi-colon. An OR operator is applied, so that if any one of the thresholds is reached the scan will fail.

For example, to set the threshold for SAST as 10 high severity or 20 medium severity vulnerabilities, and for SCA as 10 high severity vulnerabilities, use the following syntax:

```
--threshold "sast-high=10; sast-medium=20; sca-high=10; containers-high=5"
```

{% hint style="info" %}
If a `--filter <string>` is applied to the `scan create` command, then the threshold applies with respect to the filtered vulnerability count.

**For example**:

If recurrent vulnerabilities are not a concern, you can set the filter to `status=NEW`, so that only `NEW` vulnerabilities are counted when determining whether the threshold was reached.
{% endhint %}


##### Reports

You can generate reports for the scan results as part of the `scan create` command.

{% hint style="info" %}
You can also generate reports for previous scans using the results show command.
{% endhint %}

There are two main types of reports:

- **Scan summary report** - gives a summary of the scan results, including the number of risks of various types and severity levels that were identified by the scan. This type of report is available in HTML, json, console and markdown format.
- **Complete scan report **- a comprehensive report showing details about each of the risks identified in the scan. This type of report can be generated in json, sarif or sonar format.
   
   {% hint style="info" %}
   Reports generated via the CLI use the standard scan report format. There is a newer type of customized scan report that can be generated via [API](https://checkmarx.stoplight.io/docs/checkmarx-one-api-reference-guide/branches/main/ci2py4oc7hlt3-improved-reports-service-rest-api) or from the web application.
   {% endhint %}

You can also generate PDF reports, for which you can specify which sections you would like to include in the report. In addition, for PDF reports, you can specify one or more email recipients who will receive an email with a download link for the report.

To generate a report as part of the `scan create` command, add the `--report-format` flag, specifying the format you would like to generate.

For PDF reports, use the following flags to specify email recipients and to specify which sections to include in the report.

```
./cx scan create --project-name <Project Name> -s <path> --branch <branch name> --report-format pdf --report-pdf-email <recipient_email> --report-pdf-options <specify_sections>
```

For information about the content of scan reports, see [Scan Reports](https://docs.checkmarx.com/en/34965-182434-checkmarx-one-reporting.html).

###### SBOM Reports

You can generate SBOM reports for the open source packages identified in your project by the SCA scanner. Reports can be generated in [CycloneDX](https://cyclonedx.org/specification/overview/) and [SPDX](https://spdx.dev/about/) formats, with additional “property” fields showing supplemental risk data. The reports can be exported in XML (for CycloneDX only) or JSON format. You can generate SBOM reports for Checkmarx One projects on which the SCA scanner has run. For more info about Checkmarx SBOMs, see [SBOM Reports](#sbom-reports).

Example for generating a CycloneDX SBOM report in JSON format:

```
./cx scan create --project-name <Project Name> -s <path> --branch <branch name> --report-format sbom --report-sbom-format CycloneDxJson
```

###### Generating an SBOM During Dependency Resolution

As an alternative to generating an SBOM from a completed SCA scan, you can use SCA Resolver together with the `--sbom-first` argument under `--sca-resolver-params` to generate a CycloneDX 1.7 SBOM immediately after dependency resolution completes. This approach can significantly reduce the time required to produce an SBOM because it does not require waiting for scan results.

{% hint style="info" %}
**Version requirements**: This capability is supported in Checkmarx One CLI version 2.3.54 and later, together with SCA Resolver version 2.14.3 and later.
{% endhint %}

To generate an SBOM while performing dependency resolution:

```
./cx scan create --project-name <Project Name> --scan-types sast,sca -s <path> --branch <branch name> --sca-resolver <path-to-resolver> --sca-resolver-params "--sbom-first"
```

The generated SBOM includes both manifest-resolved and binary-detected components and is written to the configured output directory.

{% hint style="info" %}
You can customize the generated SBOM file name and output location using the `--sbom-output-name` and `--sbom-output-path` SCA Resolver optional arguments. For more information, see Optional Arguments.
{% endhint %}

You can also generate an SBOM without running a scan by combining the `--sbom-first` argument with the `--no-scan` flag:

```
./cx scan create --project-name <Project Name> --scan-types sast,sca -s <path> --branch <branch name> --no-scan --sca-resolver <path-to-resolver> --sca-resolver-params "--sbom-first"
```

This command performs dependency resolution and generates an SBOM without submitting a scan to Checkmarx One.


##### Container Security Scans

When running scans via the CLI you can choose to scan the project files in order to analyze the Dockerfile in your project or you can submit specific images for scanning.

###### Authentication for Scanning Private Repos

In order to access private repos you need to be authenticated in your container repo at the time that you run the scan via Checkmarx One CLI.

{% hint style="info" %}
In addition, even when using public repos in DockerHub there is an advantage to authenticating your user in order to avoid the limits that apply to anonymous requests to public repos.
{% endhint %}

Authentication can be done via Docker or Podman.

Before running the scan, it is recommended to verify that you are able to access the image on your local machine.

For details about authentication for specific registries, see [Authentication for Scanning Private Repos](#authentication-for-scanning-private-repos).

<details>

<summary>Example - DockerHub Authentication</summary>

For DockerHub authentication make sure that your environment variables are set as:

- *DockerhubUsername* - your username
- *DockerhubToken* - your password or authorization token

</details>

###### Scan Procedure

1. Run the `scan create` command with all required parameters, and specify `container-security` in the `--scan-types`.
   
   ```
   ./cx scan create --project-name <Project Name> -s <Repository URL> --branch <branch name> --scan-types container-security
   ```
1. If you want to scan only specific images (not an entire project), do the following:
   
   1. Create a "dummy" folder in your project (for use in the `-s` parameter) and give it a name that indicates that it is used for scanning images, e.g., scan_ecr_image.
   1. In the CLI scan command, for the `-s` parameter give the path to the "dummy" folder that you created, e.g., `/Users/DemoUser/scan_ecr_image`.
1. Add the `--container-images` flag followed by a comma separated list of images. Specify each image using the following syntax {image_name}:{image_tag}.
   
   ```
   ./cx scan create --project-name <Project Name> -s <Repository URL> --branch <branch name> --scan-types container-security --container-images "mycompany/myimage:myimagetag"
   ```
   
   {% hint style="info" %}
   For additional details about precise syntax for container references, see [Authentication for Scanning Private Repos](#authentication-for-scanning-private-repos) and [Scanning Container Images via Checkmarx One CLI - Flag Validation and Best Practices](https://docs.checkmarx.com/en/34965-515429-scanning-container-images-via-checkmarx-one-cli---flag-validation-and-best-practices.html).
   {% endhint %}


##### Running Secret Detection and Repository Health Scans

When running a scan via the CLI tool, the Secret Detection and Repository Health (OSSF) scanners are grouped together under Software Supply Chain Security (SCS) scanner.

{% hint style="info" %}
When running the Scorecard scanner, it is mandatory to submit the repo url and an access token with at least read permissions for that repo.
{% endhint %}

**To run a Secret Detection and Repository Health scan:**

1. Prepare the command to run a scan, using the `scan create` command and specifying the project name, branch and zip file location or repository URL using the `--project-name` , `--branch` and `-s` flags.
   
   ```
   ./cx scan create --project-name <Project name> --branch <branch name> -s <path to zip archive>
   ```
1. By default, all licensed scanners are run, including SCS (assuming that all mandatory SCS parameters are specified). If you are using the `--scan-types` flag to specify the scanners that run, you need to explicitly include the `scs` scanner, e.g., `--scan-types sast,scs`.
1. By default, when scs is included, both Secret Detection and OSSF Scorecard are run. If you would like to run only one of these scanners, add the `--scs-engines` flag and specify the engine that you want to run: `secret-detection`, or `scorecard`.
1. Add `--git-commit-history=<true|false>` to enable or disable scanning Git commit history for Secret Detection. Default: false. Applies only when running `--scan-types scs` with `--scs-engines secret-detection`.
   
   Example:
   
   ```
   # Run Secret Detection (default: commit history disabled)
   cx scan create \
    --project-name demo --branch main -s . \
    --scan-types scs --scs-engines secret-detection
   # Run Secret Detection with commit history explicitly enabled
   cx scan create \
    --project-name demo --branch main -s . \
    --scan-types scs --scs-engines secret-detection \
    --git-commit-history=true
   ```
1. When running the scorecard scanner, it is mandatory to add the following flags:
   
   - `--scs-repo-url <string>` - specifying the URL of the repo that you are scanning.
      
      {% hint style="warning" %}
      Even when `-s` specifies a repo url, you still need to use this flag to submit the URL for the SCS scanner.
      {% endhint %}
   - `--scs-repo-token <string>` - specifying a token with read permission on the specified repo.
      
      {% hint style="info" %}
      This flag is required for both private and public repos.
      {% endhint %}
1. If you would like to generate a scan report (optional), add the `--report-format` flag, specifying the desired format (e.g., `--report-format json`). For more information about scan reports, see [here](https://docs.checkmarx.com/en/34965-68643-scan.html#UUID-a0bb20d5-5182-3fb4-3da0-0e263344ffe7_section-idm4631465209593633552409907579).
   
   {% hint style="warning" %}
   PDF format is not supported for the SCS scanner.
   {% endhint %}
1. Run the scan command.
   
   The following is an example of a command to run SAST on a zip archive and run Scorecard on the project's repo.
   
   ```
   user@laptop:~/ast-cli$ ./cx scan create -s . --branch master --project-name Test111 --scan-types sast,scs --scs-engines scorecard --scs-repo-url https://github.com/juice-shop/juice-shop --scs-repo-token <TOKEN> --report-format json
   ```


##### Scanning SBOMs

You can run an SCA scan on an SBOM file. The scan is run as a Checkmarx One project, with the source specified as an SBOM file. The SCA scanner returns comprehensive results of all risks associated with your open source packages. This enables customers who don’t want to submit their actual code, to obtain comprehensive SCA results for their project and manage the remediation via Checkmarx One.

Requirements:

- Supported file formats: json or xml following CycloneDX (v1.0-1.7) or SPDX (v2.3)
- It is mandatory to include the Package URL (purl) for each package in the SBOM. For more information about purl syntax, see [here](https://spdx.github.io/spdx-spec/v3.0/model/Software/Properties/packageUrl/).
- Only the SCA scanner can run on an SBOM

{% hint style="info" %}
For complete documentation of SBOM scanning, see [Scanning SBOMs](https://docs.checkmarx.com/en/34965-728599-scanning-sboms.html)
{% endhint %}

**To scan an SBOM:**

1. For the `-s` parameter, submit the full path to the SBOM file.
1. For `--scan-types`, specify `sca`.
1. Add the `--sbom-only` flag.

```
./cx scan create --project-name <Project Name> -s <path_to_SBOM_file> --scan-types sca --sbom-only
```


###### Exit Codes

When a scan finishes, it generates an exit code indicating whether or not the scan completed successfully. In case of failure, the exit code also indicates which scanner in particular failed.

These exit codes can be retrieved using a standard command in your shell, for example:

- Powershell - `$LastExitCode`
- CMD - `echo %ErrorLevel%`
- MAC - `echo $?`

The following is a list of possible exit codes:

<details>

<summary>Exit code - possible values</summary>

| Code | Explanation |
| --- | --- |
| 0 | All scanners completed successfully |
| 1 | Multiple scanners failed |
| 2 | SAST scanner failed |
| 3 | SCA scanner failed |
| 4 | IAC Security scanner failed |
| 5 | API Security scanner failed |

</details>

In addition, Checkmarx One provides a dedicated command, `results exit-code`, that retrieves detailed information about scan failures.


##### Flags

{% hint style="warning" %}
Whenever a parameter value (e.g., project name, file location etc.) has a space or other special character in it, it needs to be escaped either by enclosing it in double quotes (and using only single quotes within the value) or by using an escape character. The specific syntax for escaping characters will vary depending on the command-line interface or programming language you are using.
{% endhint %}

**`--apisec-swagger-filter <string>`**

Allow users to select specific folders or files that they want to include or exclude from the code scanning process. This setting applies only to the api-security scanner. Example: ./swagger.json

**`--async`**

Do not wait for scan completion.

**`--application-name <string>`**

Specify an application to which this project will be assigned.

{% hint style="info" %}
This is effective both when creating a new project as well when scanning an existing project. For existing projects, the new application is added but does not overwrite previously associated applications.
{% endhint %}

{% hint style="warning" %}
Adding an application to an existing project requires the permission `update-application`.
{% endhint %}

**`--branch <string>, -b <string>` Required**

Branch to scan.

This is a required flag even when scanning from a zip archive. If the zip archive doesn't represent a specific branch, you can submit `.unknown` as the value and it will be shown in the UI as "N/A". (You should not enter `N/A` as the value, as this will be misinterpreted by the system.)

**`--branch-primary`**

This flag sets the branch specified in `--branch` as the PRIMARY branch for the project.

**`--container-images <string>`**

If you would like to scan specific images, submit a comma separated list of images to be scanned. Specify each image using the following syntax {image_name}:{image_tag}. For the syntax for images in specific registries, see [Authentication for Scanning Private Repos](#authentication-for-scanning-private-repos).

{% hint style="warning" %}
This flag can only be used when the `container-security` scanner is running, see [--scan-types](#scan-types).
{% endhint %}

**`--containers-exclude-non-final-stages`=boolean**

Exclude all images that are not from the final stage of the build process, so that only the final deployable image is scanned.

{% hint style="warning" %}
Only supported for Dockerfile images.
{% endhint %}

**`--containers-file-folder-filter <string>`**

Specify **files and folders** to be included (allow list) or excluded from (block list) scans.

Syntax:

- Including a file type - *.java
- Excluding a file type - !*.java
- Use “,” sign to chain file types
   
   for example: **.*java*,**.js
- The parameter also supports including/excluding folders.
- Regex is not supported.

**`--containers-image-tag-filter <string>`**

Exclude **images** by image name and/or tag.

Syntax:

- `image-name:image-tag` - exclude by image name and tag
- `image-name` - exclude by image name
- `:image-tag` - exclude by image tag

{% hint style="info" %}
You can use wildcard (*) at the beginning, end or both.
{% endhint %}

**`--containers-local-resolution`**

Use this flag to run the Container Security scanner locally. By default it runs in the cloud.

This flag should be used when you need to pull images from private registries that aren't integrated with your Checkmarx One account.

**`--containers-package-filter <string>`**

Prevent sensitive private **packages** from being sent to the cloud for analysis. Exclude packages by package name or file path using regex.

Syntax: Regex

**`--exlude-git-folder`**

Excludes the .git folder from the scan source upload ZIP.

You can also pass the `exclude-git-folder` option using the global [`--optional-flags`](https://docs.checkmarx.com/en/34965-68626-global-flags.html) parameter.

**`--file-filter <string>, -f <string>`**

Source file filtering pattern for including or excluding files and folders. Refer to [File Filters](#file-filters).

**`--file-filter-ext <string>`**

Source file filtering pattern using Apache Ant-style glob patterns for directory-aware and recursive matching. Refer to [File Filters](#file-filters).

**`--file-include <string>`**

Comma separated list of additional file extensions to be included in the scan.

For example: *.java2,file.txt

**`--file-source <string>, -s <string>` Required**

The path to the compressed zip file, the path to the folder, or the repository URL to scan.

When scanning a private repository, a PAT for the repo should be provided using the following format:

`https:/<username>:<pat>@github.com/<org>/<repo>.git`

**`--filter <string>`**

Filter the list of results.

- Use ',' to separate between multiple filters
- Use ';' as to separate between multiple values for a given filter
- Available filters are:
   
   project-names, scan-ids, tags-keys, tags-values, branches, statuses, initiators, source-origins, source-types.
- Options for **severity**, **state**, and **status**:
   
   - **severity** - Critical, High, Medium, Low, Info.
   - **state** - TO_VERIFY, NOT_EXPLOITABLE, PROPOSED_NOT_EXPLOITABLE, CONFIRMED, URGENT, EXCLUDE_NOT_EXPLOITABLE.
      
      {% hint style="info" %}
      The state filter can be applied either by submitting a separate value for each state to **include,** or by submitting the value `EXCLUDE_NOT_EXPLOITABLE` in order to exclude only `NOT_EXPLOITABLE`.
      {% endhint %}
   - **status** - NEW, RECURRENT, FIXED.

For examples of proper filter syntax, see [below](#below)

**`--help, -h`**

Help for the create command.

**`--iac-security-filter <string>`**

Filter option specific to IaC Security scan

- Including a file type - *.java
- Excluding a file type - !*.java
- Use "," sign to chain filter types.
   
   For example: *.java,*.js
- The parameter also supports including/excluding folders.

**`--iac-security-platforms <string>, <string>`**

Specify the platforms that you would like the IaC Security scan to run on.

When this flag is used, it overrides your account's default settings.

**`--iac-security-preset-id`**

This flag received a string (UUID) corresponding to the ID of the IaC Security Preset that can be extracted from the UI on the IaC Preset table.

**`--ignore-policy`**

Ignore policy violations, so that they will not break the build.

{% hint style="warning" %}
Requires `override-policy-management` permission, otherwise the policies will be enforced even when the flag is sent.
{% endhint %}

**`--no-scan`**

Prevents CxOne scan from running after SBOM is generated locally.

{% hint style="info" %}
Relevant only when --sbom-first is submitted under --sca-resolver-params. Submitting this flag without --sbom-first causes an error.
{% endhint %}

**`--output-name <string>` Default: "cx_result"**

Output file name.

**`--output-path <string>` Default: "."**

Output path.

**`--project-groups <string>`**

List of groups associated with projects.

For example: (groupA,groupB).

Limitation: This flag only works when creating a new project. For an existing project, it won't update the groups.

**`--project-name <string>` Required**

Name of the project.

When using the `--project-name` flag, the Project name must be written in **quotes** if there is a space in the project name.

For example: Test, Test1, "Test 1".

**`--project-private-package` NOT FULLY SUPPORTED YET Default: false**

You can designate a scan as a "Private Package" and assign a package version to it. Once a private package has been scanned, info about the risks affecting that package will be identified by SCA when that package version is used in any of you projects. You can download an article about private packages [here](https://checkmarx.atlassian.net/wiki/spaces/CR/pages/6594035713/Checkmarx+SCA+Resources#Private-Packages).

True = designate as private package.

False = not a private package.

When using this flag, you should also specify the package version using `--sca-private-package-version`.

**`--project-tags <string>`**

List of tags to associate to projects.

For example: (tagA,tagB:val, etc)

{% hint style="warning" %}
When this flag is used, the tags that are submitted overwrite any existing tags that were assigned to the project.
{% endhint %}

**`--proxy str <string>` Optional**

Proxy server to route Checkmarx One CLI network communication through.

Format: `http://<proxy_ip>:<port>` or `http://<username>:<password>@<proxy_ip>:<port>`.

When specified, the protocol prefix (`http://` or `https://`) is required.

**`--report-format <string>` Default: summaryConsole**

Report output format.

Specify one of the following:

json, json-v2, summaryHTML, summaryJSON, summaryCONSOLE, sarif, gl-sast, gl-sca, sonar, markdown or PDF, SBOM

{% hint style="info" %}
json-v2 is similar to the original json report. The main difference being that v2 is identical to the json report generated via the UI.
{% endhint %}

Report formats json, sarif, gl-sast and sonar generate complete scan reports (gl-sast returns only sast results and gl-sca returns only SCA results).

Report formats summaryHTML, summaryJSON, summaryCONSOLE and markdown generate summary reports.

For SBOM reports, you need to add the `--report-sbom-format` flag to specify the SBOM standard and output format.

**`--report-pdf-email <string>`**

Specify email recipients who will receive the pdf report. Multiple emails are separated by a ",".

This flag can only be used when `--report-format` is set as `pdf`.

**`--report-pdf-options <string>` Default: All Sections**

Specify the sections that will be included in the pdf format report.

This flag can only be used when `--report-format` is set as `pdf`.

Available sections are: `Sast`, `Sca`, `Iac-Security`, `ScanSummary`, `ExecutiveSummary`, and `ScanResults`.

`ScanResults` includes results for all scanners (IaC-Security, Sast and Sca).

**`--report-sbom-format` Default: CycloneDxJson**

The type of SBOM standard ([CycloneDX](https://cyclonedx.org/specification/overview/) or [SPDX](https://spdx.dev/about/)) as well as the output format.

Specify one of the following:

CycloneDxJson, CycloneDxXml, SpdxJson

This needs to be specified when the `--report-format` is set to "SBOM".

**`--resubmit`**

Apply the configurations used in the most recent scan in this project branch to the current scan.

Even when this flag is used, if an argument in the current scan differs from the configuration of the previous scan, the argument in the current scan takes precedence.

**`--sast-fast-scan`=boolean**

`true` - Run SAST scan using Fast Scan mode.

`false` - Do not run SAST scan using Fast Scan mode.

{% hint style="info" %}
If this flag is sent with no value (not recommended), then it is interpreted as `true`. If the flag is not sent then the default project or account settings are applied.
{% endhint %}

**`--sast-filter <string>`**

Filter option specific to SAST engine or scan.

- Including a file type - *.java
- Excluding a file type - !*.java
- Use "," sign to chain filter types.
   
   For example: *.java,*.js
- The parameter also supports including/excluding folders.

**`--sast-incremental`=boolean**

`true` - Run SAST scan as an Incremental scan.

`false` - Do not run SAST scan as Incremental (i.e., run full scan).

{% hint style="info" %}
If this flag is sent with no value (not recommended), then it is interpreted as `true`. If the flag is not sent then the default project or account settings are applied.
{% endhint %}

**`--sast-light-queries`=boolean**

`true` - Run SAST scan as a Light Queries scan.

`false` - Do not run SAST scan as LIght Queries (i.e., run standard queries).

{% hint style="info" %}
If this flag is not sent then the default project or account settings are applied.
{% endhint %}

**`--sast-preset-name <string>`**

The name of the Checkmarx preset to use.

**`--sast-recommended-exclusions`=boolean**

`true` - Run SAST scan using predefined exclusion rules.

`false` - Run SAST scan including all files and directories in the scan.

{% hint style="info" %}
If this flag is not sent then the default project or account settings are applied.
{% endhint %}

**`--sbom-only`**

Use this flag to run a scan only on the sbom at the specified file path.

Supported for CycloneDX (v1.0-1.7) and SPDX (v2.3) in xml or json format. For more information, see SBOM documentation.

{% hint style="success" %}
Relevant only when running scans using the SCA scanner.
{% endhint %}

**`--sca-hide-dev-test-dependencies`**

Adding this flag filters out dev and test dependencies from SCA results shown in scan reports.

Note: This flag is only relevant when running a scan with the SCA scanner and using the [--report-format](#report-format) flag to generate a report. Currently, this is not supported for PDF or SBOM reports.

**`--sca-exploitable-path` <string>**

Enable/disable the Exploitable Path feature for this scan.

`true` = enabled

`false` = disabled

{% hint style="info" %}
This flag must be sent with a value of `true` or `false`. If the flag is not sent, then the default project or account settings are applied.
{% endhint %}

Learn more about Exploitable Path.

**`--sca-filter <string>`**

Filter option specific to SCA engine or scan.

{% hint style="info" %}
This flag is only used when the package resolution is done in the cloud (default). However, if you are using SCA Resolver to run package resolution locally, then file exclusion is done as follows: `--sca-resolver-params "--excludes <string>"`.
{% endhint %}

- Including a file type - *.java
- Excluding a file type - !*.java
- Use "," sign to chain file types.
   
   For example: *.java,*.js
- The parameter also supports including/excluding folders.

**`--sca-last-sast-scan-time <integer>` Default: 1**

Specify the number of days that SAST scan results are considered valid for use in Exploitable Path (i.e., if there is no current SAST scan, how many days prior to the current SCA scan will Checkmarx One look for a SAST scan to use for analyzing Exploitable Path).

Options: integer ≥ 1

{% hint style="success" %}
Only **full **SAST scans are used for Expoitable Path, results from incremental scans aren't considered.
{% endhint %}

{% hint style="warning" %}
The `--sca-last-sast-scan-time` flag is only supported for single-tenant environments, not for multi-tenant.
{% endhint %}

**`--scan-info-format <string>` Default: list**

- Selects the scan info output format.
- Select one of the follwoing formats:
   
   list, table, json

**`--scan-timeout <int>`**

Cancel the scan and fail after the timeout in minutes.

**`--scan-types <string>` Default: all scanners licensed for your account**

Scan engines to be run for this scan.

For example: (sast,iac-security,sca,api-security,container-security,scs,aisc).

**`--sca-private-package-version` NOT FULLY SUPPORTED YET Default: False**

When you designate a scan as a private package using the `--project-private-package` flag, you should also specify the package version using this flag.

e.g., 0.1.1

You can download an article about private packages [here](https://checkmarx.atlassian.net/wiki/spaces/CR/pages/6594035713/Checkmarx+SCA+Resources#Private-Packages).

**`--sca-resolver-params <string>`**

Additional arguments to use with CxSCA Resolver. The arguments can be found here. The SCA Resolver runs in **offline mode**, only arguments compatible with this mode will work. The resolver params must be enclosed in quotes "", see example below.

**`--sca-resolver <string>`**

Use Checkmarx SCA Resolver to locally resolve SCA project dependencies. Specify the path to your local installation of SCA Resolver binary (executable).

When running a CLI scan that uses SCA Resolver, the source code must be in a local folder, not in a zip archive or a code repository.

**`--scs-engines <string>` Default: All supported SCS scanners**

SCS scan engines to run for this scan. Options: `secret-detection`,`scorecard`

This flag can only be used when the scs scanner is used for the scan (either by default or by specifying it in `--scan-types`).

**`--git-commit-history <boolean>` Default: false**

Enable/disable Git commit history scanning for Secret Detection.

- `true` = scans source code + Git commit history
- `false` = scans source code only

{% hint style="info" %}
This flag is only relevant when running the scs scanner with `--scs-engines secret-detection`.
{% endhint %}

**`--scs-repo-url <string>`**

Specify the URL of the repo that you are scanning.

{% hint style="warning" %}
Even when `-s` specifies a repo url, you still need to use this flag to submit the URL for the SCS scanner.
{% endhint %}

**`--scs-repo-token <string>`**

Submit a token with read permission on the specified repo.

{% hint style="info" %}
This flag is required for both private and public repos.
{% endhint %}

**`--skip-default-filter`**

Includes all files from the source location in the .zip archive, regardless of whether they are included in the supported files list.

**`--ssh-key <string>`**

Path to ssh private key.

**`--tags <string>`**

List of tags associated to scans.

For example: (tagA,tagB:val,etc)

**`--threshold <string>`**

Threshold count of severity of scan results based on the engine.

The threshold format is:

`<engine>-<severity>=<limit>`

For more information, see [Threshold](#threshold).

**`--use-gitignore`**

Adding this flag excludes files and directories from the scan based on the patterns defined in the directory's `.gitignore` file. For more information, see [Apply `.gitignore` Exclusions](#apply-gitignore-exclusions).

**`--wait-delay <int>` Default: 5 seconds**

Polling wait time (seconds) to get scan status.


##### Examples

###### Scan from a Git repository

```
./cx scan create --project-name <Project Name> -s <Repository URL> --branch <branch name>
```

Sample command:

```
C:\ast-cli_2.0.53_windows_x64>cx scan create  --project-name elidemo -s https://github.com/juice-shop/juice-shop --branch master
```

Sample response:

```
Scan ID      : 492e1626-9489-4ee9-ac1b-628de56c5e33
Project ID   : a1b1b151-d763-4f34-bfbc-de8c1422c02c
Project Name : elidemo
Status       : Running
Created at   : 08-07-23
Branch       : master
Tags         : []
Type         : Full
Timeout      : NONE
Initiator    : eli
Origin       : ASTCLI 2.0.53
Engines      : [ sast kics sca apisec]

2023/08/07 22:14:02 Scan Finished with status:  Completed
            Scan Summary:
              Created At: 2023-08-07, 22:07:57
              Project Name: elidemo
              Scan ID: 492e1626-9489-4ee9-ac1b-628de56c5e33

            Results Summary:
              Risk Level: High Risk

              -----------------------------------
              API Security - Total Detected APIs: 0
              -----------------------------------

            Policy Management Violation:
              Policy: DemoHigh | Break Build: false | Violated Rules: highVulnerability;

              Total Results: 170
              -----------------------------------
              |             High: 90            |
              |           Medium: 66            |
              |              Low: 13            |
              |             Info: 1             |
              -----------------------------------
              |     IAC-SECURITY: 41            |
              |             SAST: 0             |
              |   APIS WITH RISK: 0             |
              |              SCA: 129           |

              Checkmarx One - Scan Summary & Details: https://eu.ast.checkmarx.net/projects/a1b1b151-d763-4f34-bfbc-de8c1422c02c/scans?id=492e1626-9489-4ee9-ac1b-628de56c5e33&branch=master
```

###### Scan from a private Git repository

```
./cx scan create --project-name <Project Name> -s <https:/<username>:<pat>@github.com/<org>/<repo>.git> --branch <branch name>
```

Sample command:

```
C:\ast-cli_2.0.53_windows_x64>cx scan create  --project-name elidemo -s https://myPrivateRepo:1234567abcde@github.com/demoOrg/demoRepo --branch master
```

###### Scan from a source directory

```
./cx scan create -s <path> --branch <branch name> --project-name <Project Name>
```

Sample command:

```
user@laptop:~/ast-cli$ ./cx scan create -s . --branch main --project-name Test111
```

###### Scan in asynchronous mode

```
./cx scan create --project-name <Project Name> -s <Repository URL> --branch <branch name> --async
```

Sample command:

```
user@laptop:/AST$ ./cx scan create --project-name demo -s . --branch main --async
```

###### Scan using specific scanners

```
./cx scan create --project-name <Project Name> -s <Repository URL> --branch <branch name> --scan-types <scan types>
```

Sample command:

```
user@laptop:/AST$ ./cx scan create --project-name demo -s . --branch main --scan-types iac-security
```

###### Scan using SCA Resolver

```
./cx scan create --project-name <Project Name> -s <path> --branch <branch name> --sca-resolver <path-to-resolver> --sca-resolver-params <additional-resolver-arguments>
```

Sample command:

```
user@laptop:/AST$ ./cx scan create --project-name demo --scan-types sast,sca -s . --sca-resolver /sca/scaResolver --sca-resolver-params "-q -e my_file" --async
```

###### Scan with Inclusion of unsupported file formats

```
./cx scan create -s <path> --branch <branch name> --project-name <Project Name> --file-include <string>
```

Sample command:

```
user@laptop:~/ast-cli$ ./cx scan create -s ./Source-Folder/ --branch main --project-name Test111 --file-include sample.txt,*.myextension
```

###### Scan with exclusion of specific file or file type

```
./cx scan create -s <path> --branch <branch name> --project-name <Project Name> --file-filter <string>
```

Sample command:

```
user@laptop:~/ast-cli$ ./cx scan create -s scan_files/ --branch main --project-name Test111 --file-filter !*mycompany*.jar
```

###### Scan with exclusion of a specific folder

```
./cx scan create -s <path> --branch <branch name> --project-name <Project Name> --file-filter <folder name>
```

Sample command:

```
user@laptop:~/ast-cli$ ./cx scan create -s scan_files/ --branch main --project-name Test111 --file-filter !main
```

###### Scan with threshold

```
./cx scan create --project-name <Project Name> -s <path> --branch <branch name> --threshold <engine>-<severity>=<limit>
```

Sample command:

```
user@laptop:/ast-cli$ ./cx scan create --project-name myproject -s my_file.zip --branch main --threshold sast-high=1
```

Sample response:

```
Created At: 2022-01-26, 11:24:20
               Risk: High Risk
         Project ID: 49e6d565-933b-4a55-8d08-ec026ddcd7e2
            Scan ID: bdab6a9e-eb90-4cab-8783-5c3a2a052b31
       Total Issues: 28
        High Issues: 3
      Medium Issues: 11
         Low Issues: 14
IaC Security Issues: 18
      CxSAST Issues: 9
       CxSCA Issues: 1
2022/01/26 11:25:14 Threshold check finished with status Failed : sast-high: Limit = 1, Current = 2 |
```

###### Scan and send report to email recipient

```
./cx scan create --project-name <Project Name> -s <path> --branch <branch name> --report-format pdf --report-pdf-email <recipient_email> <specify_sections>
```

Sample command:

```
user@laptop:/ast-cli$ ./cx scan create --project-name EliCLIDemo -s . --branch main --report-format pdf --report-pdf-email demo@example.com ExecutiveSummary
```

Sample response:

```
2023/08/07 22:30:45 Scan Finished with status:  Completed
2023/08/07 22:30:56 Sending PDF report to:  [demo@example.com]
            Scan Summary:
              Created At: 2023-08-07, 22:24:56
              Project Name: elidemo
              Scan ID: 861ce408-f355-4692-9bff-3d35a6c17170

            Results Summary:
              Risk Level: High Risk

              -----------------------------------
              API Security - Total Detected APIs: 0
              -----------------------------------

            Policy Management Violation:
              Policy: EliHigh | Break Build: false | Violated Rules: high;

              Total Results: 170
              -----------------------------------
              |             High: 90            |
              |           Medium: 66            |
              |              Low: 13            |
              |             Info: 1             |
              -----------------------------------
              |     IAC-SECURITY: 41            |
              |             SAST: 0             |
              |   APIS WITH RISK: 0             |
              |              SCA: 129           |

              Checkmarx One - Scan Summary & Details: https://eu.ast.checkmarx.net/projects/a1b1b151-d763-4f34-bfbc-de8c1422c02c/scans?id=861ce408-f355-4692-9bff-3d35a6c17170&branch=master
```

###### Scan and generate report with filtered content

```
./cx scan create --project-name <Project Name> -s <path> --branch <branch name> --report-format <format> --filter <filter_type>=<value>;<value>
```

Sample command:

```
user@laptop:/ast-cli$ ./cx scan create --project-name EliCLIDemo -s . --branch main --report-format json --filter state=TO_VERIFY;CONFIRMED;URGENT --filter status=NEW --filter severity=critical;high
```

#### scan delete

The `delete` command is used to **delete one or more scans** in Checkmarx One.


##### Usage

```
./cx scan delete --scan-id <scan ID>
```


##### Flags

**`--help, -h`**

Help for the delete command.

**`--scan-id` Required**

One or more comma separated scan IDs to delete.

For example: <scan-id>,<scan-id>,...


##### Workflow Examples

<details>

<summary>Retrieve a list of scans</summary>

```
user@laptop:/AST$ ./cx scan list

Scan ID                              Project ID                           Status    Created at Tags Initiator Origin             
-------                              ----------                           ------    ---------- ---- --------- ------             
7eb83ed3-5734-4428-92a2-4819fc6c490f 9f47d3d7-76f2-418b-9513-e3e02cc5cbb9 Completed 08-27-21   []   org_admin ASTCLI 2.0.0-rc.21
```

</details>

###### Delete a scan

```
user@laptop:/AST$ ./cx scan delete --scan-id 7eb83ed3-5734-4428-92a2-4819fc6c490f
```

<details>

<summary>Verify that the scan isn't shown in the scan list</summary>

```
user@laptop:/AST$ ./cx scan list

Scan ID                              Project ID                           Status    Created at Tags Initiator Origin             
-------                              ----------                           ------    ---------- ---- --------- ------
```

</details>

###### Delete several scans

You can specify several comma separated scan ids in order to delete multiple scans.

```
./cx scan delete --scan-id 7eb83ed3-5734-4428-92a2-4819fc6c490f,a2f45c91-18ba-4d69-a748-972d0ecc1453
```

#### scan list

The `scan list` command provides a **list of all the scans** in your Checkmarx One account.


##### Usage

```
./cx scan list [flags]
```


##### Flags

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


##### Pagination

This command uses pagination. By default it returns the first 20 results (i.e., `limit=20,offset=0`). Use `limit` to adjust the maximum number of results to return and `offset` to specify the number of results to skip before starting to return results. You can use `offset=0` and `limit=0` to get all results.

**Example: **The following command returns records 21-30

```
./cx scan list --filter "limit=10,offset=20"
```


##### Applying Filters

You can limit results by filtering by various scan attributes such as scan IDs, project ID, scan tags, scan status and date range.

Filters are applied using the following syntax:

```
./cx scan list --filter "attributeA=value1,attributeB=value1;value2;value3,..."
```

**Example: **The following command returns records for all scans run on specific projects, based on project ID.

```
./cx scan list --filter "project-id=f761f24b-fbcc-4502-acef-7fa3f2de38ed"
```

When multiple filter attributes are used, an AND operator is applied between attributes. When multiple values are given for an attribute, an OR operator is used between values.

**Example:** The following command returns records for all scans with the tag key "product" and a tag value of either "AppA", "AppB" or "AppC" that were run since Jan 1, 2023.

```
./cx scan list --filter "tags-keys=product,tags-values=AppA;AppB;AppC,from-date=2023-01-01T00:00:00Z,limit=0"
```


##### Examples

###### Using the scan list command with format flags

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

#### scan show

The `show` command is used to **retrieve information about a scan** in Checkmarx One.


##### Usage

```
./cx scan show --scan-id <scan id> [flags]
```


##### Flags

**`--format <string>` Default: table**

The output format for the response. Possible values are `json`, `list` or `table`.

**`--scan-id <string>` Required**

Scan ID to show.

**`--help, -h`**

Help for the show command.


##### Examples

###### Using the scan show command with default settings

```
C:\ast-cli_2.0.53_windows_x64>cx scan show --scan-id 0f405e10-10c4-4fe9-a356-86253a52ab20

Scan ID                              Project ID                           Project Name Status  Created at Branch Tags Type Timeout Initiator Origin        Engines                
-------                              ----------                           ------------ ------  ---------- ------ ---- ---- ------- --------- ------        -------                
0f405e10-10c4-4fe9-a356-86253a52ab20 a1b1b151-d763-4f34-bfbc-de8c1422c02c elidemo      Partial 08-05-23   master []   Full NONE    eli       ASTCLI 2.0.53 [sast kics sca apisec]
```

###### Using the scan show command with format flag

```
C:\ast-cli_2.0.53_windows_x64>cx scan show --format json --scan-id 0f405e10-10c4-4fe9-a356-86253a52ab20
{"ID":"0f405e10-10c4-4fe9-a356-86253a52ab20","ProjectID":"a1b1b151-d763-4f34-bfbc-de8c1422c02c","ProjectName":"elidemo","Status":"Partial","CreatedAt":"2023-08-05T23:25:06.290004+03:00","UpdatedAt":"2023-08-05T20:28:43.918848Z","Branch":"master","Tags":{},"SastIncremental":"Full","Timeout":"NONE","Initiator":"eli","Origin":"ASTCLI 2.0.53","Engines":["sast","kics","sca","apisec"]}
```

#### scan tags

The `tags` command is used to **provide a list of all the available tags** in Checkmarx One.


Tags can be used for overriding **Jira feedback app** fields values. For additional information see:


[Fields Override](https://docs.checkmarx.com/en/34965-68752-jira.html#fields-override)


##### Usage

```
./cx scan tags [flags]
```


##### Flags

**`--help, -h`**

Help for the tags command.


##### Examples

###### Using the tags command

```
C:\ast-cli_2.0.53_windows_x64>cx scan tags
{"demotag":[""],"main":[""],"team":["dev01","dev02","qa"]
```

#### scan workflow

The `workflow` command is used to **retrieve information about a scan workflow** in Checkmarx One.


##### Usage

```
./cx scan workflow --scan-id <scan id> [flags]
```


##### Flags

**`--scan-id <string>` Required**

Scan ID for which you would like to retrieve the workflow.

**`--format <string>` Default: table**

The output format for the response. Possible values are `json`, `list` or `table`.

**`---help, -h`**

Help for the show command.


##### Workflow Examples

<details>

<summary>Retrieve a list of scans</summary>

```
user@laptop:/AST$ ./cx scan list

Scan ID                              Project ID                           Status    Created at Tags Initiator Origin             
-------                              ----------                           ------    ---------- ---- --------- ------                   
a2f45c91-18ba-4d69-a748-972d0ecc1453 9f47d3d7-76f2-418b-9513-e3e02cc5cbb9 Completed 08-27-21   []   org_admin ASTCLI 2.0.0-rc.21
```

</details>

###### Retrieve scan workflow

```
./cx scan workflow --scan-id <scan id>
```

Sample command:

```
user@laptop:/AST$ ./cx.exe scan workflow --scan-id a2f45c91-18ba-4d69-a748-972d0ecc1453 --format table
```

Sample response:

```
Source                         Timestamp                      Info                                                   
------                         ---------                      ----                                                   
scans                          2021-08-27T14:15:46.843323175Z Scan created                                           
scans                          2021-08-27T14:15:46.996620259Z Scan Running                                           
fetch-sources-default          2021-08-27T14:15:47.068Z       fetch-sources-default started                          
fetch-sources-default          2021-08-27T14:15:47.082Z       fetch-sources-default in progress                      
fetch-sources-default          2021-08-27T14:15:48.061Z       fetch-sources-default ended                            
config-as-code-default         2021-08-27T14:15:48.101Z       config-as-code-default started                         
config-as-code-default         2021-08-27T14:15:48.304Z       config-as-code-default checkmarx config file not found 
config-as-code-default         2021-08-27T14:15:48.346Z       config-as-code-default ended                           
kics-runner-default            2021-08-27T14:15:48.415Z       kics-runner-default started                            
kics-runner-default            2021-08-27T14:15:48.425Z       kics-runner-default Start scan files download          
sca-runner-default             2021-08-27T14:15:48.429Z       sca-runner-default started                             
fetch-queries-default          2021-08-27T14:15:48.43Z        fetch-queries-default started                          
sca-runner-default             2021-08-27T14:15:48.449Z       sca-runner-default Start scan files download           
kics-runner-default            2021-08-27T14:15:48.583Z       kics-runner-default Finished scan files download       
kics-runner-default            2021-08-27T14:15:48.597Z       kics-runner-default Start scan execution               
sca-runner-default             2021-08-27T14:15:48.637Z       sca-runner-default Finished scan files download        
sca-runner-default             2021-08-27T14:15:48.671Z       sca-runner-default Start scan execution                
fetch-queries-default          2021-08-27T14:15:48.975Z       fetch-queries-default ended                            
sast-scan-inc-default          2021-08-27T14:15:49.014Z       sast-scan-inc-default started                          
sast-scan-inc-default          2021-08-27T14:15:49.262Z       sast-scan-inc-default ended                            
sast-rm-default                2021-08-27T14:15:49.307Z       sast-rm-default started                                
sast-results-inc-default       2021-08-27T14:15:49.307Z       sast-results-inc-default started                       
sast-rm-default                2021-08-27T14:15:49.406Z       sast-rm-default Queued in sast resource manager        
sast-results-inc-default       2021-08-27T14:15:49.443Z       sast-results-inc-default ended                         
kics-runner-default            2021-08-27T14:15:51.285Z       kics-runner-default Finished scan execution            
kics-runner-default            2021-08-27T14:15:51.297Z       kics-runner-default Start results publish              
kics-runner-default            2021-08-27T14:15:51.311Z       kics-runner-default Finished results publish           
kics-runner-default            2021-08-27T14:15:51.331Z       kics-runner-default Start engine log publish           
kics-runner-default            2021-08-27T14:15:51.368Z       kics-runner-default Finished engine log publish        
kics-runner-default            2021-08-27T14:15:51.413Z       kics-runner-default ended                              
collect-logs-default           2021-08-27T14:15:51.464Z       collect-logs-default started                           
kics-results-processor-default 2021-08-27T14:15:51.464Z       kics-results-processor-default started                 
collect-logs-default           2021-08-27T14:15:51.613Z       collect-logs-default ended                             
kics-results-processor-default 2021-08-27T14:15:52.306Z       kics-results-processor-default ended                   
sca-runner-default             2021-08-27T14:16:20.583Z       sca-runner-default Finished scan execution             
sca-runner-default             2021-08-27T14:16:20.596Z       sca-runner-default Start results publish               
sca-runner-default             2021-08-27T14:16:20.62Z        sca-runner-default Finished results publish            
sca-runner-default             2021-08-27T14:16:20.664Z       sca-runner-default ended                               
sca-packages-processor-default 2021-08-27T14:16:20.716Z       sca-packages-processor-default started                 
sca-results-processor-default  2021-08-27T14:16:20.717Z       sca-results-processor-default started                  
sca-packages-processor-default 2021-08-27T14:16:20.924Z       sca-packages-processor-default ended                   
sca-results-processor-default  2021-08-27T14:16:21.246Z       sca-results-processor-default ended                    
sast-rm-default                2021-08-27T14:16:21.833Z       sast-rm-default ended                                  
collect-logs-default           2021-08-27T14:16:21.882Z       collect-logs-default started                           
sast-results-events-default    2021-08-27T14:16:21.883Z       sast-results-events-default started                    
collect-logs-default           2021-08-27T14:16:22.068Z       collect-logs-default ended                             
sast-results-events-default    2021-08-27T14:16:24.982Z       sast-results-events-default ended                      
scans                          2021-08-27T14:16:25.056678542Z Scan Completed
```

#### scan logs

The `logs` command is used to retreive the application logs for a single scan type.


The optional scan types are:


- sast
- kics


##### Usage

```
./cx scan logs --scan-id <scan Id> --scan-type <scan type>
```


##### Flags

**`---help, -h`**

Help for the logs command.

**`--scan-id <string>`**

Scan ID to retrieve log for.

**`--scan-type <string>` Required**

Scan type to pull logs for.

Optional scan types: sast, iac-security


##### Workflow Examples

<details>

<summary>Retrieve a list of scans</summary>

```
user@laptop:~/ast-cli$ ./cx scan list

Scan ID                              Project ID                           Status    Created at Tags Initiator                                                        Origin                 
-------                              ----------                           ------    ---------- ---- ---------                                                        ------                 
f36b063a-84ca-4c4f-ad22-debacdd588aa d7b56888-8407-4e9b-ae5b-7fc43233a497 Completed 09-26-21   []   org_admin                                                        Chrome 93.0.4577.63    
7efdc589-c8e1-436b-8980-4a907839a5d0 2924669e-f021-4fca-8d18-6b9d00881c1a Completed 09-26-21   []                                                                    grpc-java-netty 1.35.0 
b9794f15-b5a1-4565-9156-cab11ab016df 2924669e-f021-4fca-8d18-6b9d00881c1a Completed 09-26-21   []                                                                    grpc-java-netty 1.35.0
```

</details>

###### Retrieve logs for SAST scanner

Sample command:

```
user@laptop:~/ast-cli$ ./cx scan logs --scan-id f36b063a-84ca-4c4f-ad22-debacdd588aa --scan-type sast
```

Sample response for sast scanner:

```
26/09/2021 13:05:42,602 [1] INFO  Available memory: 12347 Used memory: 56 Elapsed Time: 00:00:00.1241647 [Unspecified] -
Product version: 9.4.0.0-202107110128-Release
Used memory: 56Mb
OS: Unix 5.4.129.63
Current Directory: /app/Engine

Processor Count: 3
CLR Version: 3.1.18
Executable PID: 19
Executable Location: /usr/share/dotnet/dotnet
Process ID: 19
/ 96 GB Free
/proc 0 GB Free
/dev 0 GB Free
/dev/pts 0 GB Free
/sys 0 GB Free
/sys/fs/cgroup 7 GB Free
/sys/fs/cgroup/systemd 0 GB Free
/sys/fs/cgroup/freezer 0 GB Free
/sys/fs/cgroup/net_cls,net_prio 0 GB Free
/sys/fs/cgroup/memory 0 GB Free
/sys/fs/cgroup/perf_event 0 GB Free
/sys/fs/cgroup/devices 0 GB Free
/sys/fs/cgroup/cpu,cpuacct 0 GB Free
/sys/fs/cgroup/blkio 0 GB Free
/sys/fs/cgroup/hugetlb 0 GB Free
/sys/fs/cgroup/pids 0 GB Free
/sys/fs/cgroup/cpuset 0 GB Free
/dev/mqueue 0 GB Free
/etc/podinfo 7 GB Free
/dev/shm 0 GB Free
/run/secrets/kubernetes.io/serviceaccount 7 GB Free
/proc/bus 0 GB Free
/proc/fs 0 GB Free
/proc/irq 0 GB Free
/proc/sys 0 GB Free
/proc/acpi 7 GB Free
/sys/firmware 7 GB Free

Disk Speed: 526 Ticks per one request
New Disk Speed: 292 Ticks per one request
64Bit platform
PROCESSOR IDENTIFIER: Intel(R) Xeon(R) Platinum 8275CL CPU @ 3.00GHz
Core Speed: 3.6GHz
Product: Checkmarx SAST Engine
-       Main Version:
-       Hotfix Version:
-       Path:
Current Product dll's version list:
___________________________________
Assembly name:                 File version:
ASP.dll                        9.4.0.0-202107110125-Release
CSharp.dll                     9.4.0.0-202107110125-Release
DataCollections.dll            9.4.0.0-202107110128-Release
EngineFacade.dll               9.4.0.0-202107110128-Release
Flowgraphs.dll                 9.4.0.0-202107110128-Release
Plugin.dll                     9.4.0.0-202107110125-Release
Query.dll                      9.4.0.0-202107110128-Release
CxWrm.dll                      9.4.0.0-202107110128-Release
====================================================


26/09/2021 13:05:42,628 [1] INFO  Available memory: 12265 Used memory: 127 Elapsed Time: 00:00:01.7149099 [Unspecified] - Initializing scan input
26/09/2021 13:05:42,645 [1] INFO  Available memory: 12265 Used memory: 128 Elapsed Time: 00:00:01.7321179 [Startup] - Current Engine Configuration from DefaultConfig.xml:
_____________________________
IMPORTANT_FILE_ONLY_SCAN*=true
SMALL_PROJECT_BORDER*=3000000
```

###### Retrieving logs for KICS scanner

Sample command:

```
user@laptop:~/ast-cli$ ./cx scan logs --scan-id f36b063a-84ca-4c4f-ad22-debacdd588aa --scan-type kics
```

Sample response for KICS scanner

```
1:03PM | DEBUG | console.scan()
1:03PM | INFO  | Scanning with Keeping Infrastructure as Code Secure v1.3.3
1:03PM | DEBUG | Looking for queries in executable path and in current work directory
1:03PM | DEBUG | helpers.GetDefaultQueryPath()
1:03PM | DEBUG | helpers.GetExecutableDirectory()
1:03PM | DEBUG | Queries found in /app/kics-deployment/assets/queries
1:03PM | INFO  | Loading queries of type: dockerfile, ansible
1:03PM | DEBUG | source.NewFilesystemSource()
1:03PM | DEBUG | storage.NewMemoryStorage()
1:03PM | DEBUG | engine.NewInspector()
1:03PM | INFO  | Inspector initialized, number of queries=289
1:03PM | INFO  | Query execution timeout=1m0s
1:03PM | DEBUG | provider.NewFileSystemSourceProvider()
1:03PM | DEBUG | parser.NewBuilder()
1:03PM | DEBUG | resolver.Add()
1:03PM | DEBUG | resolver.Build()
1:03PM | DEBUG | service.StartScan()
1:03PM | DEBUG | service.StartScan()
1:03PM | DEBUG | engine.Inspect()
1:03PM | DEBUG | engine.Inspect()
1:03PM | DEBUG | model.CreateSummary()
1:03PM | DEBUG | console.resolveOutputs()
1:03PM | DEBUG | helpers.PrintResult()
1:03PM | INFO  | Files scanned: 4
1:03PM | INFO  | Parsed files: 4
1:03PM | INFO  | Queries loaded: 289
1:03PM | INFO  | Queries failed to execute: 0
1:03PM | INFO  | Inspector stopped
1:03PM | DEBUG | console.printOutput()
1:03PM | DEBUG | Output formats provided [json]
1:03PM | DEBUG | helpers.ValidateReportFormats()
1:03PM | DEBUG | helpers.GenerateReport()
1:03PM | INFO  | Results saved to file /tmp/953972639/results.json fileName:results.json
1:03PM | INFO  | Scan duration: 3318ms
```

#### sca-realtime

The `scan sca-realtime` command is used to **create and run a new sca scan** on the contents of a folder. The SCA realtime scan is a free feature which does not require a Checkmarx account. Anyone can download the CLI tool and run this command without need for authentication. The results are returned in the response body as a JSON object.


{% hint style="warning" %}
Even for users with a Checkmarx account, the realtime scan results are not synced with the user's Checkmarx account.
{% endhint %}


For info about which languages and package managers are supported for the SCA scanner, see [SCA Scanner - Supported Languages and Package Managers](https://docs.checkmarx.com/en/34965-130976-sca-scanner---supported-languages-and-package-managers.html).


{% hint style="warning" %}
In order for this tool to be effective, you need to install all relevant package managers on your local environment, see [Installing Supported Package Managers for Resolver](https://docs.checkmarx.com/en/34965-19198-installing-supported-package-managers-for-resolver.html).
{% endhint %}


##### Usage

```
./cx scan sca-realtime [flags]
```


##### Flags

**`--project-dir <string>, -p <string>` Required**

Path to the project folder on which the SCA scan will run.

{% hint style="warning" %}
This must point to a regular project folder and NOT a zip archive.
{% endhint %}


##### Examples

**Scanning a folder - Sample command**

```
./cx scan sca-realtime --project-dir C:\goatlin
```

<details>

<summary>Sample response</summary>

```
{
  "results": [
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "This affects the package mpath before 0.8.4. A type confusion vulnerability can lead to a bypass of CVE-2018-16490. In particular, the condition ignoreProperties.indexOf(parts[i]) !== -1 returns -1 if parts[i] is ['__proto__']. This is because the method that has been called if the input is an array is Array.prototype.indexOf() and not String.prototype.indexOf(). They behave differently depending on the type of the input.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Advisory",
            "url": "https://github.com/advisories/GHSA-p92x-r36w-9395"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/aheckmann/mpath/pull/13"
          }
        ],
        "packageIdentifier": "mpath",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/CVE-2021-23438",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "CVE-2021-23438",
        "cvssScore": 9.800000190734863,
        "cveName": "CVE-2021-23438",
        "cvss": {
          "version": 4,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "HIGH",
          "attackComplexity": "LOW",
          "integrityImpact": "HIGH",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "MEDIUM",
      "description": "lib/utils.js in mquery before 3.2.3 allows a pollution attack because a special property (e.g., __proto__) can be copied during a merge or clone operation.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Advisory",
            "url": "https://github.com/advisories/GHSA-45q2-34rf-mr94"
          }
        ],
        "packageIdentifier": "mquery",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/CVE-2020-35149",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "CVE-2020-35149",
        "cvssScore": 5.300000190734863,
        "cveName": "CVE-2020-35149",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "NONE",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "LOW",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "MEDIUM",
      "description": "The mergeClone function in the node.js mquery package before 3.2.5 is vulnerable to prototype pollution.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Disclosure",
            "url": "https://www.huntr.dev/bounties/1-npm-mquery"
          }
        ],
        "packageIdentifier": "mquery",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cxc8ffd605-ddff",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cxc8ffd605-ddff",
        "cvssScore": 5.300000190734863,
        "cveName": "Cxc8ffd605-ddff",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "NONE",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "LOW",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Disputed",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "MEDIUM",
      "description": "The package `body-parser` is vulnerable to prototype pollution, as it does no sanitation to the values received via the incoming JSON data. A remote attacker can inject a `__proto__` object to the application, which would successfully be parsed on the server side. This affects the integrity of the application.\n\n",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Other",
            "url": "https://gist.github.com/rgrove/3ea9421b3912235e978f55e291f19d5d/revisions"
          },
          {
            "type": "Issue",
            "url": "https://github.com/expressjs/body-parser/issues/347"
          }
        ],
        "packageIdentifier": "body-parser",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx14b19a02-387a",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx14b19a02-387a",
        "cvssScore": 6.5,
        "cveName": "Cx14b19a02-387a",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "LOW",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "LOW",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "LOW",
      "description": "The package `bluebird` is vulnerable to memory leak, when running the function longStackTraces() with the flag `--expose_gc`. This causes a significant increase in the memory usage, affecting the server's availability.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/petkaantonov/bluebird/issues/1080"
          }
        ],
        "packageIdentifier": "bluebird",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cxda14f253-4e52",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cxda14f253-4e52",
        "cvssScore": 3.700000047683716,
        "cveName": "Cxda14f253-4e52",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "LOW",
          "confidentiality": "NONE",
          "attackComplexity": "HIGH",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "Mongoose before 5.12.2 is vulnerable to prototype pollution.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/Automattic/mongoose/issues/10035"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/Automattic/mongoose/pull/10053"
          }
        ],
        "packageIdentifier": "mongoose",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cxba0aa4f8-fd76",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cxba0aa4f8-fd76",
        "cvssScore": 7.5,
        "cveName": "Cxba0aa4f8-fd76",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "NONE",
          "confidentiality": "HIGH",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "Mongoose is a MongoDB object modeling tool designed to work in an asynchronous environment. Mongoose versions prior to 6.4.6 are vulnerable to Prototype Pollution. The \"Schema.path()\" and \"Schema.add()\" function is vulnerable to prototype pollution when setting the schema object. This vulnerability allows modification of the Object prototype and could be manipulated into a Denial of Service (DoS) attack.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Advisory",
            "url": "https://github.com/advisories/GHSA-f825-f98c-gj3g"
          },
          {
            "type": "Disclosure",
            "url": "https://huntr.dev/bounties/055be524-9296-4b2f-b68d-6d5b810d1ddd"
          },
          {
            "type": "Issue",
            "url": "https://github.com/Automattic/mongoose/issues/12085"
          },
          {
            "type": "Release Note",
            "url": "https://github.com/Automattic/mongoose/releases/tag/6.4.6"
          }
        ],
        "packageIdentifier": "mongoose",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/CVE-2022-2564",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "CVE-2022-2564",
        "cvssScore": 9.800000190734863,
        "cveName": "CVE-2022-2564",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "HIGH",
          "attackComplexity": "LOW",
          "integrityImpact": "HIGH",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "The qs package as used in Express through 4.17.3 and other products, allows attackers to cause a Node process hang for an Express application because an \"__ proto__ key\" can be used. In many typical Express use cases, an unauthenticated remote attacker can place the attack payload in the query string of the URL that is used to visit the application, such as \"a[__proto__]=b&a[__proto__]&a[length]=100000000\". This vulnerability affects qs versions through 6.2.3, 6.3.0 through 6.3.2, 6.4.0, 6.5.0 through 6.5.2, 6.6.0, 6.7.0 through 6.7.2, 6.8.0 through 6.8.2, 6.9.0 through 6.9.6 and 6.10.0 through 6.10.2  (and therefore Express 4.17.3, which has \"deps: qs@6.9.7\" in its release description, is not vulnerable).",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Advisory",
            "url": "https://github.com/advisories/GHSA-hrpp-h998-j3pp"
          },
          {
            "type": "Disclosure",
            "url": "https://github.com/n8tz/CVE-2022-24999"
          },
          {
            "type": "Release Note",
            "url": "https://github.com/expressjs/express/releases/tag/4.17.3"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/ljharb/qs/pull/428"
          }
        ],
        "packageIdentifier": "qs",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/CVE-2022-24999",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "CVE-2022-24999",
        "cvssScore": 7.5,
        "cveName": "CVE-2022-24999",
        "cvss": {
          "version": 1,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "In NPM `debug`, the `enable` function accepts a regular expression from user input without escaping it. Arbitrary regular expressions could be injected to cause a Denial of Service attack on the user's browser, otherwise known as a ReDoS (Regular Expression Denial of Service). This is a different issue than CVE-2017-16137.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/debug-js/debug/issues/737"
          },
          {
            "comment": "Roadmap that mentions issue",
            "type": "Other",
            "url": "https://github.com/debug-js/debug/issues/656"
          },
          {
            "type": "POC/Exploit",
            "url": "https://github.com/brunodays/POCs/blob/master/debug/POC.md"
          }
        ],
        "packageIdentifier": "debug",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx8bc4df28-fcf5",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx8bc4df28-fcf5",
        "cvssScore": 7.5,
        "cveName": "Cx8bc4df28-fcf5",
        "cvss": {
          "version": 4,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "MEDIUM",
      "description": "The package debug is vulnerable to memory leakage when instance is created inside a function. The function `debug` in the file `common.js` does not free up used memory unless there's a call to `destroy()` function. This affects the availability.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/visionmedia/debug/issues/678"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/visionmedia/debug/pull/740"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/visionmedia/debug/pull/699"
          }
        ],
        "packageIdentifier": "debug",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx65603961-769c",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx65603961-769c",
        "cvssScore": 5.300000190734863,
        "cveName": "Cx65603961-769c",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "LOW",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "NPM `debug` prior to 4.3.0 has a Memory Leak when creating `debug` instances inside a function which can have a significant impact in the Availability. This happens since the function `debug` in the file `src/common.js` does not free up used memory.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/visionmedia/debug/issues/678"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/visionmedia/debug/pull/740"
          },
          {
            "type": "POC/Exploit",
            "url": "https://github.com/MarioTeixeiraCx/POCs/blob/main/POC.md"
          }
        ],
        "packageIdentifier": "debug",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx89601373-08db",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx89601373-08db",
        "cvssScore": 7.5,
        "cveName": "Cx89601373-08db",
        "cvss": {
          "version": 3,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "In NPM `debug`, the `enable` function accepts a regular expression from user input without escaping it. Arbitrary regular expressions could be injected to cause a Denial of Service attack on the user's browser, otherwise known as a ReDoS (Regular Expression Denial of Service). This is a different issue than CVE-2017-16137.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/debug-js/debug/issues/737"
          },
          {
            "comment": "Roadmap that mentions issue",
            "type": "Other",
            "url": "https://github.com/debug-js/debug/issues/656"
          },
          {
            "type": "POC/Exploit",
            "url": "https://github.com/brunodays/POCs/blob/master/debug/POC.md"
          }
        ],
        "packageIdentifier": "debug",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx8bc4df28-fcf5",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx8bc4df28-fcf5",
        "cvssScore": 7.5,
        "cveName": "Cx8bc4df28-fcf5",
        "cvss": {
          "version": 4,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "MEDIUM",
      "description": "The package debug is vulnerable to memory leakage when instance is created inside a function. The function `debug` in the file `common.js` does not free up used memory unless there's a call to `destroy()` function. This affects the availability.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/visionmedia/debug/issues/678"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/visionmedia/debug/pull/740"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/visionmedia/debug/pull/699"
          }
        ],
        "packageIdentifier": "debug",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx65603961-769c",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx65603961-769c",
        "cvssScore": 5.300000190734863,
        "cveName": "Cx65603961-769c",
        "cvss": {
          "version": 2,
          "attackVector": "NETWORK",
          "availability": "LOW",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    },
    {
      "type": "Regular",
      "scaType": "vulnerability",
      "label": "sca",
      "severity": "HIGH",
      "description": "NPM `debug` prior to 4.3.0 has a Memory Leak when creating `debug` instances inside a function which can have a significant impact in the Availability. This happens since the function `debug` in the file `src/common.js` does not free up used memory.",
      "data": {
        "nodes": [
          {
            "line": 0,
            "column": 0,
            "fileName": "packages\\services\\api\\package.json"
          }
        ],
        "packageData": [
          {
            "type": "Issue",
            "url": "https://github.com/visionmedia/debug/issues/678"
          },
          {
            "type": "Pull request",
            "url": "https://github.com/visionmedia/debug/pull/740"
          },
          {
            "type": "POC/Exploit",
            "url": "https://github.com/MarioTeixeiraCx/POCs/blob/main/POC.md"
          }
        ],
        "packageIdentifier": "debug",
        "scaPackageData": {
          "fixLink": "https://devhub.checkmarx.com/cve-details/Cx89601373-08db",
          "supportsQuickFix": false,
          "isDirectDependency": false,
          "typeOfDependency": ""
        }
      },
      "comments": {},
      "vulnerabilityDetails": {
        "cweId": "Cx89601373-08db",
        "cvssScore": 7.5,
        "cveName": "Cx89601373-08db",
        "cvss": {
          "version": 3,
          "attackVector": "NETWORK",
          "availability": "HIGH",
          "confidentiality": "NONE",
          "attackComplexity": "LOW",
          "integrityImpact": "NONE",
          "scope": "UNCHANGED",
          "privilegesRequired": "NONE",
          "userInteraction": "NONE"
        }
      }
    }
  ],
  "totalCount": 14,
  "scanID": ""
}
```

</details>

#### kics-realtime

The `scan kics-realtime` command is used to **create and run a new IaC Security (KICS) scan** locally using a container. The SCA realtime scan is a free feature which does not require a Checkmarx account. Anyone can download the CLI tool and run this command without need for authentication. The results are returned in the response body as a JSON object.


{% hint style="warning" %}
Even for users with a Checkmarx account, the realtime scan results are not synced with the user's Checkmarx account.
{% endhint %}


##### Usage

```
./cx scan kics-realtime [flags]
```


##### Prerequisites

You must have a supported container engine (Docker or Podman) installed and running in your environment.


##### Supported scan files extensions / technologies

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

<summary>Scan files extension / files list</summary>

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


##### Additional Parameters

**--additional-params** flag provides the ability to send additional scan options supported by KICS. Should follow comma separated format.

{% hint style="info" %}
More information about the additional scan options/flags supported by KICS in their official documentation

[https://docs.kics.io/latest/commands/](https://docs.kics.io/latest/commands/)
{% endhint %}

{% hint style="warning" %}
The report format and output path cannot be overridden, even by explicitly setting those flags in the `additional-params`.
{% endhint %}


##### Flags

**`--file <string>` Required**

Path to input file.

**`--engine <string>` Default: docker**

Name for the container engine to run KICS.

**`--additional-params <string>,<string>`**

Comma separated additional scan options supported by KICS. See [https://docs.kics.io/latest/commands/](https://docs.kics.io/latest/commands/)


##### Examples

###### Scanning a file

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

###### Scanning a file with a specific engine

```
./cx scan kics-realtime --file <FILE PATH> --engine <ENGINE NAME>
```

**Sample command**

```
C:\ast-cli_2.0.53_windows_x64>cx scan kics-realtime --file .\juice-shop-master\test\smoke\Dockerfile --engine podman
```

###### Scanning a file with additional parameters

```
./cx scan kics-realtime --file <FILE PATH> --additional-params <KICS_COMMANDS>
```

**Sample command**

```
C:\ast-cli_2.0.53_windows_x64>cx scan kics-realtime --file .\juice-shop-master\test\smoke\Dockerfile --additional-params -v, --exclude-results,fec62a97d569662093dbb9739360942f
```

###### Scanning a file in debug mode

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

## triage

The `triage` command is used for managing **risks** in Checkmarx One.


For more information about triaging results in Checkmarx One, see Managing (Triaging) Vulnerabilities.


### Usage

```
./cx triage [command] [flags]
```

### Triage Commands

`triage` can be used with the following commands:

#### triage update

The **triage update** command is used to **triage the results** in Checkmarx One.


##### Usage

```
./cx triage update [flags]
```


##### Flags

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


##### Examples

###### Update result

```
./cx triage update --scan-type <scan-type> --project-id <project-id> --similarity-id <similarity-id> --state <state> --severity <severity>
```

```
user@laptop:~/ast-cli$ ./cx triage update --scan-type "sast" --project-id "885ca4ad-5926-4177-b51c-fa1d11248d84" --similarity-id "549106280"  --state "confirmed" --severity "low"
Predicate updated successfully.
```

#### triage show

The **triage show** command is used to retrieve a list of all changes made to the predicate of a specific risk instance.


##### Usage

```
./cx triage show [flags]
```


##### Flags

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


##### Examples

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

#### triage get-states

The **triage get-states** command retrieves the available triage states for a given scan type, including custom states.


{% hint style="info" %}
Custom states is only available for accounts that have Phase 1 of the new Access Management.
{% endhint %}


##### Usage

```
./cx triage get-states [flags]
```


##### Flags

**`--all`**

Show all custom states, including the ones that have been deleted.

**`--help`**

Help for the triage get-states command.


##### Examples

Sample command:

```
user@laptop:~/ast-cli$ ./cx triage get-states
```

Sample response:

```
[{"id":13651,"name":"custom-state-4269583488125138725","type":"INFO"},{"id":13684,"name":"custom-state-7065983805428327353","type":"INFO"},{"id":13717,"name":"custom-state-8841123802087642575","type":"INFO"},{"id":13752,"name":"custom-state-271808954341294024","type":"INFO"},{"id":13785,"name":"custom-state-4318314140970845122","type":"INFO"},{"id":13821,"name":"custom-state-5130643464138548710","type":"INFO"},{"id":13718,"name":"custom-state-2286071310219315628","type":"INFO"},{"id":13786,"name":"custom-state-8692272966226908953","type":"INFO"},{"id":13822,"name":"custom-state-1072205568533198574","type":"INFO"},{"id":14094,"name":"dsfd","type":"INFO"},{"id":13719,"name":"custom-state-296535314730089576","type":"INFO"},{"id":13925,"name":"sdjb","type":"INFO"},{"id":13788,"name":"daniel","type":"INFO"},{"id":13926,"name":"aa","type":"INFO"},{"id":-1,"name":"TO_VERIFY","type":""},{"id":-1,"name":"NOT_EXPLOITABLE","type":""},{"id":-1,"name":"PROPOSED_NOT_EXPLOITABLE","type":""},{"id":-1,"name":"CONFIRMED","type":""},{"id":-1,"name":"URGENT","type":""}]
```

## utils

The `utils` command is used for performing various **Checkmarx One utility functions**.


### Usage

```
./cx utils [command]
```


### Help

**`---help, -h`**

Help for the health-check command.

### Utils Commands

`utils` can be used with the following commands:

#### completion

The `completion` command is used for performing **CLI command auto completion.**


The auto completion supports 4 command line types: bash, zsh, fish, and powershell.


{% hint style="info" %}
Auto completion is enabled only for the **current session**. Once the session is closed you need to configure it again.
{% endhint %}


##### Usage

```
./cx utils completion --shell [bash|zsh|fish|powershell]
```


##### Flags

**`--shell, -s` Required**

The type of shell [bash/zsh/fish/powershell]

**`---help, -h`**

Help for the health-check command.


##### Examples

###### Bash Auto Completion

###### Linux

To configure auto completions for each session, execute the following:

```
# load and export a set of Environment Variables for the completion command:
$ source <(./cx utils completion -s bash)
```

```
# Load completion for each Linux session:
$ ./cx utils completion -s bash > /etc/bash_completion.d/cx
```

###### MAC

To configure auto completions for each session, execute the following:

```
# load and export a set of Environment Variables for the completion command:
$ source <(./cx utils completion -s bash)
```

```
# Load completion for each MAC session:
$ ./cx utils completion -s bash > /usr/local/etc/bash_completion.d/cx
```

###### zsh Auto Completion

To configure auto completions for each session, execute the following:

```
# Enable auto completion for the environment:
$ echo "autoload -U compinit; compinit" >> ~/.zshrc
```

```
# To load auto completion for each session, execute once:
$ ./cx utils completion -s zsh > "${fpath[1]}/_cx"
```

```
# start a new shell for this setup to take effect
```

###### fish Auto Completion

To configure auto completions for each session, execute the following:

```
# Configure auto completion:
$ ./cx utils completion -s fish | source
```

```
# To load auto completion for each session, execute once:
$ ./cx utils completion -s fish > ~/.config/fish/completions/cx.fish
```

###### PowerShell Auto Completion

```
# load and export a set of Environment Variables for the completion command:
$ PS> .\cx.exe utils completion -s powershell | Out-String | Invoke-Expression
```

```
# To load auto completion for each session, execute:
$ PS> .\cx.exe utils completion -s powershell > cx.ps1
```

```
# source this file from your PowerShell profile
```

#### env

The `env` command retrieves the configured environment variables.


##### Usage

```
./cx utils env [flags]
```


##### Flags

**`---help, -h`**

Help for the env command.


##### Examples

###### Using the env command

```
uaer@laptop:~/ast-cli$ ./cx utils env

Detected Environment Variables:

            cx_proxy_auth_type:
                  cx_client_id:
              cx_client_secret:
                     cx_apikey:
                     cx_branch:
                    cx_timeout:
                   cx_base_uri:
                     cx_tenant:
                    http_proxy:
                  sca_resolver:
              cx_base_auth_uri:
```

#### contributor-count

The `contributor-count` command enables users to count **unique contributors** from different **SCM** repositories, for the past **90 days**.


##### Usage

```
./cx utils contributor-count [command]
```


##### Flags

**`--help, -h`**

Help for the contributor-count command.


##### Global Flags

The `contributor-count` command does not support all global flags. The following flags are supported.

**`--proxy <string>`**

Proxy server to send communication through.

**`--proxy-auth-type <string>`**

Proxy authentication type (basic or ntlm).

**`--proxy-ntlm-domain <string>`**

Window domain when using NTLM proxy.

**`--timeout <string>` Default: 5 seconds**

Timeout for network activity.

**`--debug`**

Debug mode returns detailed logs, including the username of each of the contributors and the repos to which they contributed.

##### github

The `github` command retrieves the number of unique contributors for the provided GitHub repositories or organizations. Contributors are found by visiting all repositories and comparing the `author` property of each commit. Bots are counted as contributors if their commits do not have “type” as “Bot” (dependabot is correctly excluded).


The user's email is used as the unique identifier for counting distinct users. Contributors who commit from accounts with different emails will be counted as distinct contributors.


{% hint style="info" %}
This command returns a breakdown of unique contributors per repo as well as the total number of unique contributors. When a particular user contributes to several different repos, this is counted as a single contributor for the total count. Therefore, the total count will not necessarily be equal to the sum of the individual repos.
{% endhint %}


###### Usage

```
./cx utils contributor-count github [flags]
```


###### Flags

**`--format <string>` Default: table**

The output format for the response. Possible values are `json`, `list` or `table` (default).

**`--help, -h`**

Help for the github command.

**`--orgs <strings>`**

List of organizations to scan for contributors. Comma separated list.

**`--repos <strings>`**

List of repositories to scan for contributors. Comma separated list.

**`--token <string>`**

GitHub Personal Access Token (PAT). Requires “Repo” scope and organization SSO authorization, if enforced by the organization.

**`--url <string>`**

The API base URL. Default: https://api.github.com/


###### Examples

###### Using the github Command to Count an Organization

```
PS C:\Users\ast-cli> cx utils contributor-count github --orgs checkmarx --token <token>

Name                               UniqueContributors 
----                               ------------------ 
...
Checkmarx/ast-cli                  1                  
Checkmarx/kics                     2   
...      
Total unique contributors          N
```

###### Using the github command to count specific repositories

```
PS C:\Users\ast-cli> cx utils contributor-count github --repos ast-cli,kics --orgs checkmarx --token <token>

Name                               UniqueContributors 
----                               ------------------ 
Checkmarx/ast-cli                  1                  
Checkmarx/kics                     2         
Total unique contributors          3
```

##### azure

The `azure` command retrieves the number of unique contributors for the provided Azure DevOps repositories, projects, and organizations.


The user's email is used as the unique identifier for counting distinct users. Contributors who commit from accounts with different emails will be counted as distinct contributors.


{% hint style="info" %}
This command returns a breakdown of unique contributors per repo as well as the total number of unique contributors. When a particular user contributes to several different repos, this is counted as a single contributor for the total count. Therefore, the total count will not necessarily be equal to the sum of the individual repos.
{% endhint %}


###### Usage

```
./cx utils contributor-count azure [flags]
```


###### Flags

**`--help, -h`**

Help for the results command.

**`--orgs strings <string>`**

List of organizations to scan for contributors.

Comma separated list.

**`--projects <string>`**

List of projects to scan for contributors.

Comma separated list.

**`--repos <string>`**

List of repositories to scan for contributors.

Comma separated list.

**`--token <string>`**

Azure DevOps personal access token. Requires "Connected server" and "Code" scope.

**`--url-azure <string>` Default: [https://dev.azure.com/](https://dev.azure.com/)**

API base URL.

**`--format <string>` Default: table**

The output for the response. Possible values are `json`, `list` or `table`.


###### Examples

###### Using the azure Command to Count an Organization contributors

```
./cx utils contributor-count azure --orgs <orgs> --token <token>
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count azure --orgs Checkmarx --token 12345678910

Name                                      UniqueContributors 
----                                      ------------------ 
Checkmarx/public/ast-cli                  2
Checkmarx/private/ast-java-wrapper        1                    
...                                       ...
Total unique contributors                 7     

2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

```
./cx utils contributor-count azure --orgs <orgs> --token <token> --debug
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count azure --orgs Checkmarx --token 12345678910

Name                                      UniqueContributors 
----                                      ------------------ 
Checkmarx/public/ast-cli                  2
Checkmarx/private/ast-java-wrapper        1                    
...                                       ...
Total unique contributors                 7     

Name                                      UniqueContributorsUsername 
----                                      -------------------------- 
Checkmarx/public/ast-cli                  User Checkmarx
Checkmarx/private/ast-java-wrapper        UserCheckmarx                
...

2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

###### Using the azure Command to Count Projects contributors

```
./cx utils contributor-count azure --orgs <orgs> --projects <projects> --token <token>
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count azure --orgs Checkmarx --projects public --token 12345678910

Name                                      UniqueContributors 
----                                      ------------------ 
Checkmarx/public/ast-cli                  2                  
...                                       ...
Total unique contributors                 5     

2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

```
./cx utils contributor-count azure --orgs <orgs> --projects <projects> --token <token> --debug
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count azure --orgs Checkmarx --projects public --token 12345678910

Name                                      UniqueContributors 
----                                      ------------------ 
Checkmarx/public/ast-cli                  2                  
...                                       ...
Total unique contributors                 5     


Name                                      UniqueContributorsUsername 
----                                      -------------------------- 
Checkmarx/public/ast-cli                  User Checkmarx          
...

2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

###### Using the azure Command to Count Repositories contributors

```
./cx utils contributor-count azure --orgs <orgs> --projects <projects> --repos <repos> --token <token>
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count azure --orgs Checkmarx --projects public --repos asa-cli --token 12345678910

Name                                      UniqueContributors 
----                                      ------------------ 
Checkmarx/public/ast-cli                  2                  
Total unique contributors                 2     

2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

```
./cx utils contributor-count azure --orgs <orgs> --projects <projects> --repos <repos> --token <token> --debug
```

```
user@laptop:~/ast-cli$ ./cx utils contributor-count azure --orgs Checkmarx --projects public --repos ast-cli --token 12345678910

Name                                      UniqueContributors 
----                                      ------------------ 
Checkmarx/public/ast-cli                  2                                                    
Total unique contributors                 2     


Name                                      UniqueContributorsUsername 
----                                      -------------------------- 
Checkmarx/public/ast-cli                  User Checkmarx          


2022/03/18 10:30:46 Note: dependabot is not counted but other bots might be considered users.
```

##### gitlab

The `gitlab` command retrieves the number of unique contributors for the provided GitLab groups or projects.


{% hint style="info" %}
This command returns a breakdown of unique contributors per repo as well as the total number of unique contributors. When a particular user contributes to several different repos, this is counted as a single contributor for the total count. Therefore, the total count will not necessarily be equal to the sum of the individual repos.
{% endhint %}


###### Usage

```
.\cx.exe utils contributor-count gitlab [flags]
```


###### Flags

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


###### Examples

###### Using the gitlab Command to Count an Organization

```
C:\Users\ast-cli> .\cx.exe utils contributor-count gitlab --token <token> --groups Checkmarx-ts/cxlite

Name                               UniqueContributors 
----                               ------------------ 
...
Checkmarx/CxLite/CxDemo            1                  
...      
Total unique contributors          1
```

###### Using the gitlab Command to Count Specific Repositories

```
C:\Users\ast-cli>.\cx.exe utils contributor-count gitlab --token <token> --projects Checkmarx/CxLite/CxDemo

Name                               UniqueContributors 
----                               ------------------ 
Checkmarx/CxLite/CxDemo            1                           
Total unique contributors          1
```

##### bitbucket

The `bitbucket` command retrieves the number of unique contributors for the provided Bitbucket repositories, projects and organizations.


{% hint style="info" %}
This command returns a breakdown of unique contributors per repo as well as the total number of unique contributors. When a particular user contributes to several different repos, this is counted as a single contributor for the total count. Therefore, the total count will not necessarily be equal to the sum of the individual repos.
{% endhint %}


###### Usage

```
./cx utils contributor-count bitbucket [flags]
```


###### Flags

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


###### Examples

###### Using the bitbucket Command to Count Workspace Contributors

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

###### Using the bitbucket Command to Count Repositories Contributors

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

##### bitbucket-server

The `bitbucket-server` command retrieves the number of unique contributors for the provided Bitbucket Server repositories and projects.


{% hint style="info" %}
This command returns a breakdown of unique contributors per repo as well as the total number of unique contributors. When a particular user contributes to several different repos, this is counted as a single contributor for the total count. Therefore, the total count will not necessarily be equal to the sum of the individual repos.
{% endhint %}


###### Usage

```
./cx utils contributor-count bitbucket-server [flags]
```


###### Flags

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


###### Examples

###### Using the bitbucket-server Command to Count All Contributors

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

###### Using the bitbucket-server Command to Count Projects' Contributors

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

###### Using the bitbucket-server Command to Count Repositories' Contributors

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

#### learn-more

The `learn-more` command retrieves additional descriptions from the CLI for SAST vulnerabilities.


The command must be run with the attribute `query-id`, which can be retrieved from a scan’s results and passed to this command.


##### Usage

```
./cx utils learn-more --query-id <query-id> --format [json|table|list]
```


##### Flags

**`--query-id` Required**

The SAST query-id for a vulnerability.

**`--format` Default: list**

The output format for the response. Possible values are `json`, `list` or `table`.

**`---help, -h`**

Help for the learn-more command.


##### Examples

###### learn-more command

###### Default (without format flag)

```
./cx utils learn-more --query-id 5854466950125120303
QueryID                : 5854466950125120303
QueryName              : Open_Redirect
QueryDescriptionID     : Stored_Open_Redirect
ResultDescription      : The potentially tainted value provided by @SourceElement in @SourceFile at line @SourceLine is used as a desti
nation URL by @DestinationElement in @DestinationFile at line @DestinationLine, potentially allowing attackers to perform an open redirection.


Risk                   : An attacker could use social engineering to get a victim to click a link to the application, so that the user 
will be immediately redirected to another site of the attacker's choice. An attacker can then craft a destination website to fool the v
ictim; for example - they may craft a phishing website with an identical looking UI as the previous website's login page, and with a si
milar looking URL, convincing the user to submit their access credentials in the attacker's website. Another example would be a phishing website with an identical UI as that of a popular payment service, convincing the user to submit their payment information.


Cause                  : The application redirects the user’s browser to a URL provided by a tainted input, without first ensuring that
 URL leads to a trusted destination, and without warning users that they are being redirected outside of the current site. An attacker 
could use social engineering to get a victim to click a link to the application with a parameter defining another site to which the app
lication will redirect the user’s browser. Since the user may not be aware of the redirection, they may be under the misconception that the website they are currently browsing can be trusted.


GeneralRecommendations :
1.  Ideally, do not allow arbitrary URLs for redirection. Instead, create a mapping from user-provided parameter values to legitimate URLs.
2.  If it is necessary to allow arbitrary URLs:
    *   For URLs inside the application site, first filter and encode the user-provided parameter, and then either:
        *   Create a white-list of allowed URLs inside the application
        *   Use variables as a relative URL as an absolute one, by prefixing it with the application site domain - this will ensure all redirection will occur inside the domain
    *   For URLs outside the application (if necessary), either:
        *   White-list redirection to allowed external domains by first filtering URLs with trusted prefixes. Prefixes must be tested u
p to the third slash \[/\] - `scheme://my.trusted.domain.com/,` to prevent evasion. For example, if the third slash \[/\] is not valida
ted and scheme://my.trusted.domain.com is trusted, the URL scheme://my.trusted.domain.com.evildomain.com would be valid under this filter, but the domain actually being browsed is evildomain.com, not domain.com.
        *   For fully dynamic open redirection, use an intermediate disclaimer page to provide users with a clear warning that they are leaving the site.


Samples                : [{Java protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    String redirectUrl = request.getParameter("redirectUrl");
    if (redirectUrl != null) {
        response.sendRedirect(redirectUrl);
    } else {
          response.sendRedirect("/");
    }
} Java Servlet Vulnerable to Open Redirection} {Java protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    String redirectUrl = request.getParameter("redirectUrl");
    if (redirectUrl != null && redirectUrl.startsWith("https://www.trusteddomain.com/")) {
        response.sendRedirect(redirectUrl);
    } else {
          response.sendRedirect("/");
    }
} Whitelisting an Allowed External Domain, Preventing Open Redirection}]
```

###### Json format

```
./cx utils learn-more --query-id 5854466950125120303 --format json
[{"queryId":"5854466950125120303","queryName":"Open_Redirect","queryDescriptionId":"Stored_Open_Redirect","resultDescription":"The pote
ntially tainted value provided by @SourceElement in @SourceFile at line @SourceLine is used as a destination URL by @DestinationElement
 in @DestinationFile at line @DestinationLine, potentially allowing attackers to perform an open redirection.\n\n","risk":"An attacker 
could use social engineering to get a victim to click a link to the application, so that the user will be immediately redirected to ano
ther site of the attacker's choice. An attacker can then craft a destination website to fool the victim; for example - they may craft a
 phishing website with an identical looking UI as the previous website's login page, and with a similar looking URL, convincing the use
r to submit their access credentials in the attacker's website. Another example would be a phishing website with an identical UI as tha
t of a popular payment service, convincing the user to submit their payment information.\n\n","cause":"The application redirects the us
er’s browser to a URL provided by a tainted input, without first ensuring that URL leads to a trusted destination, and without warning 
users that they are being redirected outside of the current site. An attacker could use social engineering to get a victim to click a l
ink to the application with a parameter defining another site to which the application will redirect the user’s browser. Since the user
 may not be aware of the redirection, they may be under the misconception that the website they are currently browsing can be trusted.\
n\n","generalRecommendations":"\r\n1.  Ideally, do not allow arbitrary URLs for redirection. Instead, create a mapping from user-provid
ed parameter values to legitimate URLs.\r\n2.  If it is necessary to allow arbitrary URLs:\r\n    *   For URLs inside the application s
ite, first filter and encode the user-provided parameter, and then either:\r\n        *   Create a white-list of allowed URLs inside th
e application\r\n        *   Use variables as a relative URL as an absolute one, by prefixing it with the application site domain - thi
s will ensure all redirection will occur inside the domain\r\n    *   For URLs outside the application (if necessary), either:\r\n     
   *   White-list redirection to allowed external domains by first filtering URLs with trusted prefixes. Prefixes must be tested up to 
the third slash \\[/\\] - `scheme://my.trusted.domain.com/,` to prevent evasion. For example, if the third slash \\[/\\] is not validat
ed and scheme://my.trusted.domain.com is trusted, the URL scheme://my.trusted.domain.com.evildomain.com would be valid under this filte
r, but the domain actually being browsed is evildomain.com, not domain.com.\r\n        *   For fully dynamic open redirection, use an i
ntermediate disclaimer page to provide users with a clear warning that they are leaving the site.\r\n\n\n","samples":[{"progLanguage":"
Java","code":"protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {\n  
  String redirectUrl = request.getParameter(\"redirectUrl\");\n    if (redirectUrl != null) {\n        response.sendRedirect(redirectUr
l);\n    } else {\n          response.sendRedirect(\"/\");\n    }\n}","title":"Java Servlet Vulnerable to Open Redirection"},{"progLang
uage":"Java","code":"protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOExceptio
n {\n    String redirectUrl = request.getParameter(\"redirectUrl\");\n    if (redirectUrl != null \u0026\u0026 redirectUrl.startsWith(\
"https://www.trusteddomain.com/\")) {\n        response.sendRedirect(redirectUrl);\n    } else {\n          response.sendRedirect(\"/\");\n    }\n}","title":"Whitelisting an Allowed External Domain, Preventing Open Redirection"}]}]
```

#### remediation

The `remediation` command enables you to automatically **remediate** **vulnerabilities** for results that came from a specific **Checkmarx scanner**.


##### Usage

```
./cx utils remediation [command]
```


##### Flags

**`--help`**

Help for the utils remediation.

##### kics

The `kics` command enables you to automatically **remediate kics vulnerabilities**.


{% hint style="warning" %}
This feature is currently supported only for Terraform projects.
{% endhint %}


###### Usage

```
./cx utils remediation kics [flags]
```


###### Flags

**`--engine <string>` Default: docker**

Name in the $PATH for the container engine to run kics. Example: podman

**`--kics-files <string>` Required**

Absolute path to the folder that contains the file(s) to be remediated.

**`--results-file <string>` Required**

Path to the kics scan results file. This is used to identify and remediate the kics vulnerabilities.

**`--similarity-ids <string>,<string>` Default: Remediates all vulnerabilities**

Comma separated list of the similarity ids for the vulnerability instances that you would like to remediate.


###### Examples

###### Remediating all vulnerabilities

```
./cx utils remediation kics --results-file <PATH-TO-RESULTS> --kics-files <ABSOLUTE-PATH-TO-FILES>
```

```
user@laptop:/AST$ ./cx utils remediation kics --results-file "./results.json" --kics-files "/home/terraform_examples/"
{"available_remediation_count":3,"applied_remediation_count":3}
```

###### Remediating a specific vulnerability

```
./cx utils remediation kics --results-file <PATH-TO-RESULTS> --kics-files <ABSOLUTE-PATH-TO-FILES> --similarity-ids <SIMILARITY-ID-LIST>
```

```
user@laptop:/AST$ ./cx utils remediation kics --results-file "./results.json" --kics-files "/home/terraform_examples/" --similarity-ids b42a19486a8e18324a9b2c06147b1c49feb3ba39a0e4aeafec5665e60f98d047,40d17ca090c7f7e49e9a8005113dd1b22aac3fcf93add6a302baddfaf449fc03
{"available_remediation_count":3,"applied_remediation_count":1}
```

###### Remediating using a specific engine

```
./cx utils remediation kics --results-file <PATH-TO-RESULTS> --kics-files <ABSOLUTE-PATH-TO-FILES> --engine <ENGINE-NAME>
```

```
user@laptop:/AST$ ./cx utils remediation kics --results-file "./results.json" --kics-files "/home/terraform_examples/" --engine podman
{"available_remediation_count":3,"applied_remediation_count":3}
```

##### sca

The `sca` command is used to automatically **remediate sca vulnerabilities**.


###### Usage

```
./cx utils remediation sca [flags]
```

{% hint style="warning" %}
Currently only npm dependency files (package.json) are supported for this functionality.
{% endhint %}


###### Flags

**`--package-files <string>`**

Path to input package files to remediate the package version.

**`--package <string>`**

Name of the package to be replaced.

**`--package-version <string>`**

Version of the package to be replaced.


###### Examples

###### Remediating a specific package

```
././cx utils remediation sca --package-files <PACKAGE-FILE-PATHS> --package <PACKAGE-NAME> --package-version <PACKAGE-VERSION>
```

```
user@laptop:/AST$ ./cx utils remediation sca --package-files /home/package.json ,/home/src/package.json --package copyfiles --package-version 1.2.1
```

If you attempt to remediate a package that doesn't exist in your project, you will receive the following response:

```
Package copyfile not found
```

If you attempt to remediate a package of an unsupported type, you will receive the following response:

```
Unsupported package manager file
```

#### pr

The pr command decorates pull requests with results from Checkmarx One scans that were triggered by that pull request. The pull request comments show a list of new vulnerabilities that were introduced by the code changes as well a list of vulnerabilities that were fixed by the code changes. This feature is available for all supported SCMs, `github`, `gitlab`, `azure` and `bitbucket` (both Managed Setup and Custom Setup repos).


{% hint style="info" %}
For secured code repository environments, pr decorations can be sent via CxLink using the environment variable `CX_LINK_SERVER_HOST`.
{% endhint %}


![Image](UUID-fbf6cf15-2b6a-6e47-053b-e30b7eb269e9)


##### Usage

```
./cx utils pr [command]
```

##### github

The pr github command decorates pull requests in GitHub with results from Checkmarx One scans that were triggered by that pull request. The command must be submitted with a series of required attributes that specify the relevant repo and PR and provide the authentication credentials.


###### Usage

```
./cx utils pr github --scan-id <scan-id> --token <PAT> --namespace <organization> --repo-name <repository> --pr-number <pr number>
```


###### Flags

**`--scan-id` Required**

The scan ID of the Checkmarx One scan that was triggered by this PR. This can be extracted from the scan result that is obtained after the pull request is scanned.

**`--token` Required**

The GitHub OAuth token used for creating the decoration.

**`--namespace` Required**

SCM namespace for the repository.

**`--repo-name` Required**

SCM repository name.

**`--pr-number` Required**

The pull request number for decoration PR.

**`--code-repository-url` Required only for custom setup**

The URL of the custom setup instance.


###### Examples

###### pr github command

```
./cx.exe utils pr github --scan-id b8e043bc-4c72-4638-ac54-7ac1b40d1234 --namespace jay-nanduri --repo-name testGHAction --pr-number 1 --token <secret-token>
2022/08/31 12:31:43 PR comment created successfully.
```

##### gitlab

The pr gitlab command decorates pull requests in GitLab with results from Checkmarx One scans that were triggered by that pull request. The command must be submitted with a series of required attributes that specify the relevant repo and PR and provide the authentication credentials.


###### Usage

```
./cx utils pr gitlab --gitlab-project-id <project-id> --mr-iid <mr-id> --namespace <organization> --repo-name <repository> --scan-id <scan-id> --token <OAuth-token>
```


###### Flags

**`--gitlab-project-id` Required**

The ID of the project in GitLab.

**`--scan-id` Required**

The scan ID of the Checkmarx One scan that was triggered by this PR. This can be extracted from the scan result that is obtained after the pull request is scanned.

**`--token` Required**

The GitLab OAuth token used for creating the decoration.

**`--namespace` Required**

SCM organization name.

**`--repo-name` Required**

SCM repository name.

**`--mr-iid` Required**

The internal GitLab ID for the merge request.

**`--code-repository-url` Required only for custom setup**

The URL of the custom setup instance.


###### Examples

###### pr gitlab command

```
./cx.exe utils pr gitlab --gitlab-project-id 40227565 --mr-iid 19 --namespace tiagobcx --repo-name testProject --scan-id efc148f9-521d-4d60-8540-a36e98c2dd27 --token TOKEN
2023/11/15 09:30:00 gitlab PR comment created successfully.
```

##### azure

The pr azure command decorates pull requests in Azure DevOps with results from Checkmarx One scans that were triggered by that pull request. The command must be submitted with a series of required attributes that specify the relevant repo and PR and provide the authentication credentials.


###### Usage

```
./cx utils pr azure --scan-id <scan-id> --token <AAD> --namespace <organization> --project <project-name or project id> --pr-number <pr number> --code-repository-url <code-repository-url>
```


###### Flags

**`--scan-id` Required**

The scan ID of the Checkmarx One scan that was triggered by this PR. This can be extracted from the scan result that is obtained after the pull request is scanned.

**`--token` Required**

The Azure token used for creating the decoration.

**`--namespace` Required**

SCM namespace for the organization.

**`--project` Required**

The ID or name of the project in Azure.

**`--pr-number` Required**

The pull request number for decoration PR.

**`--code-repository-url` Required only for custom setup**

The URL of the custom setup instance.

**`--code-repository-username` Optional**

The username for the repo. This flag can only be used together with `--code-repository-url`.


###### Examples

###### pr azure command

```
./cx.exe utils pr azure --scan-id 91ff85b6-e067-45bd-83f2-c77b895651ed --namespace DefaultCollection --project DemoProject --pr-number 20 --code-repository-url http://ec2-54-160-203-63.compute-1.amazonaws.com/%22 --token TOKEN
```

##### bitbucket

The pr bitbucket command decorates pull requests in Bitbucket with results from Checkmarx One scans that were triggered by that pull request. The command must be submitted with a series of required attributes that specify the relevant repo and PR and provide the authentication credentials.


###### Usage

**Managed Setup**

```
./cx utils pr bitbucket --scan-id <scan-id> --token <PAT> --namespace <username> --repo-name <repository-slug> --pr-id <pr number>
```

**Custom Setup**

```
./cx utils pr bitbucket --scan-id <scan-id> --token <PAT> --code-repository-url <bitbucket-server-url> --project-key <project-key> --repo-name <repository-slug> --pr-id <pr number>
```


###### Flags

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


###### Examples

###### pr bitbucket command

```
/cx.exe utils pr bitbucket --scan-id 00f383f6-c618-4973-a576-938a64cee4b5 --token TOKEN --namespace elchananaarbiv --repo-name decoration1 --pr-id 20 --token TOKEN
```

#### tenant

The `tenant` command enables users to retrieve info about the global settings that apply to their tenant account (i.e., the info shown on the Account Settings screen in the web portal). For more information about settings, see [Global Account Settings](https://docs.checkmarx.com/en/34965-68598-global-account-settings.html).


##### Usage

```
./cx utils tenant [flags]
```


##### Flags

**`--format` Default: list**

The output format for the response. Possible values are `json`, `list` or `table`.

**`---help, -h`**

Help for the `tenant` command.


##### Examples

###### Sample Response

```
C:\ast-cli_2.0.53_windows_x64>cx utils tenant

Key   : scan.config.sca.filter
Value :

Key   : scan.config.sast.languageMode
Value :

Key   : scan.handler.git.repository
Value :

Key   : scan.config.kics.platforms
Value :

Key   : scan.config.sast.filter
Value : *.java

Key   : scan.handler.git.branch
Value :

Key   : scan.config.sca.ExploitablePath
Value :

Key   : scan.config.sast.defaultConfigId
Value :

Key   : scan.config.plugins.aiGuidedRemediation
Value :

Key   : scan.handler.git.token
Value :

Key   : scan.config.plugins.ideScans
Value : true

Key   : scan.config.apisec.swaggerFilter
Value :

Key   : scan.config.kics.filter
Value :

Key   : scan.config.sast.incremental
Value :

Key   : scan.config.sast.engineVerbose
Value :

Key   : scan.handler.git.sshKey
Value :

Key   : scan.config.sast.presetName
Value :

Key   : scan.config.sca.LastSastScanTime
Value :user@laptop:~/ast-cli$ ./cx utils tenant
Key   : scan.config.sast.defaultConfigId
Value :

Key   : scan.config.kics.filter
Value :

Key   : scan.config.sast.presetName
Value : ASA Premium

Key   : scan.handler.git.token
Value :

Key   : scan.config.sca.LastSastScanTime
Value :

Key   : scan.config.sast.filter
Value :

Key   : scan.handler.git.sshKey
Value :

Key   : scan.config.sca.filter
Value :

Key   : scan.config.sca.ExploitablePath
Value :

Key   : scan.handler.git.repository
Value :

Key   : scan.config.sast.engineVerbose
Value :

Key   : scan.handler.git.branch
Value :

Key   : scan.config.kics.platforms
Value :

Key   : scan.config.sast.languageMode
Value :

Key   : scan.config.sast.incremental
Value :

Key   : scan.config.plugins.ideScans
Value :
```

#### mask

The `mask` command enables users to return the secrets identified in an IaC file and show how they will be masked when the file is sent to ChatGPT using the `chat` command.


##### Usage

```
./cx utils mask [flags]
```


##### Flags

**`--reult-file` Required**

Specify the file path to the IaC file for which you would like to identify the secrets.

**`---help, -h`**

Help for the `mask` command.


##### Examples

```
PS C:\_repos\ast-cli> .\bin\cx.exe utils mask --result-file .\Dockerfile
{"maskedSecrets":[{"masked":"PASSWORD=\u003cmasked\u003e","secret":"PASSWORD=test","line":6}],"maskedFile":"FROM alpine:3.18.2\n\nRUN apk add --no-cache bash\nRUN adduser --system --disabled-password cxuser\nUSER cxuser\n\nPASSWORD=\u003cmasked\u003e\n\nCOPY cx /app/bin/cx\n\nENTRYPOINT [\"/app/bin/cx\"]\n"}
```

#### import

The `import` command is used to import vulnerability results that adhere to SARIF version 2.1.0 format from third-party security tools and services (i.e. the BYOR feature). These imported results are integrated into the Application Risk Management feature, providing organizations with a unified view of their application risk profile and enabling them to make informed decisions to secure their end-to-end application lifecycle.


The command is submitted with the `--project-name` attribute specifying the name of the Checkmarx One project that these results will be associated with. It is also submitted with the `--import-file-path` argument specifying the path to the import file.


##### Usage

```
./cx utils import --project-name "<project name>" --import-file-path <file path>
```


##### Flags

**--project-name**

The name of the Checkmarx One Project with which the results will be associated. This must be a Project that has already been created in Checkmarx One. It can be a dedicated Project created for the import or it can be a Project for which Checmarx One scans are run. In order to be able to access the imported results, the Project must be associated with a Checkmarx One Application.

**--import-file-path**

The path to the file with the sarif file. This can be a single SARIF file or a zip archive containing several SARIF files.

Make sure that the file conforms to the guidelines described in SARIF File - Specificationst and SARIF File - Limitations.

**`---help, -h`**

Help for the import command.


##### Examples

```
./cx utils import --project-name "importDemo" --import-file-path .
```

## version

The `version` command is used to retrieve the ** CLI version number**.


### Usage

```
./cx version [flags]
```


### Flags

**`--help, -h`**

Help for the version command.


### Examples

#### Retrieving the CLI version

```
C:\ast-cli_2.0.53_windows_x64>cx version
2.0.53
```
