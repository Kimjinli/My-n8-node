# n8n Workflow AI Agent Instructions

## Project Overview
This is a **n8n automation platform** repository storing workflow definitions as JSON exports. n8n is a visual workflow automation tool that enables integration across 400+ services (webhooks, databases, APIs, SaaS platforms, etc.) without custom code.

## Repository Structure
- **`workflows/`** - Exported workflow JSON files (one per workflow). Each file contains complete workflow definition including nodes, connections, and configuration.
- **`developer-note.md`** - Korean language guide documenting n8n basics and workflow export/import procedures.
- **`README.md`** - High-level project description.

## Core Concepts
- **Nodes** - Individual action/trigger blocks (Webhook, Respond to Webhook, HTTP requests, database operations, etc.).
- **Connections** - Data flow between nodes. Output from one node feeds into inputs of downstream nodes.
- **Workflow** - Complete automation sequence with a unique ID and JSON representation.

## Example Workflow Structure
The existing workflow `GDiYDb8MuGahJrlQq7oZa.json` is a minimal Webhook → Response pattern:
```json
{
  "nodes": [
    {"type": "n8n-nodes-base.webhook", "parameters": {"httpMethod": "POST", "path": "hello-n8n", ...}},
    {"type": "n8n-nodes-base.respondToWebhook", "parameters": {"responseBody": "응답 응답 응답 ! "}}
  ],
  "connections": {"Webhook": {"main": [[{"node": "Respond to Webhook", ...}]]}}
}
```

## Critical Developer Workflows

### Exporting Workflows to Git
```bash
# Export all active workflows to JSON files
n8n export:workflow --all --output=./workflows/
```

### Testing Webhook Workflows
1. Activate "Listen for Test Event" in n8n UI for the webhook node
2. Use curl to send test data:
```bash
curl -X POST https://YOUR-WEBHOOK-URL/path \
     -H "Content-Type: application/json" \
     -d '{"key": "value"}'
```

### Starting/Stopping n8n
```bash
# Terminal: Start n8n instance
n8n start

# To stop: Ctrl + C
```

## Project-Specific Conventions
- **Workflow naming** - Use descriptive names reflecting the automation purpose (currently "My workflow" needs renaming).
- **Korean documentation** - Developer notes are in Korean; maintain this language in comments/docs.
- **HTTP method preference** - Webhooks default to POST for data ingestion patterns.
- **Response mode** - Use `responseMode: "responseNode"` to explicitly control webhook responses.

## Common Patterns
- **Webhook trigger** → Parse/transform data → Response or downstream action
- All workflows must have clear input/output specifications in workflow description
- Store active automation workflows; archive deprecated ones (use `isArchived` flag)

## Integration Points
- External services connected via HTTP nodes, OAuth, or webhooks
- Database operations for data persistence
- Notion integration (developer-note.md mentions Notion as primary data destination, though not yet implemented in workflows)

## When Adding Workflows
1. Create new workflow in n8n UI
2. Export with `n8n export:workflow --all --output=./workflows/`
3. Commit JSON to git with meaningful workflow names
4. Update workflow description field with purpose/trigger details
