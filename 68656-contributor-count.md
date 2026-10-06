# contributor-count

The `contributor-count` command enables users to count **unique contributors** from different **SCM** repositories, for the past **90 days**.


## Usage
```
./cx utils contributor-count [command]
```


## Flags
**`--help, -h`**

Help for the contributor-count command.


## Global Flags
The `contributor-count` command does not support all global flags. The following flags are supported.

**`--proxy <string>`**

Proxy server to send communication through.

**`--proxy-auth-type <string>`**

Proxy authentication type (basic or ntlm).

**`--proxy-ntlm-domain <string>`**

Window domain when using NTLM proxy.

**`--timeout <string>` Default: 5 seconds**

Timeout for network activity.

**`--debug`**

Debug mode returns detailed logs, including the username of each of the contributors and the repos to which they contributed.

