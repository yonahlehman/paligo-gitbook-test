# project branches

The `branches` command **provides a list of all the available branches** in Checkmarx One.


## Usage
```
./cx project branches [flags]
```


## Flags
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


## Example
### Using the project branches command
```
ophir@OphirS-Laptop:~/ast-cli$ ./cx project branches --project-id 5a529813-62bc-4d56-89a0-11ffc37b3bc6
["dev","main"]
```

