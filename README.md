# Diagram Prompts MCP Server

MCP server that provides AWS architecture diagram generation prompts with parameter support.

## Installation

1. Install dependencies:
```bash
pip install -r requirements.txt
```

2. Configure in Kiro CLI by adding to your MCP settings (`~/.kiro/mcp.json`):
```json
{
  "mcpServers": {
    "diagram-prompts": {
      "command": "python",
      "args": ["/home/nizar/diagram-prompts-mcp/server.py"]
    }
  }
}
```

## Usage

In Kiro CLI chat:
```
@diagram-prompts/dg EC2 instance with ALB and RDS database
```

## Available Prompts

- `dg` - AWS Architecture Diagram Generator
  - Arguments:
    - `description` (required): Architecture description
# diagram-prompts-mcp
