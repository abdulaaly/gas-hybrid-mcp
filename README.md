# GAS Hybrid MCP Server (Google Apps Script Dual-Auth)

An enterprise-grade Model Context Protocol (MCP) server for **Google Apps Script** providing complete API parity with `mohalmah/google-appscript-mcp-server` while introducing **Dual-Authentication Architecture (Official + Cookie Session + Hybrid Auto-Failover)**.

---

## 🌟 The 3 Authentication Modes

Users and AI agents can choose how to connect based on their requirements:

1. **Mode `official` (GCP Authorized)**:
   - Uses `GOOGLE_APPSCRIPT_OAUTH_TOKEN` (Bearer token generated via Google Cloud Console).
   - Strict standard compliance with Google Apps Script REST API v1.

2. **Mode `cookie` (Unofficial / Zero-GCP Setup)**:
   - Uses `GOOGLE_APPSCRIPT_COOKIE` (Raw session cookies) or Clasp tokens.
   - **Zero Google Cloud Console hassle**: bypasses creating GCP projects, OAuth client IDs, and verification screens.
   - Grants direct access to internal Apps Script execution endpoints.

3. **Mode `hybrid` (Default & Recommended)**:
   - Tries the official GCP API first.
   - If unauthenticated, permission denied (401/403), or if an endpoint is restricted by GCP policies, it **automatically fails over to the cookie session bridge** with zero interruption to your workflow.

---

## 🛠️ Complete Suite of 14 MCP Tools

| Tool Name | Category | Description |
| :--- | :--- | :--- |
| `gas_get_status` | System | Checks active auth mode (Official, Cookie, or Hybrid) & server health |
| `gas_set_auth_mode` | System | Dynamically switches between `official`, `cookie`, and `hybrid` |
| `gas_create_project` | Project | Creates a new standalone Google Apps Script project in Google Drive |
| `gas_get_project` | Project | Retrieves metadata and file info for a project by `scriptId` |
| `gas_get_content` | Code | Downloads all `.gs` source files and `appsscript.json` manifest |
| `gas_update_content` | Code | Uploads and overwrites code files in a project |
| `gas_run_function` | Execution | Runs a deployed Google Apps Script function in the cloud |
| `gas_eval_snippet` | Execution | Evaluates arbitrary JavaScript in the cloud Apps Script V8 runtime |
| `gas_sync_drive_file` | Drive | Directly creates or updates files/markdown in Google Drive folders |
| `gas_list_deployments` | Deploy | Lists all active Web App and API deployments for a script |
| `gas_create_deployment` | Deploy | Creates a new Web App or API executable deployment |
| `gas_delete_deployment` | Deploy | Deletes an existing deployment |
| `gas_list_versions` | Versions | Lists all immutable version snapshots of a project |
| `gas_create_version` | Versions | Creates a new immutable version snapshot |

---

## ⚙️ Configuration in `mcp_config.json`

```json
{
  "mcpServers": {
    "gas-hybrid": {
      "command": "node",
      "args": ["C:/Users/abdul/.gemini/antigravity-ide/scratch/gas-hybrid-mcp/index.js"],
      "env": {
        "GOOGLE_APPSCRIPT_MODE": "hybrid",
        "GOOGLE_APPSCRIPT_OAUTH_TOKEN": "",
        "GOOGLE_APPSCRIPT_COOKIE": ""
      }
    }
  }
}
```

---

## 📄 License
Apache-2.0 © abdulaaly
