# SchemaCrawler AI MCP Server Environment Variables

The SchemaCrawler AI MCP Server reads the `SCHCRWLR_*` settings below from the Java process environment. They are not read from Java system properties. In Docker Compose, specify them in the service's `environment` section.

## Database Connection

Set either a nonblank JDBC URL or `SCHCRWLR_SERVER` with any needed connection fields. Without a JDBC URL, the server setting is required to select a connector; host, port, and database are optional. A JDBC URL determines the database and connector; when it is present, `SCHCRWLR_SERVER`, `SCHCRWLR_HOST`, `SCHCRWLR_PORT`, and `SCHCRWLR_DATABASE` are ignored. Credentials are applied separately and may be used with either connection form.

| Environment variable | Purpose and behavior |
| --- | --- |
| `SCHCRWLR_JDBC_URL` | Full JDBC URL. Surrounding whitespace is removed. If blank or unset, the server-and-fields form is used. A URL may contain credentials, so prefer separate credential variables when possible. |
| `SCHCRWLR_SERVER` | SchemaCrawler database connector identifier, such as `postgresql`, `mysql`, or `sqlite`. Trimmed before use. A matching connector and JDBC driver must be available. |
| `SCHCRWLR_HOST` | Database host. Trimmed; a blank value leaves the connector's host default in effect. |
| `SCHCRWLR_PORT` | Database port. A trimmed decimal integer from 1024 through 65535 is used; blank, malformed, or out-of-range values leave the connector's default port in effect. |
| `SCHCRWLR_DATABASE` | Database name or connector-specific database value. Trimmed; a blank value leaves the connector's default in effect. |
| `SCHCRWLR_DATABASE_USER` | Database username. Trimmed; unset or blank supplies an empty username. |
| `SCHCRWLR_DATABASE_PASSWORD` | Database password. Preserved exactly, including whitespace; unset supplies `null`, while explicitly empty supplies an empty password. Treat it as a secret. |

For example, configure individual fields in Docker Compose as follows:

```yaml
environment:
  SCHCRWLR_SERVER: postgresql
  SCHCRWLR_HOST: database.example.invalid
  SCHCRWLR_PORT: "5432"
  SCHCRWLR_DATABASE: example
  SCHCRWLR_DATABASE_USER: ${SCHCRWLR_DATABASE_USER}
  SCHCRWLR_DATABASE_PASSWORD: ${SCHCRWLR_DATABASE_PASSWORD}
```

Provide real credentials through a secret-management mechanism or a local `.env` file that is not committed to source control.

## MCP Server and Schema Settings

| Environment variable | Purpose and behavior |
| --- | --- |
| `SCHCRWLR_INFO_LEVEL` | Amount of schema metadata to retrieve: `minimum`, `standard`, `detailed`, or `maximum`. Defaults to `standard`; unset or unrecognized values also use `standard`. Values are case-sensitive. |
| `SCHCRWLR_OFFLINE_DATABASE` | Path to a serialized offline catalog snapshot. Blank or unset loads the catalog online. When set, catalog loading uses this snapshot; some operational tools may still need a live database connection. |
| `SCHCRWLR_ADDITIONAL_CONFIG` | Additional SchemaCrawler configuration encoded as a JSON object. Blank or unset gives empty additional configuration. Invalid or non-convertible JSON logs a warning and falls back to empty configuration. Do not include secrets. |
| `SCHCRWLR_DATABASE_ALIAS` | Optional trimmed database identity included in MCP instructions and tool results. Blank or unset leaves the alias unset. |
| `SCHCRWLR_DATABASE_DESCRIPTION` | Optional trimmed database description included in MCP instructions and the `about_database` response. Blank or unset leaves the description empty. |
| `SCHCRWLR_MCP_SERVER_TRANSPORT` | MCP transport: `stdio` (default) or `http` (Streamable HTTP). Values are case-sensitive. Blank, unset, `unknown`, or an invalid value uses `stdio`. HTTP transport does not configure authentication. |
| `SCHCRWLR_EXCLUDE_TOOLS` | Comma-separated list of MCP tool names to omit from registration. Names are trimmed, case-sensitive, and deduplicated; empty entries are ignored. Blank or unset excludes no tools. |
| `SCHCRWLR_LOG_LEVEL` | Java logging level. Defaults to `INFO`; values are uppercased before parsing, and blank or invalid values use `INFO`. Java logging names such as `SEVERE`, `WARNING`, `INFO`, `CONFIG`, `FINE`, `FINER`, `FINEST`, `ALL`, and `OFF`, as well as numeric levels, are supported. Surrounding whitespace on a nonblank value is not stripped. |

For offline catalog setup, see [Offline Use](offline-use.md). For complete Docker Compose examples, see the sample `schemacrawler-mcpserver-*.yaml` files in this repository.
