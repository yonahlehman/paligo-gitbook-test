# configure show

The `configure show` command is used for retreiving the **configuration properties** for the current profile.


## Usage
```
./cx configure show [flags]
```


## Flags
**`---help, -h`**

Help for the configure command.


## Examples
### Presenting all the Configuration Parameters Values
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

