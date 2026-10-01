# GAS Hybrid MCP Server (Google Apps Script Dual-Auth)

An advanced Model Context Protocol (MCP) server for **Google Apps Script** supporting **Dual-Authentication**:
1. **Mode A (Official GCP OAuth2)**: Authorized via Google Cloud Platform credentials.
2. **Mode B (Unofficial Zero-GCP WebApp / Cookie Bridge)**: Run scripts, read/write Google Drive files without any GCP project or OAuth verification hassle.
3. **Mode C (Hybrid Automatic Routing)**: Uses official endpoints when available, falling back to WebApp bridge for unrestricted internal operations.

---

## 🚀 Features

- **Direct Cloud Script Execution**: Run Google Apps Script code directly from Claude, Cursor, Antigravity, or any MCP client.
- **Google Drive Real-Time Sync**: Create and update files (Markdown, JSON, Docs) in Google Drive folders programmatically.
- **Zero-GCP Quickstart**: Paste a 10-line bridge into `script.google.com` and connect immediately with zero API keys.
- **High Availability**: Fallback to local AST validation and dry-run execution if cloud endpoints are temporarily offline.

---

## ⚙️ Configuration in `mcp_config.json`

Add the server to your MCP configuration:

```json
{
  "mcpServers": {
    "gas-hybrid": {
      "command": "node",
      "args": ["C:/Users/abdul/.gemini/antigravity-ide/scratch/gas-hybrid-mcp/index.js"],
      "env": {
        "GOOGLE_APPSCRIPT_WEBAPP_URL": "https://script.google.com/macros/s/YOUR_DEPLOYMENT_ID/exec",
        "GOOGLE_APPSCRIPT_OAUTH_TOKEN": ""
      }
    }
  }
}
```

---

## 🛠️ Available MCP Tools

| Tool | Description |
| :--- | :--- |
| `gas_get_status` | Returns active authentication mode (Official, Zero-GCP, or Hybrid) |
| `gas_run_code` | Executes arbitrary Apps Script JavaScript code and returns console logs |
| `gas_sync_drive_file` | Creates or updates documents/markdown in Google Drive folders |
| `gas_create_project` | Scaffolds a new Apps Script project with manifest and V8 engine |

---

## 📄 License
Apache-2.0 © abdulaaly
