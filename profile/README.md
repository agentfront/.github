<!-- .github/profile/README.md -->

<h1 align="center">AgentFront</h1>

<p align="center">
  <strong>Open-source TypeScript building blocks for AI agents.</strong><br/>
  A framework for MCP servers • A sandbox for the code agents write • A vector database that runs in memory
</p>

<p align="center">
  <a href="https://frontmcp.dev">FrontMCP docs</a> ·
  <a href="https://github.com/agentfront/frontmcp">FrontMCP</a> ·
  <a href="https://docs.agentfront.dev">EnclaveVM &amp; VectoriaDB docs</a> ·
  <a href="https://github.com/agentfront/frontmcp/issues">Issues</a> ·
  <a href="https://github.com/agentfront/frontmcp/releases">Releases</a>
</p>

---

## Projects

| Project | What it is | Docs |
| --- | --- | --- |
| [FrontMCP](https://github.com/agentfront/frontmcp) | The TypeScript framework for MCP servers | [frontmcp.dev](https://frontmcp.dev) |
| [EnclaveVM](https://github.com/agentfront/enclave) | A JavaScript sandbox for running the code AI agents write | [docs.agentfront.dev](https://docs.agentfront.dev/enclave/getting-started/welcome) |
| [VectoriaDB](https://github.com/agentfront/vectoriadb) | An in-memory vector database for semantic search, with offline embeddings | [docs.agentfront.dev](https://docs.agentfront.dev/vectoriadb/get-started/welcome) |

Also: [mcp-from-openapi](https://github.com/agentfront/mcp-from-openapi), which turns OpenAPI specs into MCP tools, and [json-schema-to-zod-v3](https://github.com/agentfront/json-schema-to-zod-v3), which turns JSON Schema into Zod v3 schemas.

## What is FrontMCP?

**FrontMCP** is our TypeScript framework for building servers that speak the **Model Context Protocol (MCP)**—the emerging standard for connecting LLM apps to tools, data, and services. FrontMCP focuses on developer joy and production pragmatism:

- **TypeScript-first DX** — strong types, Zod schemas, ergonomic decorators
- **Composable architecture** — plugins, adapters, resources, and tools with clear metadata
- **Secure, scoped execution** — DI-powered invoker with per-tool access views and consent
- **Modern transports** — Streamable HTTP, SSE compatibility, and session management
- **Great ergonomics** — clean logging, hooks, and structured flow control

> If you’re building an AI IDE, copilots, or custom workflows, FrontMCP gives you the fastest path from **idea → MCP server**.

## Learn and build

- **The docs** are at [frontmcp.dev](https://frontmcp.dev): lessons, the reference, examples and comparisons. Every example runs in your browser.
- **Docs for your agent:** FrontMCP's own MCP server gives coding agents those docs, for the FrontMCP release your project uses. See [Docs for Your Agent](https://frontmcp.dev/learn/docs-for-your-agent), or add it to Claude Code:

  ```bash
  claude mcp add --transport http frontmcp-docs https://frontmcp.dev/mcp
  ```

- **Start a server:**

  ```bash
  npx frontmcp create my-mcp-server
  ```
