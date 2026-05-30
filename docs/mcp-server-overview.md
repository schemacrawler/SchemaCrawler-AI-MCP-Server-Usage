# SchemaCrawler AI MCP Server Overview

Model Context Protocol (MCP) servers let AI clients call specialized tools through a standard interface. The SchemaCrawler AI MCP Server provides schema-aware database analysis capabilities so you can explore metadata, understand relationships, and generate SQL with grounded context.

## What This Server Helps You Do

- Discover tables, columns, routines, and other schema objects
- Inspect foreign keys and table relationships
- Detect schema design issues using lint-focused checks
- Generate SQL with awareness of actual schema metadata
- Support documentation and governance workflows with repeatable analysis

## Images

The server is available through:
- Docker MCP Catalog image: https://hub.docker.com/r/mcp/schemacrawler-ai
- Early-release image: https://hub.docker.com/repository/docker/schemacrawler/schemacrawler-ai

## Full Usage Documentation

For setup instructions, Docker Compose examples, Visual Studio Code MCP client usage, and offline snapshot workflows, see this repository's guides:

- Getting Started
- Offline Use
- Docker MCP Gateway

Additional configuration parameters for server environment variables:

- https://github.com/schemacrawler/SchemaCrawler-AI/blob/main/schemacrawler-ai-mcpserver/mcp-server-registration.json

## Example Questions to Ask in Agent Mode

- What tables are available in this database?
- Which tables reference Customers?
- Show potential schema design issues in this schema.
- Draft a query to list orders with customer and shipment status.

## Related

- SchemaCrawler website: https://www.schemacrawler.com
- SchemaCrawler project: https://github.com/schemacrawler/SchemaCrawler
