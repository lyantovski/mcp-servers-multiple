# Weather MCP Server (Streamable HTTP)

## Running the MCP Server locally and push image to container registry
Run the following commands
```
cd mcp-servers/weather-mcp-server/src/
uv init
uv venv
uv add mcp
uv run weather.py
```
Run the following commands
```
git clone https://github.com/Azure/azure-mcp.git
cd mcp-servers/weather-mcp-server/src/
```
Run following to build and push image to ACR (or any other container registry):
```
docker build -t myacr.azurecr.io/weather-mcp-server:1.0.0 .
docker push myacr.azurecr.io/weather-mcp-server:1.0.0
```

## Deploy MCP server to AKS cluster
Helm command to deploy release by using Helm chart on this repo (for example we used dev environment):
```
helm upgrade --install mcp-server-weather -n mcp-dev . -f values.yaml -f envs/dev.yaml --set app.version=1.0.0 --set spec.pod.containers.imageName=myacr.azurecr.io/weather-mcp-server:1.0.0
```
To delete release from cluster:
```
helm delete mcp-server-weather -n mcp-dev
```

## Run MCP Inspector to test and debug MCP Server
Open a new terminal window and run the following commands
```
npx @modelcontextprotocol/inspector
```

Open a browser and navigate to http://127.0.0.1:6274

In the URL enter: http://localhost:8001/mcp and click Connect. 




    