# Offline Use

## Overview

SchemaCawler can generate serialized snapshots of your database schema metadata, and load them from disk even when a connection to your database is not available. This technique is useful when you want to use the SchemaCrawler AI MCP Server but do not have access to connect to your database. You will notice that SchemaCawler loads faster when loading this offline snapshot, so you can use the technique for quick start-up even if you do have access to your database server.


## Create a snapshot

First, create a serialized snapshot of your database schema metadata. 

Run a command similar to:

```sh
docker run -it \
  --rm \
  -v ".:/home/schcrwlr/share" \
  --name schemacrawler-ai \
  --entrypoint /bin/bash \
  schemacrawler/schemacrawler-ai \
    /opt/schemacrawler/bin/schemacrawler.sh \
      --server sqlite \
      --database sc.db \
      --info-level maximum \
      --command serialize \
      --output-file share/sc.ser
```

Modify the connection arguments to suit your needs. It is recommended to use the maximum info-level so that you the serialized snapshot has as much data as possible, but you can tailor it to your needs.

(If you are running the Docker command in Powershell, replace the line continuation character "\" with "`".)

You will find the serialized snapshot file on your local disk.


## Start SchemaCrawler AI MCP Server with the Offline snapshot

Modify the following environmental variables in your "schemacrawler-mcpserver.yaml" Docker Compose file:

- `SCHCRWLR_SERVER` to `offline`
- `SCHCRWLR_OFFLINE_DATABASE` to `share/sc.ser`

Run `docker compose -f schemacrawler-mcpserver.yaml up -d` but make sure that the "sc.ser" file is in the same working directory that you run the Docker command from.
