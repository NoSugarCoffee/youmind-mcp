# YouMind MCP Server

A Model Context Protocol (MCP) server built with FastMCP that provides access to YouMind content.

## Installation

```bash
pip install youmind-mcp
```

## Configuration

**To get your authentication token:**
1. Log in to YouMind in your browser
2. Open browser developer tools (F12)
3. Go to Application/Storage > Cookies > https://youmind.com
4. Copy the value of `sb-flzdupptcpbcowdaetfq-auth-token`

## Usage

Configure your MCP client (e.g., Claude Desktop, Cursor) and set the token in the `env` section:

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

## Available Tools

### `get_craft_content`

Retrieves the plain text content of a craft by its ID.

**Parameters:**
- `craft_id` (string, required): The ID of the craft to retrieve

**Returns:**
- The plain text content of the craft

**Example:**
```python
get_craft_content(craft_id="019bc6bc-e1cc-79a2-a6fd-448b711a8895")
```
