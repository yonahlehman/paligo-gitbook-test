# Checkmarx MCP Server

## Overview

Modern development and security workflows are increasingly centered around AI-assisted environments. However, traditional security tooling often requires users to leave these environments to take action, disrupting productivity and reducing engagement. The Checkmarx MCP Server addresses this gap by bringing security operations directly into the tools where users already work — making it easier to adopt, integrate, and act on security insights in real time

<details>

<summary>Test Expandable</summary>

Test Content

</details>

The Checkmarx MCP Server acts as a translation layer between MCP-compatible clients and the Checkmarx One REST APIs, enabling developers and security teams to interact with Checkmarx One from AI assistants and supported third-party integrations. Through these clients, users can interact with Checkmarx One using natural language within an IDE, terminal, chat, or other supported interface. Users can trigger scans, retrieve findings, and query security posture within AI workflows without needing to switch to the platform UI. That means that a developer can now request a scan and immediately receive prioritized results and a security lead can query organization-wide coverage and risk trends, without disrupting their workflows.

Built on the Model Context Protocol (MCP), an open standard for connecting AI applications and platforms to external tools and data sources, the Checkmarx MCP Server exposes a curated set of capabilities that map to Checkmarx One functionality. It acts as a controlled interface between AI agents and the Checkmarx APIs, enabling secure, structured access to data and actions through natural language. This release introduces the initial phase of the MCP Server - providing a minimal set of capabilities required to support meaningful, end-to-end workflows for both developers and AppSec teams. We will soon be adding more advanced capabilities such as automated triage, external integrations, and agent-driven workflows.

## Who is it for?

* **Developers** - Trigger scans and receive prioritized findings directly within the IDE or terminal, without switching between tools.
* **AppSec Engineers** - Query findings by severity, type, or scanner; manage project and application inventory; and monitor scan status.
* **Security Leads** - Gain organization-wide visibility into scan coverage, risk posture, and trends across teams through simple, natural language queries.

## Supported Scanners and Tools

* **Scanners** - Supported for **SAST**, **SCA**, **IaC Security**, **Secrets** and **API Security**.
* **Tools** - Currently provides tools in the areas of remediation, scan workflow, project, and application management, scan history and triage. Other advanced Checkmarx One workflows are not yet supported.

{% hint style="info" %}
Triage tools are not yet supported for the **API Security** scanner.
{% endhint %}

## Prerequisites

Certain MCP features require the Checkmarx CLI to be installed and configured. To enable these features, ensure that the Checkmarx CLI is installed and that the MCP can access its executable path.

For best results, use credentials with matching permissions in both the Checkmarx CLI and the MCP server configuration. Permission mismatches may prevent some operations from completing successfully.

Local directory scanning specifically requires access to the Checkmarx CLI and is not available through the MCP alone.

## Data Security

* Data in encryption in transit - TLS 1.2+ on all connections
* No credential storage or logging
* Complete tenant segregation
* RBAC passthrough enforced - no privilege escalation via MCP
* Repo URL credentials always sanitized - never shown to user
* No destructive activities (e.g., project deletion) allowed via MCP

## Authentication and Permissions

Authentication is done using an OAuth login workflow or by submitting an API Key. Once authenticated, the MCP is able to interact with the relevant tenant account based on the specific set of permissions assigned to the user or API Key.

The MCP is available to all Checkmarx One customers. However, functionality is limited based on:

* **License Packages** - Only tools licensed for your account are available. For example, remediation tools are only available for accounts with **Checkmarx One Assist**, **AI Protection** or **Checkmarx Developer Assist** license. In addition, only licensed scanners can be run.
* **User Permissions** - Tools are only available to users with the relevant permission for each action (based on Checkmarx One IAM). For example, only users with permission to run scans can initiate a scan via the MCP. And, only users with access to a particular project can ask the MCP to view results for that project.

### Supported Authentication Methods

Checkmarx MCP supports the following authentication methods:

* **API Key** -Submit a JWT (JSON Web Token) access token. Access tokens are obtained via the Checkmarx web application (UI), see [Creating an API Key for Checkmarx One Integrations](https://docs.checkmarx.com/en/34965-182096-creating-an-api-key-for-checkmarx-one-integrations.html).
* **Predefined OAuth Client** — Uses a fixed OAuth client that is registered in advance. This is the simpler option, relying on a known, shared client identity. Use this predefined clientId: `cx-mcp-client`
* **Dynamic OAuth Client Registration** (DCR) — The MCP client registers itself dynamically at runtime by calling the authorization server's registration endpoint, obtaining its own client credentials on the fly.

{% hint style="warning" %}
There is an upper limit of 500 clients per tenant using DCR authentication. When the limit is reached, the following message is displayed:

_Policy 'Max Clients Limit' rejected request to client-registration service_

In this case, you must use one of the other authentication methods for some of your users.
{% endhint %}

#### Supported Methods by Platform

The following table shows which authentication methods are supported for each platform.

| Platform                      | API Key | Predefined OAuth Client |    DCR   |
| ----------------------------- | :-----: | :---------------------: | :------: |
| Claude Code                   |    ✔    |            ✔            |     ✔    |
| Gemini CLI                    |    ✔    |            ✔            |     ✔    |
| Codex CLI                     |    ✔    |            x            |     ✔    |
| Copilot CLI                   |    ✔    |            x            |     ✔    |
| Cursor IDE                    |    ✔    |            ✔            | See note |
| VS Code                       |    ✔    |            ✔            |     ✔    |
| JetBrains IDEs                |    ✔    |            x            |     x    |
| Windsurf                      |    ✔    |            x            |     ✔    |
| Kiro IDE                      |    ✔    |            x            |     ✔    |
| Antigravity IDE               |    ✔    |            x            |     ✔    |
| Claude Web and Claude Desktop |    x    |            ✔            |     ✔    |
| Amazon Quick                  |    x    |            ✔            |     ✔    |

## Installation and Configuration

The Checkmarx MCP Server can be integrated with AI assistants and development tools that connect directly to the MCP server, as well as with supported third-party platforms.

* **AI Assistants and Development Tools** — Connect an MCP-compatible AI assistant or development tool directly to the Checkmarx MCP Server. Installation and authentication methods vary by platform.
* **Third-Party Integrations** — Connect a third-party platform, such as Amazon Quick, to the Checkmarx MCP Server. These integrations may require additional configuration within the third-party platform.

### Checkmarx One Server Base URLs

{% hint style="info" %}
For all installation flows, you will need to provide your Checkmarx One Server Base URL.

* US Environment - https://ast.checkmarx.net
* US2 Environment - https://us.ast.checkmarx.net
* EU Environment - https://eu.ast.checkmarx.net
* EU2 Environment - https://eu-2.ast.checkmarx.net
* DEU Environment - https://deu.ast.checkmarx.net
* Australia & New Zealand – https://anz.ast.checkmarx.net
* India - https://ind.ast.checkmarx.net
* India 2 - https://ind-2.ast.checkmarx.net/
* Singapore - https://sng.ast.checkmarx.net
* UAE - https://mea.ast.checkmarx.net
* Israel - https://gov-il.ast.checkmarx.net
{% endhint %}

### IAM Base URLs

{% hint style="warning" %}
For some third-party integration configurations, you will need to provide your IAM Base URL.

* US: https://iam.checkmarx.net
* US2: https://us.iam.checkmarx.net
* EU: https://eu.iam.checkmarx.net
* EU2: https://eu-2.iam.checkmarx.net
* DEU: https://deu.iam.checkmarx.net
* Australia & NZ: https://anz.iam.checkmarx.net
* India: https://ind.iam.checkmarx.net
* Singapore: https://sng.iam.checkmarx.net
* UAE: https://mea.iam.checkmarx.net
{% endhint %}

## AI Assistants and Developer Tools

Use the following instructions to connect your AI assistant or development tool directly to the Checkmarx MCP Server. Select your platform below. The supported authentication methods for each platform are listed in the recommended order.

{% tabs %}
{% tab title="Claude Code" %}
You can register, authenticate and enable the MCP directly from the command line. Follow the instructions below for your chosen authentication method.

#### API Key

Enter the following command, replacing the placeholders:

```
claude mcp add --transport http --scope user Checkmarx <CX_BASE_URL>/api/security-mcp/mcp --header "Authorization: <API_KEY>"
```

#### Predefined OAuth Client

*   Enter the following command, replacing the placeholders:

    ```
    claude mcp add  --transport http   Checkmarx ${CX_BASE_URL}/api/security-mcp/mcp/{tenant_name} --client-id cx-mcp-client
    ```
* Enter `/mcp` to view the Checkmarx MCP.
* Select **Authenticate**.
* You will be redirected to Checkmarx One login.

#### DCR

*   Enter the following command, replacing the placeholders:

    ```
    claude mcp add --transport http --scope user Checkmarx <CX_BASE_URL>/api/security-mcp/mcp/<TENANT_NAME>
    ```
* Enter `/mcp` to view the Checkmarx MCP.
* Select **Authenticate**.
* You will be redirected to Checkmarx One login.
{% endtab %}

{% tab title="Gemini CLI" %}
You can register, authenticate and enable the MCP directly from the command line. This method uses an API Key.

#### API Key

Enter the following command, replacing the placeholders:

```
gemini mcp add --scope user --transport http Checkmarx <CX_BASE_URL>/api/security-mcp/mcp --header "Authorization: <API_KEY>"
```

#### Manual Installation

Follow the instructions below for your chosen authentication method.

#### Predefined OAuth Client

* Open `~/.gemini/settings.json`.
*   Add the following MCP server configuration:

    ```
    {
      "mcpServers": {
        "Checkmarx": {
          "httpUrl": "<CX_BASE_URL>/api/security-mcp/mcp/<TENANT_NAME>",
          "oauth": {
            "clientId": "cx-mcp-client"
          }
        }
      }
    }
    ```
* Replace the placeholder values and save the configuration.
* Authenticate using the command: `/mcp auth Checkmarx`.
* Complete the browser-based authentication flow.

#### DCR

* Open `~/.gemini/settings.json`.
*   Add the following MCP server configuration:

    ```
    {
      "mcpServers": {
        "Checkmarx": {
          "httpUrl": "<CX_BASE_URL>/api/security-mcp/mcp/<TENANT_NAME>"
        }
      }
    }
    ```
* Replace the placeholder values and save the configuration.
* Authenticate using the command: `/mcp auth Checkmarx`.
* Complete the browser-based authentication flow.
{% endtab %}

{% tab title="Codex CLI" %}
Follow the instructions below for your chosen authentication method.

#### DCR

* Open `~/.codex/config.toml`.
*   Add the following MCP server configuration:

    ```
    [mcp_servers.Checkmarx]
    url = "<CX_BASE_URL>/api/security-mcp/mcp/<TENANT_NAME>"
    ```
* Replace the placeholder values and save the configuration.
* Authenticate using the command: `codex mcp login Checkmarx`.
* Complete the browser-based authentication flow.

#### API Key

* Open `~/.codex/config.toml`.
*   Add the following MCP server configuration:

    ```
    [mcp_servers.Checkmarx]
    url = "<CX_BASE_URL>/api/security-mcp/mcp"

    [mcp_servers.Checkmarx.http_headers]
    Authorization = "<API_KEY>"
    ```
* Replace the placeholder values and save the configuration.
{% endtab %}

{% tab title="Copilot CLI" %}
You can register, authenticate and enable the MCP directly from the command line. Follow the instructions below for your chosen authentication method.

#### API Key

Enter the following command, replacing the placeholders:

```
copilot mcp add --transport http Checkmarx <CX_BASE_URL>/api/security-mcp/mcp --header "Authorization: <API_KEY>"
```

#### DCR

*   Enter the following command, replacing the placeholders:

    ```
    copilot mcp add --transport http Checkmarx <CX_BASE_URL>/api/security-mcp/mcp/<TENANT_NAME>
    ```
* Enter `/mcp` to view the Checkmarx MCP.
* Select **Checkmarx**.
* Select **Authenticate**.
* You will be redirected to Checkmarx One login.
{% endtab %}

{% tab title="Cursor IDE" %}
Follow the instructions below for your chosen authentication method.

#### Predefined OAuth Client

* Open `~/.cursor/mcp.json`.
*   Add the following MCP server configuration:

    ```
    {
      "mcpServers": {
        "Checkmarx": {
          "url": "<CX_BASE_URL>/api/security-mcp/mcp/<TENANT_NAME>",
          "auth": {
            "CLIENT_ID": "cx-mcp-client"
          }
        }
      }
    }
    ```
* Replace the placeholder values and save the configuration.
* Authenticate from **Settings > MCP**.
* Complete the browser-based authentication flow.

#### API Key

* Open `~/.cursor/mcp.json`.
*   Add the following MCP server configuration:

    ```
    {
      "mcpServers": {
        "Checkmarx": {
          "url": "<CX_BASE_URL>/api/security-mcp/mcp",
          "headers": {
            "cx-origin": "Cursor",
            "Authorization": "<API_KEY>"
          }
        }
      }
    }
    ```
* Replace the placeholder values and save the configuration.

#### DCR

{% hint style="warning" %}
There is a known issue that is causing DCR authentication to fail in Cursor. Please use a predefined client until the issue is resolved.
{% endhint %}

* Open `~/.cursor/mcp.json`.
*   Add the following MCP server configuration:

    ```
    {
      "mcpServers": {
        "Checkmarx": {
          "url": "<CX_BASE_URL>/api/security-mcp/mcp/<TENANT_NAME>"
        }
      }
    }
    ```
* Replace the placeholder values and save the configuration.
* Complete the browser-based authentication flow.
{% endtab %}

{% tab title="VS Code" %}
#### Predefined OAuth Client

* Open the user configuration with **MCP: Open User Configuration** from the Command Palette (Ctrl+Shift+P / Cmd+Shift+P).
*   Add the following MCP server configuration:

    ```
    {
      "servers": {
        "checkmarx": {
          "type": "http",
          "url": "<CX_BASE_URL>/api/security-mcp/mcp/<TENANT_NAME>",
          "oauth": {
            "clientId": "cx-mcp-client"
          }
        }
      }
    }
    ```
* Replace the placeholder values and save the configuration.
* Authenticate from **Settings > MCP**.
* Complete the browser-based authentication flow.

#### DCR

* Open the user configuration with **MCP: Open User Configuration** from the Command Palette (Ctrl+Shift+P / Cmd+Shift+P).
*   Add the following MCP server configuration:

    ```
    {
      "servers": {
        "checkmarx": {
          "type": "http",
          "url": "<CX_BASE_URL>/api/security-mcp/mcp/<TENANT_NAME>"
        }
      }
    }
    ```
* Replace the placeholder values and save the configuration.
* Complete the browser-based authentication flow.

#### API Key

* Open the user configuration with **MCP: Open User Configuration** from the Command Palette (Ctrl+Shift+P / Cmd+Shift+P).
*   Add the following MCP server configuration:

    ```
    {
      "servers": {
        "checkmarx": {
          "type": "http",
          "url": "<CX_BASE_URL>/api/security-mcp/mcp",
          "headers": {
            "cx-origin": "Vscode",
            "Authorization": "<API_KEY>"
          }
        }
      }
    }
    ```
* Replace the placeholder values and save the configuration.
{% endtab %}

{% tab title="JetBrains IDEs" %}
Applies to IntelliJ IDEA, PyCharm, GoLand, WebStorm, Rider and other JetBrains IDEs with AI Assistant. JetBrains AI Assistant does not support OAuth-based MCP authentication — only a static token supplied as a request header. To install, follow the instructions below.

#### API Key

* Open **Settings > Tools > AI Assistant > Model Context Protocol (MCP)**.
* Click **Add**.
* In the **New MCP Server** dialog, select the **Streamable HTTP** connection type (not STDIO).
*   Switch the dialog to **As JSON** and enter the following configuration:

    ```
    {
      "mcpServers": {
        "Checkmarx": {
          "url": "<CX_BASE_URL>/api/security-mcp/mcp",
          "headers": {
            "cx-origin": "Jetbrains",
            "Authorization": "<API_KEY>"
          }
        }
      }
    }
    ```
* Replace the placeholder values and save the configuration.
* Set the server level to **Global** so the MCP is available in all projects, rather than **Project**, which limits it to the current project.
* Click **OK**, then **Apply** to start the server.
{% endtab %}

{% tab title="Windsurf" %}
#### DCR

* Open `~/.codeium/windsurf/mcp_config.json`.
*   Add the following MCP server configuration:

    ```
    {
      "mcpServers": {
        "Checkmarx": {
          "serverUrl": "<CX_BASE_URL>/api/security-mcp/mcp/<TENANT_NAME>"
        }
      }
    }
    ```
* Replace the placeholder values and save the configuration.
* Select **Settings > Cascade > MCP Servers > Refresh**.
* Authenticate from the MCP panel.

#### API Key

* Open `~/.codeium/windsurf/mcp_config.json`.
*   Add the following MCP server configuration:

    ```
    {
      "mcpServers": {
        "Checkmarx": {
          "serverUrl": "<CX_BASE_URL>/api/security-mcp/mcp",
          "headers": {
            "cx-origin": "Windsurf",
            "Authorization": "<API_KEY>"
          }
        }
      }
    }
    ```
* Replace the placeholder values and save the configuration.
* Select **Settings > Cascade > MCP Servers > Refresh**.
{% endtab %}

{% tab title="Kiro IDE" %}
#### DCR

* Open `~/.kiro/settings/mcp.json`.
*   Add the following MCP server configuration:

    ```
    {
      "mcpServers": {
        "Checkmarx": {
          "url": "<CX_BASE_URL>/api/security-mcp/mcp/<TENANT_NAME>"
        }
      }
    }
    ```
* Replace the placeholder values.
* Click **Authenticate**.
* Complete the browser-based authentication flow.

#### API Key

* Open `~/.kiro/settings/mcp.json`.
*   Add the following MCP server configuration:

    ```
    {
      "mcpServers": {
        "Checkmarx": {
          "url": "<CX_BASE_URL>/api/security-mcp/mcp",
          "headers": {
            "cx-origin": "Kiro",
            "Authorization": "<API_KEY>"
          }
        }
      }
    }
    ```
* Replace the placeholder values and save the configuration.
{% endtab %}

{% tab title="Antigravity IDE" %}
#### DCR

* Open `~/.gemini/config/mcp_config.json`.
*   Add the following MCP server configuration:

    ```
    {
      "mcpServers": {
        "Checkmarx": {
          "serverUrl": "<CX_BASE_URL>/api/security-mcp/mcp/<TENANT_NAME>"
        }
      }
    }
    ```
* Replace the placeholder values.
* The MCP is added in the **Install MCP** section of the IDE.
* Click **Authenticate**.

#### API Key

* Open `~/.gemini/config/mcp_config.json`.
*   Add the following MCP server configuration:

    ```
    {
      "mcpServers": {
        "Checkmarx": {
          "serverUrl": "<CX_BASE_URL>/api/security-mcp/mcp",
          "headers": {
            "Authorization": "<API_KEY>"
          }
        }
      }
    }
    ```
* Replace the placeholder values.
{% endtab %}

{% tab title="Claude Web and Claude Desktop" %}
* Navigate to **Settings > Connectors**.
* Click the **Add** button.
* Hover over **Custom**, then select **Web**.
* Add your connector's remote MCP server URL: `<CX_BASE_URL>/api/security-mcp/mcp/<TENANT_NAME>`.
* To use a predefined client ID, click **Advanced settings** and specify the OAuth Client ID: `cx-mcp-client`. Leave it empty to use DCR.
* Click **Add**, then **Connect**, and complete the Checkmarx One login.

{% hint style="info" %}
Enterprise administrators can introduce custom connectors as described [here](https://support.claude.com/en/articles/11175166-get-started-with-custom-connectors-using-remote-mcp?utm_source=chatgpt.com#h_3d1a65aded).
{% endhint %}
{% endtab %}
{% endtabs %}

### Troubleshooting

| Message or symptom                                                           | Cause                                                                      | Resolution                                                                 |
| ---------------------------------------------------------------------------- | -------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| `401 Unauthorized` on all calls                                              | API Key invalid, expired, or issued in a different environment             | Regenerate the key and confirm the Base URL matches the issuing tenant     |
| `401` after a successful browser login                                       | Token issued for a different tenant                                        | Verify `<TENANT_NAME>` in the endpoint URL                                 |
| `Policy 'Max Clients Limit' rejected request to client-registration service` | Tenant reached the 500 DCR client limit                                    | Use the Predefined OAuth Client or an API Key for some users               |
| `403 Forbidden` on a single operation                                        | Permission gating                                                          | The user lacks the Checkmarx One permission for that action                |
| Server does not connect                                                      | Endpoint URL shape                                                         | API Key endpoints have no tenant path segment; OAuth endpoints require one |
| `404 Not Found`                                                              | Trailing slash on the Base URL, or a mistyped `/api/security-mcp/mcp` path | Correct the URL                                                            |
| Configuration saved but no server appears                                    | Wrong root key                                                             | VS Code and Visual Studio use `servers`; other platforms use `mcpServers`  |
| Root key correct but no server appears                                       | Wrong URL field                                                            | Windsurf and Antigravity use `serverUrl`; Gemini CLI uses `httpUrl`        |
| Copilot CLI connects but exposes no tools                                    | `tools` field missing from a manually edited configuration                 | Add `"tools": ["*"]`                                                       |
| Server available in one project only                                         | Configuration written at project scope                                     | Reapply at user scope                                                      |
| Remediation tools not listed                                                 | License gating                                                             | Requires Checkmarx One Assist, AI Protection or Checkmarx Developer Assist |
| Local directory scan does not run                                            | Checkmarx One CLI not installed or not on `PATH`                           | Verify with `cx version`                                                   |
| Scan starts but the CLI step fails                                           | CLI and MCP configured with different credentials                          | Use matching credentials                                                   |

## Third-Party Integrations

Third-party platforms can integrate with the Checkmarx MCP Server to make Checkmarx tools available through their own AI agents and interfaces.

## Using the MCP

Interact with Checkmarx One via natural language chat in your AI assistant. The MCP interprets your instructions and runs the appropriate tools to provide the requested information and initiate the appropriate activities. A single prompt can trigger a series of tools, with the AI Agent requesting confirmation or additional input before moving from one step to the next.

The following is a list of tools by category. More detailed information about each tool is available below.

* Remediation
  * packageRemediation
  * codeRemediation
  * imageRemediation
* Scan Workflow
  * planScan
  * triggerScan
  * getScanDetails
  * getLatestScans
  * listFindings
  * getFindingDetails
  * getTenantVulnerabilitiesSummary
* Finding Triage
  * changeFindingState
  * changeFindingSeverity
  * getTriageHistory
* Project Management
  * resolveProject
  * createProject
  * listProjects
  * getProjectConfig
* Application Management
  * listApplications
  * getApplicationDetails
  * createApplication
  * associateProject
* Scan History
  * listScans

### Sample Workflows

#### Scan Project

The MCP can be used to run an E2E flow of triggering a scan, viewing results, identifying risks, and remediating those risks. The process begins by the developer entering a chat "scan this project" (or similar prompt). AI Agent runs the following tools, asking for input and/or confirmation before moving from one step to the next:

1. `resolveProject` - Checks if a corresponding project already exists in your Checkmarx One account, based on project name.

{% hint style="info" %}
To identify a project based on repository URL, other prompts are used. For example, trigger the `listProjects` tool by asking the agent to "Show Checkmarx projects", and search for the desired repository URL.
{% endhint %}

2. `createProject` - If the project doesn't exist, then a new project is created.
3. `getLatestScans` - For pre-existing projects, checks if a scan has already run on the same commit, enabling display of results from that scan.
4. `planScan` - Checks file types and determines which scanners to run.
5. `triggerScan` - The scan is run using the relevant scanners.
6. `getScanDetails` - Polls the status of the scan, until it is completed.

{% hint style="info" %}
For longer scans, the scan will continue running in the background and the user needs to prompt to check for completion.
{% endhint %}

This tool also provides vulnerability summaries by severity upon scan completion.

7. The developer can drill down further by asking additional questions like, "show me the critical vulnerabilities", "which packages have critical risks", "Show me all revealed secrets" etc. (triggering additional tools such as `listFindings` and `getFindingDetails`.
8. **Triage the finding** - After reviewing a finding, the developer can change its state or severity by asking, for example, "mark this finding as confirmed", "mark this finding as not exploitable", or "set this finding severity to high" (triggering `changeFindingState` or `changeFindingSeverity`). The agent asks for confirmation before applying the change.
9. After identifying a vulnerability that requires remediaton the user can give instructions to remediate by saying "fix it", "find a safer package", "remediate this finding" etc. (triggering `packageRemediation`, `codeRemediation` or `imageRemediation`).
