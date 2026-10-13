---
name: external-cli-tools
description: Lists the CLIs installed in this environment and when to use each one instead of its MCP equivalent. Use before calling an MCP tool for Vercel (deployment status, project management, environment variables) or any other service that also has a CLI listed here.
---

# External CLI tools

Rule: if you already know the operation you need, run the CLI. Use the MCP server only to discover what exists or when the CLI lacks the operation.

## Vercel (`vercel`)

Use instead of the Vercel MCP (`mcp__vercel__*`) for:

| Need | Command |
|------|---------|
| Deployment / dev status | `vercel ls` |
| Inspect one deployment | `vercel inspect <url>` |
| Project management | `vercel project ls`, `vercel project add`, `vercel project rm` |
| List env vars | `vercel env ls` |
| Add / remove env var | `vercel env add <name> <environment>`, `vercel env rm <name>` |
| Pull env vars locally | `vercel env pull` |

Fall back to the Vercel MCP only when you do not know which operation you need (exploring teams, projects, domains, logs) or the CLI has no matching command.

Never print env var values in output.

---

Add new CLIs below as `## <tool> (`<binary>`)` with the same table: need, command.
