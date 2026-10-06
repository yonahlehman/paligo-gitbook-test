# scan logs

The `logs` command is used to retreive the application logs for a single scan type.


The optional scan types are:


- sast
- kics


## Usage
```
./cx scan logs --scan-id <scan Id> --scan-type <scan type>
```


## Flags
**`---help, -h`**

Help for the logs command.

**`--scan-id <string>`**

Scan ID to retrieve log for.

**`--scan-type <string>` Required**

Scan type to pull logs for.

Optional scan types: sast, iac-security


## Workflow Examples
<details>

<summary>Retrieve a list of scans</summary>

```
user@laptop:~/ast-cli$ ./cx scan list

Scan ID                              Project ID                           Status    Created at Tags Initiator                                                        Origin                 
-------                              ----------                           ------    ---------- ---- ---------                                                        ------                 
f36b063a-84ca-4c4f-ad22-debacdd588aa d7b56888-8407-4e9b-ae5b-7fc43233a497 Completed 09-26-21   []   org_admin                                                        Chrome 93.0.4577.63    
7efdc589-c8e1-436b-8980-4a907839a5d0 2924669e-f021-4fca-8d18-6b9d00881c1a Completed 09-26-21   []                                                                    grpc-java-netty 1.35.0 
b9794f15-b5a1-4565-9156-cab11ab016df 2924669e-f021-4fca-8d18-6b9d00881c1a Completed 09-26-21   []                                                                    grpc-java-netty 1.35.0
```

</details>

### Retrieve logs for SAST scanner
Sample command:

```
user@laptop:~/ast-cli$ ./cx scan logs --scan-id f36b063a-84ca-4c4f-ad22-debacdd588aa --scan-type sast
```

Sample response for sast scanner:

```
26/09/2021 13:05:42,602 [1] INFO  Available memory: 12347 Used memory: 56 Elapsed Time: 00:00:00.1241647 [Unspecified] -
Product version: 9.4.0.0-202107110128-Release
Used memory: 56Mb
OS: Unix 5.4.129.63
Current Directory: /app/Engine

Processor Count: 3
CLR Version: 3.1.18
Executable PID: 19
Executable Location: /usr/share/dotnet/dotnet
Process ID: 19
/ 96 GB Free
/proc 0 GB Free
/dev 0 GB Free
/dev/pts 0 GB Free
/sys 0 GB Free
/sys/fs/cgroup 7 GB Free
/sys/fs/cgroup/systemd 0 GB Free
/sys/fs/cgroup/freezer 0 GB Free
/sys/fs/cgroup/net_cls,net_prio 0 GB Free
/sys/fs/cgroup/memory 0 GB Free
/sys/fs/cgroup/perf_event 0 GB Free
/sys/fs/cgroup/devices 0 GB Free
/sys/fs/cgroup/cpu,cpuacct 0 GB Free
/sys/fs/cgroup/blkio 0 GB Free
/sys/fs/cgroup/hugetlb 0 GB Free
/sys/fs/cgroup/pids 0 GB Free
/sys/fs/cgroup/cpuset 0 GB Free
/dev/mqueue 0 GB Free
/etc/podinfo 7 GB Free
/dev/shm 0 GB Free
/run/secrets/kubernetes.io/serviceaccount 7 GB Free
/proc/bus 0 GB Free
/proc/fs 0 GB Free
/proc/irq 0 GB Free
/proc/sys 0 GB Free
/proc/acpi 7 GB Free
/sys/firmware 7 GB Free

Disk Speed: 526 Ticks per one request
New Disk Speed: 292 Ticks per one request
64Bit platform
PROCESSOR IDENTIFIER: Intel(R) Xeon(R) Platinum 8275CL CPU @ 3.00GHz
Core Speed: 3.6GHz
Product: Checkmarx SAST Engine
-       Main Version:
-       Hotfix Version:
-       Path:
Current Product dll's version list:
___________________________________
Assembly name:                 File version:
ASP.dll                        9.4.0.0-202107110125-Release
CSharp.dll                     9.4.0.0-202107110125-Release
DataCollections.dll            9.4.0.0-202107110128-Release
EngineFacade.dll               9.4.0.0-202107110128-Release
Flowgraphs.dll                 9.4.0.0-202107110128-Release
Plugin.dll                     9.4.0.0-202107110125-Release
Query.dll                      9.4.0.0-202107110128-Release
CxWrm.dll                      9.4.0.0-202107110128-Release
====================================================


26/09/2021 13:05:42,628 [1] INFO  Available memory: 12265 Used memory: 127 Elapsed Time: 00:00:01.7149099 [Unspecified] - Initializing scan input
26/09/2021 13:05:42,645 [1] INFO  Available memory: 12265 Used memory: 128 Elapsed Time: 00:00:01.7321179 [Startup] - Current Engine Configuration from DefaultConfig.xml:
_____________________________
IMPORTANT_FILE_ONLY_SCAN*=true
SMALL_PROJECT_BORDER*=3000000
```

### Retrieving logs for KICS scanner
Sample command:

```
user@laptop:~/ast-cli$ ./cx scan logs --scan-id f36b063a-84ca-4c4f-ad22-debacdd588aa --scan-type kics
```

Sample response for KICS scanner

```
1:03PM | DEBUG | console.scan()
1:03PM | INFO  | Scanning with Keeping Infrastructure as Code Secure v1.3.3
1:03PM | DEBUG | Looking for queries in executable path and in current work directory
1:03PM | DEBUG | helpers.GetDefaultQueryPath()
1:03PM | DEBUG | helpers.GetExecutableDirectory()
1:03PM | DEBUG | Queries found in /app/kics-deployment/assets/queries
1:03PM | INFO  | Loading queries of type: dockerfile, ansible
1:03PM | DEBUG | source.NewFilesystemSource()
1:03PM | DEBUG | storage.NewMemoryStorage()
1:03PM | DEBUG | engine.NewInspector()
1:03PM | INFO  | Inspector initialized, number of queries=289
1:03PM | INFO  | Query execution timeout=1m0s
1:03PM | DEBUG | provider.NewFileSystemSourceProvider()
1:03PM | DEBUG | parser.NewBuilder()
1:03PM | DEBUG | resolver.Add()
1:03PM | DEBUG | resolver.Build()
1:03PM | DEBUG | service.StartScan()
1:03PM | DEBUG | service.StartScan()
1:03PM | DEBUG | engine.Inspect()
1:03PM | DEBUG | engine.Inspect()
1:03PM | DEBUG | model.CreateSummary()
1:03PM | DEBUG | console.resolveOutputs()
1:03PM | DEBUG | helpers.PrintResult()
1:03PM | INFO  | Files scanned: 4
1:03PM | INFO  | Parsed files: 4
1:03PM | INFO  | Queries loaded: 289
1:03PM | INFO  | Queries failed to execute: 0
1:03PM | INFO  | Inspector stopped
1:03PM | DEBUG | console.printOutput()
1:03PM | DEBUG | Output formats provided [json]
1:03PM | DEBUG | helpers.ValidateReportFormats()
1:03PM | DEBUG | helpers.GenerateReport()
1:03PM | INFO  | Results saved to file /tmp/953972639/results.json fileName:results.json
1:03PM | INFO  | Scan duration: 3318ms
```

