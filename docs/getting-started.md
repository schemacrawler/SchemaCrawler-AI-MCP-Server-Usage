# Getting Started With the SchemaCrawler AI MCP Server

The SchemaCawler AI MCP Server is available as a Docker image from [Docker Hub](https://hub.docker.com/mcp/server/schemacrawler-ai/overview).

## Prerequisites

1. Install supporting software
   - [Docker](https://docs.docker.com/engine/install/)
   - Docker Compose
   - [Visual Studio Code](https://code.visualstudio.com/download)
2. Read [Use MCP servers in VS Code](https://code.visualstudio.com/docs/copilot/chat/mcp-servers)
3. Clone this project, and open it in Visual Studio Code


## Start the SchemaCrawler AI MCP Server

1. Pull the latest image for SchemaCrawler AI MCP Server
   ```sh
   docker compose -f schemacrawler-mcpserver.yaml pull
   ```
2. Run the SchemaCrawler AI MCP Server
   ```sh
   docker compose -f schemacrawler-mcpserver.yaml up -d
   ```
3. Check server health in a browser [http://localhost:9292/health](http://localhost:9292/health)


## Use Visual Studio Code MCP Client

1. Connect to the SchemaCrawler AI MCP Server in Visual Studio Code (the server is configured in the ".vscode/mcp.json" file)
2. Ask questions about your database in "Agent" mode - here are some examples:
   - "What tables are available in my database?"
   - "Show me the columns in the Books table"
   - "What foreign keys reference the Authors table?"
   - "Are there any design issues with my database schema?"
   - "Write SQL to find books and their authors"
   - "Is there any sensitive data in the database?"
   - "Help me visualize the relations of the Authors table in a visualization tool"
3. Additional agents are provided in this project too. Use the "database-expert" or "sql-query-assistant" agents for fine-tuned help for specific tasks.


## Configure Your Database

1. Stop the SchemaCrawler AI MCP Server
   ```sh
   docker compose -f schemacrawler-mcpserver.yaml down -t0
   ```
2. Configure a connection to your database in the "schemacrawler-mcpserver.yaml" file, and follow the steps above again. See [additional configuration parameters which can be set as environmental variables](https://github.com/schemacrawler/SchemaCrawler-AI/blob/main/schemacrawler-ai-mcpserver/mcp-server-registration.json).


## Use Other MCP Clients

Try other MCP Clients:
- [Microsoft AI Shell](https://learn.microsoft.com/en-us/powershell/utility-modules/aishell/overview?view=ps-modules) for a shell
- ... and more at [Awesome MCP Clients](https://github.com/punkpeye/awesome-mcp-clients)

