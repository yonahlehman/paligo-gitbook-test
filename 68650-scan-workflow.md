# scan workflow

The `workflow` command is used to **retrieve information about a scan workflow** in Checkmarx One.


## Usage
```
./cx scan workflow --scan-id <scan id> [flags]
```


## Flags
**`--scan-id <string>` Required**

Scan ID for which you would like to retrieve the workflow.

**`--format <string>` Default: table**

The output format for the response. Possible values are `json`, `list` or `table`.

**`---help, -h`**

Help for the show command.


## Workflow Examples
<details>

<summary>Retrieve a list of scans</summary>

```
user@laptop:/AST$ ./cx scan list

Scan ID                              Project ID                           Status    Created at Tags Initiator Origin             
-------                              ----------                           ------    ---------- ---- --------- ------                   
a2f45c91-18ba-4d69-a748-972d0ecc1453 9f47d3d7-76f2-418b-9513-e3e02cc5cbb9 Completed 08-27-21   []   org_admin ASTCLI 2.0.0-rc.21
```

</details>

### Retrieve scan workflow
```
./cx scan workflow --scan-id <scan id>
```

Sample command:

```
user@laptop:/AST$ ./cx.exe scan workflow --scan-id a2f45c91-18ba-4d69-a748-972d0ecc1453 --format table
```

Sample response:

```
Source                         Timestamp                      Info                                                   
------                         ---------                      ----                                                   
scans                          2021-08-27T14:15:46.843323175Z Scan created                                           
scans                          2021-08-27T14:15:46.996620259Z Scan Running                                           
fetch-sources-default          2021-08-27T14:15:47.068Z       fetch-sources-default started                          
fetch-sources-default          2021-08-27T14:15:47.082Z       fetch-sources-default in progress                      
fetch-sources-default          2021-08-27T14:15:48.061Z       fetch-sources-default ended                            
config-as-code-default         2021-08-27T14:15:48.101Z       config-as-code-default started                         
config-as-code-default         2021-08-27T14:15:48.304Z       config-as-code-default checkmarx config file not found 
config-as-code-default         2021-08-27T14:15:48.346Z       config-as-code-default ended                           
kics-runner-default            2021-08-27T14:15:48.415Z       kics-runner-default started                            
kics-runner-default            2021-08-27T14:15:48.425Z       kics-runner-default Start scan files download          
sca-runner-default             2021-08-27T14:15:48.429Z       sca-runner-default started                             
fetch-queries-default          2021-08-27T14:15:48.43Z        fetch-queries-default started                          
sca-runner-default             2021-08-27T14:15:48.449Z       sca-runner-default Start scan files download           
kics-runner-default            2021-08-27T14:15:48.583Z       kics-runner-default Finished scan files download       
kics-runner-default            2021-08-27T14:15:48.597Z       kics-runner-default Start scan execution               
sca-runner-default             2021-08-27T14:15:48.637Z       sca-runner-default Finished scan files download        
sca-runner-default             2021-08-27T14:15:48.671Z       sca-runner-default Start scan execution                
fetch-queries-default          2021-08-27T14:15:48.975Z       fetch-queries-default ended                            
sast-scan-inc-default          2021-08-27T14:15:49.014Z       sast-scan-inc-default started                          
sast-scan-inc-default          2021-08-27T14:15:49.262Z       sast-scan-inc-default ended                            
sast-rm-default                2021-08-27T14:15:49.307Z       sast-rm-default started                                
sast-results-inc-default       2021-08-27T14:15:49.307Z       sast-results-inc-default started                       
sast-rm-default                2021-08-27T14:15:49.406Z       sast-rm-default Queued in sast resource manager        
sast-results-inc-default       2021-08-27T14:15:49.443Z       sast-results-inc-default ended                         
kics-runner-default            2021-08-27T14:15:51.285Z       kics-runner-default Finished scan execution            
kics-runner-default            2021-08-27T14:15:51.297Z       kics-runner-default Start results publish              
kics-runner-default            2021-08-27T14:15:51.311Z       kics-runner-default Finished results publish           
kics-runner-default            2021-08-27T14:15:51.331Z       kics-runner-default Start engine log publish           
kics-runner-default            2021-08-27T14:15:51.368Z       kics-runner-default Finished engine log publish        
kics-runner-default            2021-08-27T14:15:51.413Z       kics-runner-default ended                              
collect-logs-default           2021-08-27T14:15:51.464Z       collect-logs-default started                           
kics-results-processor-default 2021-08-27T14:15:51.464Z       kics-results-processor-default started                 
collect-logs-default           2021-08-27T14:15:51.613Z       collect-logs-default ended                             
kics-results-processor-default 2021-08-27T14:15:52.306Z       kics-results-processor-default ended                   
sca-runner-default             2021-08-27T14:16:20.583Z       sca-runner-default Finished scan execution             
sca-runner-default             2021-08-27T14:16:20.596Z       sca-runner-default Start results publish               
sca-runner-default             2021-08-27T14:16:20.62Z        sca-runner-default Finished results publish            
sca-runner-default             2021-08-27T14:16:20.664Z       sca-runner-default ended                               
sca-packages-processor-default 2021-08-27T14:16:20.716Z       sca-packages-processor-default started                 
sca-results-processor-default  2021-08-27T14:16:20.717Z       sca-results-processor-default started                  
sca-packages-processor-default 2021-08-27T14:16:20.924Z       sca-packages-processor-default ended                   
sca-results-processor-default  2021-08-27T14:16:21.246Z       sca-results-processor-default ended                    
sast-rm-default                2021-08-27T14:16:21.833Z       sast-rm-default ended                                  
collect-logs-default           2021-08-27T14:16:21.882Z       collect-logs-default started                           
sast-results-events-default    2021-08-27T14:16:21.883Z       sast-results-events-default started                    
collect-logs-default           2021-08-27T14:16:22.068Z       collect-logs-default ended                             
sast-results-events-default    2021-08-27T14:16:24.982Z       sast-results-events-default ended                      
scans                          2021-08-27T14:16:25.056678542Z Scan Completed
```

