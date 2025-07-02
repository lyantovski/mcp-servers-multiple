# Multiple MCP Servers on AKS

This folder contains two MCP servers Helm charts and KAITO Workspace CRDs: 

Azure MCP server using SSE (Server-Sent Events) HTTP Transport and Weather MCP Server using Streamable HTTP transport 

**Read the Blog Posts**: 
- Part 1: https://medium.com/@lioryantovski/running-mcp-clients-on-aks-connecting-to-both-aks-based-and-remote-mcp-servers-part-1-416c89f0b3de
- Part 2: https://medium.com/@lioryantovski/running-mcp-clients-on-aks-connecting-to-both-aks-based-and-remote-mcp-servers-part-2-8ce7f57d78bb

## Project folders
- `mcp-servers`: 
   - azure-mcp-server: Azure MCP server using SSE (/sse endpoint)
   - weather-mcp-server: Weather MCP Server using Streamable HTTP (/mcp endpoint)
- `kaito`: Workspace CRD files for differnet steps of using KAITO
   - Creating inference endpoint for LLM model "phi-4-mini-instruct"
   - Running fine-tuning on LLM model "phi-4-mini-instruct" with parquet file with sample data about KAITO itself, located on HuggingFace
   - Creating inference endpoint for LLM model "phi-4-mini-instruct" with container "adapter" created on step before