---
name: YouMind MCP Server
overview: Create a Python-based Model Context Protocol (MCP) server using FastMCP that provides a tool to retrieve craft content from YouMind by craft ID.
todos:
  - id: setup-project
    content: Create project structure, requirements.txt, and basic configuration files
    status: completed
  - id: api-client
    content: Implement YouMindAPIClient class with authentication and getCraft API method
    status: completed
    dependencies:
      - setup-project
  - id: mcp-server
    content: Implement FastMCP server with get_craft_content tool
    status: completed
    dependencies:
      - api-client
  - id: content-extraction
    content: Implement content extraction logic for craft content.plain field
    status: completed
    dependencies:
      - api-client
  - id: error-handling
    content: Add comprehensive error handling for API failures and edge cases
    status: completed
    dependencies:
      - mcp-server
  - id: documentation
    content: Create README with setup instructions and usage examples
    status: completed
    dependencies:
      - mcp-server
---

# YouMind MCP Server Implementation Plan

## Overview

Build a Python MCP server using FastMCP that exposes one tool:

1. `get_craft_content` - Retrieves craft content by craft ID

## Architecture

The server will use FastMCP library to create an MCP server, making authenticated requests to YouMind's API endpoints.

## Implementation Details

### 1. Project Structure

```javascript
youmind-mcp/
├── server.py          # Main FastMCP server implementation
├── api_client.py      # YouMind API client
├── requirements.txt
├── README.md
└── .env.example
```



### 2. Dependencies (`requirements.txt`)

- `fastmcp` - FastMCP library for building MCP servers
- `httpx` or `requests` - HTTP client for API calls
- `python-dotenv` - Environment variable management

### 3. Core Components

#### `api_client.py`

- `YouMindAPIClient` class
- Method:
- `get_craft(craft_id: str)` - Calls `POST /api/v1/getCraft` with body `{"id": craft_id}`
- Handles authentication via cookie header from environment variable
- Sets required headers (x-client-type, x-time-zone, x-use-snake-case, accept, content-type, etc.)
- Returns the full API response

#### `server.py`

- Uses FastMCP to create the MCP server
- Defines one tool using `@mcp.tool` decorator:
- `get_craft_content(craft_id: str)`: Takes `craft_id` parameter, returns craft content (extracts `content.plain` field)
- Uses `mcp.run(transport="stdio")` to start the server
- Error handling for API failures and invalid IDs

### 4. Configuration

- Environment variable: `YOUMIND_AUTH_TOKEN` - Contains the full cookie string (sb-flzdupptcpbcowdaetfq-auth-token=...)
- Base URL: `https://youmind.com/api/v1`

### 5. Content Extraction

- For `get_craft_content`: Extract and return the `content.plain` field from the API response
- The tool should return the plain text content in a user-friendly format

### 6. Error Handling

- Handle HTTP errors (4xx, 5xx)
- Handle missing IDs
- Handle authentication failures
- Return user-friendly error messages via MCP error responses

## API Endpoints Used

- `POST /api/v1/getCraft` with body `{"id": "craft-id"}`

## FastMCP Implementation Pattern

The server will use FastMCP's decorator pattern:

```python
from fastmcp import FastMCP

mcp = FastMCP("YouMindMCP")

@mcp.tool
def get_craft_content(craft_id: str) -> str:
    """
    Retrieve craft content by craft ID.
    
    Args:
        craft_id: The ID of the craft to retrieve
        
    Returns:
        The plain text content of the craft
    """
    # Implementation here
    pass

if __name__ == "__main__":
    mcp.run(transport="stdio")
```