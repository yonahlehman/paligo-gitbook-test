# configure set

The `configure set` command is used for setting configuration properties. For each parameter (property) that you would like to set, you need to specify the property name and the value that you would like to assign to that property.


## Usage
```
./cx configure set --prop-name <property name> --prop-value <property value>
```


## Flags
**`---help, -h`**

Help for the configure command.

**`--prop-name <string>`**

Name of property set.

**`--prop-value <string>`**

Value of property set.


## Properties
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


## Examples
### Setting the cx_base_uri Property
```
# Setting the Checkmarx One server URI
user@laptop:~/ast-cli$ ./cx configure set --prop-name cx_base_uri --prop-value https://eu.ast.checkmarx.net/
Setting property [ cx_base_uri ] to value [ https://eu.ast.checkmarx.net/ ]
```

