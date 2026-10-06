# hooks pre-commit

The **pre-commit** command is used to configure and run pre-commit secret detection scans.


For detailed information about usage and workflows, see [Pre-Commit Secret Scanning](https://docs.checkmarx.com/en/34965-364702-pre-commit-secret-scanning.html).


## Usage
```
./cx hooks pre-commit [sub-command][flags]
```


## sub-commands
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


## Flags
**`--all`**

Used with `secrets-ignore` sub-command to ignore all detected secrets.

**`--global`**

For global installation of hooks, add this flag to all sub-commands for installing, uninstalling or updating the hooks.

**`--resultIds <string>`**

Used with `secrets-ignore` sub-command to ignore specific secrets. Submit a comma separated list of result IDs of the secretst that will be ignored.

**`--help`**

Help for the hook commands.


## Examples
### Install locally
```
./cx hooks pre-commit secrets-install-git-hook
Installing local pre-commit hooks...
pre-commit installed at .git\hooks\pre-committriage show --scan-type <scan-type> --project-id <project-id> --similarity-id <similarity-id>
```

### Install Globally
```
./cx hooks pre-commit secrets-install-git-hook --global
Installing global pre-commit hook...
Global pre-commit hook installed successfully.
```

### Commit File With Secrets
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

