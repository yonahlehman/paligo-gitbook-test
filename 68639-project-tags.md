# project tags

The `tags` command **provides a list of all the available tags** in your tenant.


Tags are also used for overriding **Jira feedback apps** fields values. For additional information see:


[Fields Override](https://docs.checkmarx.com/en/34965-68752-jira.html#fields-override)


## Usage
```
./cx project tags [flags]
```


## Flags
**`---help, -h`**

Help for the tags command.


## Examples
### Using the tags Command
```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project tags
{"Demo":[""],"QA":["Automation","Manual"],"test":[""]}{"insecure-bank":[""],"insecure-bank-app":[""],"rwwr":[""],"wrwr":[""]}
```

