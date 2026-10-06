# scan tags

The `tags` command is used to **provide a list of all the available tags** in Checkmarx One.


Tags can be used for overriding **Jira feedback app** fields values. For additional information see:


[Fields Override](https://docs.checkmarx.com/en/34965-68752-jira.html#fields-override)


## Usage
```
./cx scan tags [flags]
```


## Flags
**`--help, -h`**

Help for the tags command.


## Examples
### Using the tags command
```
C:\ast-cli_2.0.53_windows_x64>cx scan tags
{"demotag":[""],"main":[""],"team":["dev01","dev02","qa"]
```

