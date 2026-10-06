# auth login

The `auth login` command is used for authenticating with Checkmarx One.


Opens your default web browser and guides you through the Checkmarx One sign-in process, including multi-factor authentication (MFA). After you sign in, the CLI stores a refresh token, allowing future CLI commands to authenticate without requiring you to sign in again.


By default, the refresh token is stored in the CLI configuration file. Use the optional `--session` flag to instead store the token for the current shell (`local`) or in a dedicated file shared across shells (`global`).


Signing in automatically revokes any previously issued refresh token and replaces it with a new one.


{% hint style="info" %}
If `--tenant` or `--base-auth-uri` are not specified, the CLI uses the values stored in the current CLI configuration. Specify these options to authenticate against a different tenant or IAM environment.
{% endhint %}


## Usage
```
./cx auth login [flags]
```


## Flags
**`--help, -h`**

Help for the login command.

**`--no-browser`**

Prints the authorization URL instead of opening a browser

**`--port <int>`**

Local port for the OAuth callback listener (0 = pick a free port)

**`--session <string>`**

Controls how the refresh token is stored. If omitted, the CLI uses the default configuration file.

- `local` – Stores the refresh token in the `CX_APIKEY` environment variable for the current shell session only. In **PowerShell**, pipe the login and logout commands through `Invoke-Expression`; in **Bash** or **Zsh**, use `eval`. This executes the generated command that sets or clears the environment variable in the current shell.
- `global` – Stores the refresh token in a persistent location that is shared across shell sessions. Unlike local, no `Invoke-Expression` or `eval` wrapper is required.


## Examples
### Default Session
```
./cx auth login --tenant my-tenant
```

### Authenticating against a non-default environment
```
./cx auth login --tenant my-tenant --base-auth-uri <my-IAM-URL>
```

### Local session in PowerShell and Bash
```
Invoke-Expression (cx auth login --tenant my-tenant --session local)
```

```
eval "$(cx auth login --tenant my-tenant --session local)"
```

### Global Session
```
./cx auth login --tenant my-tenant --session global
```

