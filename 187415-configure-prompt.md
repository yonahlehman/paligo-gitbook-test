# configure (prompt)

The `configure` command initiates a series of prompts for configuring the CLI authentication credentials. The configurations are saved in a config file in the user's home directory under a subdirectory named ($HOME/.checkmarx).


{% hint style="info" %}
If you would like to set additional configuration parameters that are not related to authentication, then you need to use the `configure set` command.
{% endhint %}


## Required Parameters
The following parameters are required for authentication, depending on the method being used. When the CLI prompts for values that aren't required for your authentication method, you can just hit ENTER.

- cx_apikey

{% hint style="info" %}
The CLI automatically extracts all relevant account info (Base URL, Auth URL, Tenant name) from the API Key. You can use arguments to submit these values explicitly, overriding the extracted values. However, this is generally not recommended.
{% endhint %}

- cx_base_uri
- cx_base_auth_uri
- cx_tenant
- cx_client_id
- cx_client_secret


## CLI Authentication Parameters
The configure command prompts for the following authentication parameters

- AST Base URI - The base URL of your Checkmarx One environment.
   
   <details>
   
   <summary>Checkmarx One Server Base URLs</summary>
   
   - US Environment - https://ast.checkmarx.net
   - US2 Environment - https://us.ast.checkmarx.net
   - EU Environment - https://eu.ast.checkmarx.net
   - EU2 Environment - https://eu-2.ast.checkmarx.net
   - DEU Environment - https://deu.ast.checkmarx.net
   - Australia & New Zealand – https://anz.ast.checkmarx.net
   - India - https://ind.ast.checkmarx.net
   - India 2 - https://ind-2.ast.checkmarx.net/
   - Singapore - https://sng.ast.checkmarx.net
   - UAE - https://mea.ast.checkmarx.net
   - Israel - https://gov-il.ast.checkmarx.net
   
   </details>
- AST Base Auth URI - The base URI of the authentication server for you Checkmarx One environment.
   
   <details>
   
   <summary>Checkmarx One Authentication URLs</summary>
   
   - US Environment - https://iam.checkmarx.net
   - US2 Environment - https://us.iam.checkmarx.net
   - EU Environment - https://eu.iam.checkmarx.net
   - EU2 Environment - https://eu-2.iam.checkmarx.net
   - DEU Environment - https://deu.iam.checkmarx.net
   - Australia & New Zealand – https://anz.iam.checkmarx.net
   - India - https://ind.iam.checkmarx.net
   - Singapore - https://sng.iam.checkmarx.net
   - UAE - https://mea.iam.checkmarx.net
   - Israel - https://gov-il.iam.checkmarx.net
   
   </details>
- AST Tenant - The name of you Checkmarx One tenant account.
- Do you want to use API Key authentication? - Specify your authentication method. Y = API Key, N = OAuth client
- AST API Key - Your Checkmarx One API Key. See [Creating API Keys](https://docs.checkmarx.com/en/34965-188712-creating-api-keys.html)
- Checkmarx One Client ID - Your Checkmarx One OAuth client ID. See [Creating an OAuth Client](https://docs.checkmarx.com/en/34965-188033-creating-an-oauth-client-for-checkmarx-one-integrations.html)
- Client Secret - Your Checkmarx One OAuth secret.


## Usage Example
```
C:\ast-cli_2.0.55_windows_x64>cx configure
Setup guide: https://checkmarx.com/resource/documents/en/34965-68621-checkmarx-one-cli-quick-start-guide.html

AST Base URI [https://eu.ast.checkmarx.net/]: https://ast.checkmarx.net/
AST Base Auth URI (IAM) [https://eu.iam.checkmarx.net/]: https://iam.checkmarx.net/
AST Tenant [ast_integration_tenant_eu]: myTenant
Do you want to use API Key authentication? (Y/N): n
Checkmarx One Client ID []: myOAuthClient
Client Secret []: myOAuthSecretuser@laptop:/ast$ ./cx.exe configure
Setup guide: https://checkmarx.atlassian.net/wiki/x/mIKctw
```

