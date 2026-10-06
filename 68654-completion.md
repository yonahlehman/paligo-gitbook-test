# completion

The `completion` command is used for performing **CLI command auto completion.**


The auto completion supports 4 command line types: bash, zsh, fish, and powershell.


{% hint style="info" %}
Auto completion is enabled only for the **current session**. Once the session is closed you need to configure it again.
{% endhint %}


## Usage
```
./cx utils completion --shell [bash|zsh|fish|powershell]
```


## Flags
**`--shell, -s` Required**

The type of shell [bash/zsh/fish/powershell]

**`---help, -h`**

Help for the health-check command.


## Examples
### Bash Auto Completion
### Linux
To configure auto completions for each session, execute the following:

```
# load and export a set of Environment Variables for the completion command:
$ source <(./cx utils completion -s bash)
```

```
# Load completion for each Linux session:
$ ./cx utils completion -s bash > /etc/bash_completion.d/cx
```

### MAC
To configure auto completions for each session, execute the following:

```
# load and export a set of Environment Variables for the completion command:
$ source <(./cx utils completion -s bash)
```

```
# Load completion for each MAC session:
$ ./cx utils completion -s bash > /usr/local/etc/bash_completion.d/cx
```

### zsh Auto Completion
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

### fish Auto Completion
To configure auto completions for each session, execute the following:

```
# Configure auto completion:
$ ./cx utils completion -s fish | source
```

```
# To load auto completion for each session, execute once:
$ ./cx utils completion -s fish > ~/.config/fish/completions/cx.fish
```

### PowerShell Auto Completion
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

