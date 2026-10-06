# auth logout

The `auth logout` command signs you out of Checkmarx One by revoking the current refresh token and removing any locally stored authentication credentials.


The command automatically detects how you authenticated and cleans up the appropriate storage location. If you authenticated using `--session local`, run the command through `Invoke-Expression` (PowerShell) or `eval` (Bash/Zsh) to clear the CX_APIKEY environment variable in the current shell.


No `--session` option is required when logging out.


## Usage
```
./cx auth logout [flags]
```


## Flags
**`--help, -h`**

Help for the logout command.


## Examples
### Default logout
```
cx auth logout
```

### Local session (PowerShell)
```
Invoke-Expression (cx auth logout)
```

### Local session (Bash/Zsh
```
eval "$(cx auth logout)"
```

