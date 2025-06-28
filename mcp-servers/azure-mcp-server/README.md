# Azure MCP Server (SSE)

Source: https://github.com/Azure/azure-mcp

Full README: https://github.com/Azure/azure-mcp/blob/main/README.md

## Running the MCP Server locally and push image to container registry
Run the following commands
```
git clone https://github.com/Azure/azure-mcp.git
cd azure-mcp/
```
Copy Dockerfile from this repo to folder azure-mcp/ and run following to build and push image to ACR (or any other container registry):
```
docker build -t myacr.azurecr.io/azure-mcp-server:1.0.0 .
docker push myacr.azurecr.io/azure-mcp-server:1.0.0
```
## Running the MCP Server on Azure
In order to run locally or on AKS, please prepare Service Principal(SP) identity (for example: azure-mcp-sp as below):
```
az ad sp create-for-rbac --name azure-mcp-sp --query 'password' --output tsv --skip-assignment
```
Add assignment to SP with relevant Role(we used Contributor for simplicity of this demo, but it can be with lower permissions of course) on Subscription scope.

Pay attention to following settings need to be configured as environment variables on Helm chart or by running docker image localy.
Note: recommended to use integration with Azure KeyVault and keep secrets there and retrieve them by Azure KeyVault CSI driver to AKS!
```
AZURE_TENANT_ID=
AZURE_CLIENT_ID=
AZURE_CLIENT_SECRET=
```
## Deploy MCP server to AKS cluster
Helm command to deploy release by using Helm chart on this repo (for example we used dev environment):
```
helm upgrade --install azure-mcp-server -n mcp-dev . -f values.yaml -f envs/dev.yaml --set app.version=1.0.0 --set spec.pod.containers.imageName=myacr.azurecr.io/azure-mcp-server:1.0.0
```
To delete release from cluster:
```
helm delete azure-mcp-server -n mcp-dev
```
## Configure MCP server on clients
You can configure Azure MCP server on Librechat or other clients:
```
  mcp-azure-server:
    type: "sse"
	url: http://azure-mcp-server.mcp-dev.svc.cluster.local:5008/sse
```

## Run MCP Inspector to test and debug MCP Server
Open a new terminal window and run the following commands
```
npx @modelcontextprotocol/inspector
```

Open a browser and navigate to http://127.0.0.1:6274

In the URL enter: http://localhost:5008/sse and click Connect. 




    