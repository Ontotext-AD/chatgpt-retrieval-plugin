# ChatGPT Retrieval Plugin (Ontotext fork)

This is a fork of http://github.com/openai/chatgpt-retrieval-plugin that adds some improvements and resolves
some issues. Follow the instructions in the [README.md](README.md) to install and run the plugin.

# Improvements

The upstream ChatGPT Retrieval Plugin binds to port 8000. The forked version allows you to use a custom port
by setting the environment variable PORT. If unset, the port will be 8000. For example, to use port 8001:

```bash
export PORT=8001
```

The upstream version uses a fixed chunk size of 200. The forked version's chunk size can be configured
by setting the environment variable CHUNK_SIZE. If unset, the chunk size will be 200. For example,
to set a chunk size of 1000:

```bash
export CHUNK_SIZE=1000
```

# Fixes

In the upstream version, when using Weaviate and issuing a delete all request, the plugin will delete not only
the documents but also the corresponding schema. In the forked version we resolve this by recreating the schema
automatically after a delete all operation.

# Simple deployment for testing

In order to run this in a quick prepackaged environment, together with GraphDB, you can use the bundled
`docker-compose.yml`. This will start GraphDB, Weaviate and the retrieval plugin on ports 7200, 8080 and 8000.
Remember to set your GPT key and the `BEARER_TOKEN` in the `docker-compose.yml`, as per our documentation.

Note that logs are set to INFO to prevent log spam. For debugging, please refer to the LOGURU_LEVEL variable.