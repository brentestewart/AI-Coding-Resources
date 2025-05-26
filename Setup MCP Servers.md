## Example MCP Server Configuration for VS Code
VS Code: Place the following in projectdirectory/.vscode/mcp.json
Cursor: Place the following in projectdirectory/.cursor/mcp.json

```
{
 "inputs": [
    {
      "type": "promptString",
      "id": "github_token",
      "description": "GitHub Personal Access Token",
      "password": true
    },
    {
      "type": "promptString",
      "id": "supabase-access-token",
      "description": "Supabase Personal Access Token",
      "password": true
    }
  ],
  "servers": {
    "Context7": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@upstash/context7-mcp"]
    },
    "supabase": { 
	  "command": "cmd", 
	  "args": ["/c", "npx", "-y", "@supabase/mcp-server-supabase@latest"], 
	  "env": { "SUPABASE_ACCESS_TOKEN": "${input:supabase-access-token}" 
	},
    "github": {
      "command": "docker",
      "args": [
        "run",
        "-i",
        "--rm",
        "-e",
        "GITHUB_PERSONAL_ACCESS_TOKEN",
        "ghcr.io/github/github-mcp-server"
      ],
      "env": {
        "GITHUB_PERSONAL_ACCESS_TOKEN": "${input:github_token}"
      }
    }    
  }
}
```