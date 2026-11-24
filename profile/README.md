<!-- .github/profile/README.md: the page at https://github.com/agentfront -->

<p align="center">
  <a href="https://agentfront.dev"><img src="https://avatars.githubusercontent.com/u/240770336?s=200&v=4" alt="AgentFront logo" width="88" height="88"></a>
</p>

<h1 align="center">AgentFront</h1>

<p align="center">
  <strong>Open-source TypeScript infrastructure for AI agents and the Model Context Protocol (MCP).</strong><br>
  An MCP server framework · OpenAPI to MCP tools · A sandbox for agent-written code · In-memory semantic search
</p>

<p align="center">
  <a href="https://agentfront.dev">Website</a> ·
  <a href="https://frontmcp.dev">FrontMCP docs</a> ·
  <a href="https://docs.agentfront.dev">Enclave &amp; VectoriaDB docs</a> ·
  <a href="https://discord.gg/53AHnJnmwR">Discord</a> ·
  <a href="mailto:info@agentfront.dev">info@agentfront.dev</a>
</p>

---

AgentFront builds open-source **TypeScript** tools that connect **AI agents** to real software over the **Model Context Protocol (MCP)**. [**FrontMCP**](https://github.com/agentfront/frontmcp) is an **MCP server framework** for TypeScript. [**mcp-from-openapi**](https://github.com/agentfront/mcp-from-openapi) does **OpenAPI to MCP**: it turns Swagger and OpenAPI specs into MCP tools. [**Enclave**](https://github.com/agentfront/enclave) runs the JavaScript an agent writes inside a sandbox, and [**VectoriaDB**](https://github.com/agentfront/vectoriadb) gives agents semantic search in memory, with embeddings computed locally. Every project is Apache-2.0 and published on npm.

## FrontMCP: the TypeScript MCP server framework

[![GitHub stars](https://img.shields.io/github/stars/agentfront/frontmcp?style=flat&logo=github&label=stars)](https://github.com/agentfront/frontmcp)
[![npm @frontmcp/sdk](https://img.shields.io/npm/v/@frontmcp/sdk?style=flat&logo=npm&label=%40frontmcp%2Fsdk)](https://www.npmjs.com/package/@frontmcp/sdk)

**[FrontMCP](https://github.com/agentfront/frontmcp)** lets you write MCP tools, resources and prompts as typed TypeScript classes with Zod schemas, and serves them over the Model Context Protocol. It handles transport, sessions, dependency injection and execution flow, and the same server runs locally and in production on Node.js, Vercel, AWS Lambda and Cloudflare Workers. It serves MCP 2026-07-28, the stateless revision, and the earlier ones.

- **Auth built in:** OAuth 2.1, JWT and session checks, and a credential vault (`@frontmcp/auth`)
- **Testing:** Jest fixtures with a connected MCP client and MCP matchers (`@frontmcp/testing`)
- **OpenAPI adapter:** generate MCP tools from an OpenAPI spec (`@frontmcp/adapters`)
- **Tool UIs:** React widgets for ChatGPT, Claude and other MCP Apps hosts (`@frontmcp/ui`)
- **Plugins:** CodeCall, result caching, per-session memory, human approval gates, feature flags and WebMCP
- **Production:** rate limits and concurrency guards, OpenTelemetry tracing and Prometheus-format metrics

```bash
npx frontmcp create my-mcp-server   # Node.js 24+
```

Learn at [frontmcp.dev](https://frontmcp.dev/learn), try the [browser playground](https://frontmcp.dev/playground), or see how FrontMCP [compares with other TypeScript MCP frameworks](https://frontmcp.dev/compare).

<details>
<summary><b>Give your coding agent the FrontMCP docs</b></summary>
<br>

FrontMCP's own MCP server gives coding agents the docs for the FrontMCP release your project uses ([Docs for Your Agent](https://frontmcp.dev/learn/docs-for-your-agent)). To add it to Claude Code:

```bash
claude mcp add --transport http frontmcp-docs https://frontmcp.dev/mcp
```

</details>

## OpenAPI to MCP and API schema tooling

### [mcp-from-openapi](https://github.com/agentfront/mcp-from-openapi)

[![GitHub stars](https://img.shields.io/github/stars/agentfront/mcp-from-openapi?style=flat&logo=github&label=stars)](https://github.com/agentfront/mcp-from-openapi)
[![npm mcp-from-openapi](https://img.shields.io/npm/v/mcp-from-openapi?style=flat&logo=npm&label=mcp-from-openapi)](https://www.npmjs.com/package/mcp-from-openapi)

Convert Swagger 2.0 and OpenAPI 3.0, 3.1 and 3.2 specs into MCP tool definitions: input and output schemas, plus an explicit mapper that says where each argument goes in the HTTP request.

- Resolves parameter name conflicts across path, query, header, cookie and body, and builds the request with OpenAPI's full serialization rules (`buildHttpRequest()`)
- Emits schemas each client accepts: `target: 'claude' | 'openai' | 'gemini' | 'strict'`
- Loads untrusted specs safely: SSRF protection while resolving `$ref`s, and a one-flag `secureDefaults` mode
- Curates large APIs: OpenAPI Overlays, lint, filters by tag, method and path, token-budget reports, and Arazzo workflows as tools
- Infers MCP tool annotations (read-only, destructive, idempotent) from HTTP methods

```bash
npm install mcp-from-openapi
```

### [openapi-spec](https://github.com/agentfront/openapi-spec) (upcoming)

Up-to-date TypeScript types and readers for OpenAPI 3.2, 3.1, 3.0 and Swagger 2.0. The upcoming **1.0.0** is its first functional release: types for every version, version detection, one walker for the operations of a path item, and a Swagger 2.0 to OpenAPI 3.0 converter. The code is being extracted from mcp-from-openapi, where it is developed and tested against the official OpenAPI JSON Schemas, and a weekly check against the OpenAPI Initiative's published sources flags new spec versions. npm `0.0.1` only reserves the name: [watch the repository](https://github.com/agentfront/openapi-spec) to hear when 1.0.0 ships.

### [json-schema-to-zod-v3](https://github.com/agentfront/json-schema-to-zod-v3)

[![npm json-schema-to-zod-v3](https://img.shields.io/npm/v/json-schema-to-zod-v3?style=flat&logo=npm&label=json-schema-to-zod-v3)](https://www.npmjs.com/package/json-schema-to-zod-v3)

Convert JSON Schema (Draft 7+) to Zod v3 validation schemas in TypeScript, with ReDoS protection for `pattern` on by default.

```bash
npm install json-schema-to-zod-v3 zod@^3.23.8
```

## Secure code execution and semantic search for AI agents

### [Enclave](https://github.com/agentfront/enclave)

[![GitHub stars](https://img.shields.io/github/stars/agentfront/enclave?style=flat&logo=github&label=stars)](https://github.com/agentfront/enclave)
[![npm @enclave-vm/core](https://img.shields.io/npm/v/@enclave-vm/core?style=flat&logo=npm&label=%40enclave-vm%2Fcore)](https://www.npmjs.com/package/@enclave-vm/core)

A sandbox for JavaScript written by AI agents. Enclave checks AgentScript, the subset of JavaScript a model writes to call your tools, rewrites it so that limits can be enforced, and runs it where it reaches only the globals and tools you give it, with limits on time, iterations, tool calls and memory. Packages cover Node.js, the browser (nested sandboxed iframes), and a streaming layer that runs scripts behind HTTP routes, with a client and React hooks.

```bash
npm install @enclave-vm/core
```

[Docs](https://docs.agentfront.dev/enclave/getting-started/welcome) · [Live playground](https://enclave.agentfront.dev)

### [VectoriaDB](https://github.com/agentfront/vectoriadb)

[![npm vectoriadb](https://img.shields.io/npm/v/vectoriadb?style=flat&logo=npm&label=vectoriadb)](https://www.npmjs.com/package/vectoriadb)

A lightweight in-memory vector database for semantic search in TypeScript. Embeddings run locally with transformers.js, so your data stays on your server and there is no API quota. HNSW indexing, typed metadata filters, file and Redis persistence, and a zero-dependency TF-IDF mode.

```bash
npm install vectoriadb
```

[Docs](https://docs.agentfront.dev/vectoriadb/get-started/welcome)

## How the pieces fit together

FrontMCP builds on the libraries: its OpenAPI adapter (`@frontmcp/adapters`) runs on mcp-from-openapi, and its CodeCall plugin (`@frontmcp/plugin-codecall`) finds tools with VectoriaDB and runs the scripts a model writes in Enclave. Each library is also a standalone npm package that works without FrontMCP.

## Get started

- **Building an MCP server?** Follow [Learn FrontMCP](https://frontmcp.dev/learn), or try it first in the [playground](https://frontmcp.dev/playground).
- **Have an OpenAPI spec?** Read [Getting Started with mcp-from-openapi](https://github.com/agentfront/mcp-from-openapi/blob/main/docs/getting-started.md).
- **Running code a model wrote?** Start with the [Enclave docs](https://docs.agentfront.dev/enclave/getting-started/welcome).
- **Need search over tools or documents?** Start with the [VectoriaDB docs](https://docs.agentfront.dev/vectoriadb/get-started/welcome).

## Contribute

Issues and pull requests are welcome in every repository. Read the repository's contributing guide first, for example [FrontMCP's](https://github.com/agentfront/frontmcp/blob/main/CONTRIBUTING.md) or [mcp-from-openapi's](https://github.com/agentfront/mcp-from-openapi/blob/main/CONTRIBUTING.md). Report vulnerabilities privately, as the repository's `SECURITY.md` describes or by email to [info@agentfront.dev](mailto:info@agentfront.dev), never in a public issue. For questions and ideas, join the [Discord](https://discord.gg/53AHnJnmwR).

If one of these projects saves you time, a star helps other developers find it.

---

<p align="center">
  <a href="https://agentfront.dev">agentfront.dev</a> ·
  <a href="https://frontmcp.dev">frontmcp.dev</a> ·
  <a href="https://docs.agentfront.dev">docs.agentfront.dev</a> ·
  <a href="https://discord.gg/53AHnJnmwR">Discord</a> ·
  <a href="mailto:info@agentfront.dev">info@agentfront.dev</a>
</p>
