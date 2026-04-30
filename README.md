<div align="center">
  <img src="logo.png" alt="youmind-mcp" width="512"/>

  [![PyPI](https://img.shields.io/pypi/v/youmind-mcp)](https://pypi.org/project/youmind-mcp/)
  [![Python](https://img.shields.io/pypi/pyversions/youmind-mcp)](https://pypi.org/project/youmind-mcp/)
  [![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
  [![MCP](https://img.shields.io/badge/MCP-compatible-blueviolet)](https://modelcontextprotocol.io)

  **🧠 Bridge your YouMind content to any AI assistant via the Model Context Protocol 🔗**
</div>

---

## 🚀 Quick Start

```bash
pip install youmind-mcp
```

## ⚙️ Configuration

**Get your authentication token:**
1. Log in to YouMind in your browser
2. Open browser developer tools (F12)
3. Go to Application/Storage > Cookies > https://youmind.com
4. Copy the value of `sb-flzdupptcpbcowdaetfq-auth-token`

Configure your MCP client (e.g., Claude Desktop, Cursor) with the token in the `env` section:

```json
{
  "mcpServers": {
    "youmind": {
      "command": "youmind-mcp",
      "env": {
        "YOUMIND_AUTH_TOKEN": "sb-flzdupptcpbcowdaetfq-auth-token=your-actual-token-here"
      }
    }
  }
}
```

## 🛠️ Available Tools

### `get_craft_content`

Retrieves the plain text content of a craft by its ID.

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `craft_id` | string | ✅ | The ID of the craft to retrieve |

**Returns:** The plain text content of the craft.

**Example:**

```python
get_craft_content(craft_id="019bc6bc-e1cc-79a2-a6fd-448b711a8895")
```

## 📄 License

MIT — see [LICENSE](LICENSE)
