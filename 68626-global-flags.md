# Global Flags

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

**Example 2:** `scan create --optional-flags="use-gitignore=true"` passes the `--use-gitignore` flag to the `scan create` command, excluding files and directories based on patterns defined in the directory's `.gitignore` file.

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


## Example
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

