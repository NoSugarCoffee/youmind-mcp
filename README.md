# YouMind MCP Server

A Model Context Protocol (MCP) server built with FastMCP that provides access to YouMind content.

## Features

- Retrieve craft content by craft ID
- Authenticated API access to YouMind
- Simple FastMCP-based implementation

## Prerequisites

- Python 3.8 or higher
- A YouMind account with valid authentication token

## Installation

1. Clone this repository:
```bash
git clone <repository-url>
cd youmind-mcp
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Set up environment variables:
```bash
cp .env.example .env
```

4. Edit `.env` and add your YouMind authentication token:
```
YOUMIND_AUTH_TOKEN=sb-flzdupptcpbcowdaetfq-auth-token=your-actual-token-here
```

To get your authentication token:
1. Log in to YouMind in your browser
2. Open browser developer tools (F12)
3. Go to Application/Storage > Cookies > https://youmind.com
4. Copy the value of `sb-flzdupptcpbcowdaetfq-auth-token`
5. Set `YOUMIND_AUTH_TOKEN=sb-flzdupptcpbcowdaetfq-auth-token=<copied-value>`

## Usage

### Running the Server

Run the MCP server:
```bash
python server.py
```

The server will start and communicate via stdio (standard input/output), which is the standard transport for MCP servers.

### Using with MCP Clients

Configure your MCP client (e.g., Claude Desktop, Cursor) to use this server:

```json
{
  "mcpServers": {
    "youmind": {
      "command": "python",
      "args": ["/path/to/youmind-mcp/server.py"],
      "env": {
        "YOUMIND_AUTH_TOKEN": "sb-flzdupptcpbcowdaetfq-auth-token=your-token"
      }
    }
  }
}
```

### Available Tools

#### `get_craft_content`

Retrieves the plain text content of a craft by its ID.

**Parameters:**
- `craft_id` (string, required): The ID of the craft to retrieve

**Returns:**
- The plain text content of the craft, or an error message if the craft is not found or accessible

**Example:**
```python
# Called via MCP protocol
get_craft_content(craft_id="019bc6bc-e1cc-79a2-a6fd-448b711a8895")
```

## Project Structure

```
youmind-mcp/
├── server.py          # Main FastMCP server implementation
├── api_client.py      # YouMind API client
├── requirements.txt   # Python dependencies
├── README.md         # This file
└── .env.example      # Environment variable template
```

## Error Handling

The server handles various error scenarios:

- **404 Not Found**: Craft ID doesn't exist
- **401 Unauthorized**: Authentication token is invalid or expired
- **403 Forbidden**: No permission to access the craft
- **Network Errors**: Connection issues with YouMind API
- **Invalid Input**: Empty or malformed craft IDs

All errors are returned as user-friendly messages.

## Development

### Testing

You can test the API client directly:

```python
from api_client import YouMindAPIClient

client = YouMindAPIClient()
response = client.get_craft("craft-id-here")
print(response)
```

## Support

For issues or questions, please open an issue in the repository.

