# Azure MCP Server

## Running the MCP Server locally 
Run the following commands
```
cd mcp-servers/weather-mcp-sse/src/
uv init
uv venv
uv add mcp
uv run weather.py
```

## Run MCP Inspector to test and debug MCP Server
Open a new terminal window and run the following commands
```
npx @modelcontextprotocol/inspector
```

Open a browser and navigate to http://127.0.0.1:6274

In the URL enter: http://localhost:8001/mcp and click Connect. 




    