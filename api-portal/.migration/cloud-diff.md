# API Portal & MCP Hub: Cloud pages against the main line

The main line is seeded from the newest Self-hosted line; pages found only in the Cloud sub-section are added and marked Cloud only (Platform-by-platform walkthrough, rule 4). A Cloud page with the same name as a main-line page is **not** added: the main line keeps its own text, and the Cloud page's legacy URL maps to it. This report lists those pairs so the team can decide each one by PR. Converted from `wso2/docs-api-platform@e9987cde09f3f6859357429a051aa04ee461c13b`.

- Pairs: 2 (0 identical, **2 differ**)
- Cloud-only pages added: 13
- Cloud-only pages whose file name several pages share (possible counterparts, not paired): 0

| Cloud page (legacy) | Main-line page | Paired by | Word F1 | Lines +/− | |
|---|---|---|---|---|---|
| [cloud/devportal/admin-settings/llm-instructions.md](https://wso2.com/api-platform/docs/cloud/devportal/admin-settings/llm-instructions/) | `docs/guides/admin-settings/content/llm-instructions.mdx` (from api-portal/next/admin-settings/llm-instructions.md) | same path | 0.467 | +25 / −45 | **differs** |
| [cloud/devportal/discover-apis/ai-agent-discovery.md](https://wso2.com/api-platform/docs/cloud/devportal/discover-apis/ai-agent-discovery/) | `docs/guides/ai-agent-discovery.mdx` (from api-portal/next/ai-agent-discovery.md) | same file name | 0.617 | +46 / −76 | **differs** |

## Differences

Each diff reads from the main-line text (`-`) to the Cloud text (`+`), front matter left out.

### cloud/devportal/admin-settings/llm-instructions.md

Main-line page `docs/guides/admin-settings/content/llm-instructions.mdx`; word F1 0.467.

<details><summary>Diff</summary>

```diff
--- main line: api-portal/next/admin-settings/llm-instructions.md
+++ Cloud: cloud/devportal/admin-settings/llm-instructions.md
@@ -1,65 +1,45 @@
-# LLM instructions
+# LLM Instructions
 
-**LLM Instructions** controls how AI agents see your portal as a whole. The name refers to large language models (LLMs), the systems behind those agents. It sets the name and description at the top of `llms.txt`—the first thing an agent reads before it navigates anything else—and carries the switch that turns AI discoverability on or off for the entire portal.
+LLM Instructions allow portal admins to provide AI agents with high level context about the developer portal, what APIs are available, how the portal is organized, and any conventions or constraints agents should follow when interacting with it.
 
-Everything on this page is scoped to one [view](manage-views.md). Use the view selector to switch.
+These instructions are published as part of the portal's `llms.txt` file, which is the primary entry point for AI agents discovering the portal's capabilities.
 
-## Open the page
+## What Are LLM Instructions?
 
-Go to **Settings** and select **LLM Instructions** under **AI & DISCOVERY**.
+LLM Instructions are free form natural language text written by the portal admin. They appear at the top of `llms.txt` and are read by agents before they navigate the rest of the portal's content.
 
-The page puts the editable fields beside a live preview of the file they produce:
+Use this space to tell agents:
 
-![LLM Instructions page with the AI-discoverable toggle, portal name and description fields, and a live llms.txt preview](../../../assets/img/devportal/llm-instructions.png)
-
-## Turn AI discoverability on or off
-
-The **Portal is AI-discoverable** card at the top shows the view's live `llms.txt` path and a toggle.
-
-Switching it off makes every agent-facing endpoint return `404`—`llms.txt` itself, the API and MCP catalogs, per-artifact Markdown, raw specifications, and every workflow endpoint. It overrides each artifact's own agent-visibility setting, so nothing reaches an agent while it's off.
-
-The **Publish** button stays clickable when the toggle is off, so you can save the change.
-
-## Set the portal identity
+- What the portal covers and what kind of APIs it exposes
+- How APIs are organized (by product area, team, lifecycle stage, etc.)
+- Any authentication conventions agents should be aware of
+- Which workflows are the recommended starting points for common tasks
+- Any limitations or usage policies agents should respect
 
-Two fields make up the instructions, and both appear verbatim at the top of `llms.txt`.
+Well written LLM instructions reduce agent errors and improve the quality of AI-assisted integrations by giving agents the orientation they need upfront, rather than leaving them to infer context from individual API specs.
 
-| Field | What it does |
-|---|---|
-| **Portal name** | Replaces the default `{orgName} API Portal` heading |
-| **Description** | The paragraph below the name. This is the orientation text agents read first |
 
-The description is a free-text area, not a one-liner. Use it for the context an agent can't infer from individual API specs:
+## Configuring LLM Instructions
 
-- What the portal covers and what kinds of APIs it exposes
-- How the catalog is organized—by domain, team, or lifecycle stage
-- Authentication conventions that apply across APIs
-- Which workflows are the recommended starting points for common tasks
-- Usage policies or limitations agents should respect
+LLM Instructions are configured at the portal (view) level in the admin settings.
 
-Leave either field empty and the portal falls back to its defaults: `{orgName} API Portal` for the heading, and a generic one-line description.
+1. Log in to the Developer Portal as an admin and navigate to **Admin Settings**.
+2. Select **LLM Instructions** tab.
+3. Enter your instructions in the text editor.
+4. Click **Publish**.
 
-Click **Publish** to save. Changes take effect immediately—the next request for `llms.txt` reflects them.
+![LLM Instructions page with Portal Identity fields, text editor, and Publish button](../../../assets/img/devportal/llm-instructions.png)
 
-## Preview the result
+Changes take effect immediately, the updated instructions are reflected in `llms.txt` as soon as you save.
 
-The pane beside the fields renders the `llms.txt` your settings produce, and refreshes as you type, so you can see the header in context above the generated API and workflow index. The icon in its corner opens the live `llms.txt` in a new tab.
+## Previewing the Output
 
-To fetch it yourself:
+To verify how your instructions appear to agents, fetch the portal's `llms.txt` directly:
 
 ```text
-GET /api-portal/{orgName}/views/{viewName}/llms.txt
+GET /{orgName}/views/{viewName}/llms.txt
 ```
 
-The generated file lists each agent-visible artifact under its own section:
-
-![Generated llms.txt showing an API Workflows section with workflow names, descriptions, and links](../../../assets/img/devportal/llms-txt.png)
-
-Only your name and description are editable. Everything below them—the API Workflows, APIs, MCPs, GraphQL, WebSocket, and WebSub sections—is generated from the catalog and reflects each artifact's own agent visibility. See [AI Agent Discovery](../ai-agent-discovery.md) for how that index is built.
-
-## Related
+Your LLM Instructions will appear at the top of the file, followed by the portal's API and workflow index.
 
-- [AI Agent Discovery](../ai-agent-discovery.md): every agent-facing endpoint, and what `llms.txt` contains
-- [Managing API Workflows](manage-api-workflows.md): per-workflow agent visibility
-- [Make an API AI-Ready](../../../cloud/develop-api-proxy/make-api-ai-ready.md): per-API agent visibility, and writing descriptions agents can use
-- [Manage Views](manage-views.md): why these settings are per-view
+![llms.txt file showing API Workflows section with workflow names, descriptions, and spec links](../../../assets/img/devportal/llms-txt.png)
```

</details>

### cloud/devportal/discover-apis/ai-agent-discovery.md

Main-line page `docs/guides/ai-agent-discovery.mdx`; word F1 0.617.

<details><summary>Diff</summary>

```diff
--- main line: api-portal/next/ai-agent-discovery.md
+++ Cloud: cloud/devportal/discover-apis/ai-agent-discovery.md
@@ -1,118 +1,88 @@
-# AI agent API discovery
+# AI Agent API Discovery
 
-The API Portal & MCP Hub has built-in support for AI agent discoverability. Every published API, MCP server, and API workflow is exposed through a set of machine-readable endpoints that AI agents, large language model (LLM)-powered assistants, and agentic frameworks can use to discover, understand, and invoke them without human assistance.
+API Platform's Developer Portal has built-in support for AI agent discoverability. Every published API is automatically exposed through a set of machine readable endpoints that AI agents, LLM powered assistants, and agentic frameworks can use to discover, understand, and invoke APIs without human assistance.
 
-This page explains what those endpoints return and how agents navigate the portal.
+This page explains how those endpoints work and how agents navigate the portal.
 
-Every endpoint below is scoped to an organization handle (`{orgName}`) and a [view](admin-settings/manage-views.md) (`{viewName}`, which is `default` unless an admin has created more views). Responses are plain text or JSON, so agents can fetch them without authentication, JavaScript rendering, or a browser. Only discovery is unauthenticated—invoking an API or MCP server still requires its credentials, a subscription where one applies, and the scopes it declares.
+## `llms.txt`: The Entry Point for Agents
 
-## `llms.txt`: The entry point for agents
-
-The portal generates an `llms.txt` file on every request—a Markdown index designed as the entry point for AI agents. It gives a structured overview of everything the portal exposes for AI consumption.
+The portal dynamically generates an `llms.txt` file — a plain-text Markdown index designed as the entry point for AI agents. It provides a structured overview of everything the portal exposes for AI consumption.
 
 **Endpoint:**
 
 ```text
-GET /api-portal/{orgName}/views/{viewName}/llms.txt
+GET /{orgName}/views/{viewName}/llms.txt
 ```
 
-The file opens with the portal's name and description, both configured through [LLM Instructions](admin-settings/llm-instructions.md). It then lists every agent-visible artifact, grouped into the following sections, with each entry linking to that artifact's own Markdown document:
+**What it contains:**
 
-| Section | Contains |
-|---|---|
-| API Workflows | Published, agent-visible workflows, each linking to `/api-workflows/{handle}.md` |
-| APIs | REST APIs, each linking to `/api/{apiHandle}.md` |
-| MCPs | MCP servers, each linking to `/mcp/{apiHandle}.md` |
-| GraphQL APIs | GraphQL APIs, each linking to `/api/{apiHandle}.md` |
-| Async / WebSocket APIs | WebSocket APIs, each linking to `/api/{apiHandle}.md` |
-| WebSub APIs | WebSub APIs, each linking to `/api/{apiHandle}.md` |
+- The portal's name, description, and any LLM Instructions configured by the portal admin
+- A list of all agent visible APIs, each with its name, description, and a link to its Markdown documentation
+- A list of all published, agent visible API Workflows
 
-A section is omitted when it holds no agent-visible artifacts. An agent that starts at `llms.txt` therefore learns the full scope of the catalog without crawling the portal, which makes it the standard starting point for LLM-native API consumption.
+An agent or agentic framework that starts at `llms.txt` immediately understands the scope of available APIs and workflows without crawling the entire portal. This makes it the standard starting point for LLM native API consumption.
 
 !!! tip
-    Portal admins set the name and description that head `llms.txt` under [LLM Instructions](admin-settings/llm-instructions.md). The same page carries the toggle that turns AI discoverability on or off for the whole portal.
+    Portal admins can enrich `llms.txt` with high-level guidance for agents such as how APIs are organized, common authentication patterns, and recommended workflows using [LLM Instructions](../admin-settings/llm-instructions.md).
+
+---
 
-## Machine-readable endpoints
+## Machine Readable API Endpoints
 
-Beyond `llms.txt`, the portal serves its catalog, documentation, and specifications as Markdown and raw specification files.
+Beyond `llms.txt`, the portal exposes all content as clean Markdown and raw specification files. These endpoints require no authentication, no JavaScript rendering, and no browser. Therefore, agents can fetch them reliably as plain text.
 
-### API and MCP server catalogs
+### API Catalog and Per API Documentation
 
 | Endpoint | Description |
 |---|---|
-| `/api-portal/{orgName}/views/{viewName}/apis.md` | Every agent-visible API, grouped by type, as a single Markdown document |
-| `/api-portal/{orgName}/views/{viewName}/mcps.md` | Every agent-visible MCP server as a single Markdown document |
+| `/{orgName}/views/{viewName}/apis.md` | All agent-visible APIs as a single Markdown document |
+| `/{orgName}/views/{viewName}/api/{apiHandle}.md` | Full documentation for a specific API in Markdown, including description, documents, and a link to the specification |
 
-### Per-API and per-MCP-server documentation
+### API Specifications
 
 | Endpoint | Description |
 |---|---|
-| `/api-portal/{orgName}/views/{viewName}/api/{apiHandle}.md` | Full documentation for one API, in Markdown |
-| `/api-portal/{orgName}/views/{viewName}/mcp/{apiHandle}.md` | Full documentation for one MCP server, in Markdown |
-| `/api-portal/{orgName}/views/{viewName}/api/{apiHandle}/docs/{docType}/{docName}.md` | One attached document, as the raw Markdown the publisher uploaded |
-| `/api-portal/{orgName}/views/{viewName}/mcp/{apiHandle}/docs/{docType}/{docName}.md` | The same, for an MCP server |
-
-A per-API Markdown document is self-contained. It carries:
-
-- The name, version, description, type, production and sandbox endpoints, tags, and labels
-- A subscription plan table listing each plan's rate limits
-- Step-by-step authentication instructions for the API's security scheme: OAuth2, API key, or a statement that the API needs no credentials
-- Links to every attached document, pointing at the raw Markdown endpoints above
-- The full API specification, inlined in a fenced code block, with the live endpoint URLs substituted in
+| `/{orgName}/views/{viewName}/api/{apiHandle}/docs/specification.json` | OpenAPI or AsyncAPI specification (JSON) |
+| `/{orgName}/views/{viewName}/api/{apiHandle}/docs/specification.graphql` | GraphQL schema |
+| `/{orgName}/views/{viewName}/api/{apiHandle}/docs/specification.xml` | SOAP specification (WSDL/XML) |
 
-An agent that fetches this one document usually has everything it needs to make a call.
+### MCP Server Catalog
 
-### API specifications
-
-The specification format follows the API type, so each API serves exactly one extension. Requesting any other extension returns `404`.
-
-| API type | Endpoint | Format |
-|---|---|---|
-| REST | `/api-portal/{orgName}/views/{viewName}/api/{apiHandle}/docs/specification.json` | OpenAPI (JSON) |
-| WebSocket, WebSub | `/api-portal/{orgName}/views/{viewName}/api/{apiHandle}/docs/specification.json` | AsyncAPI (JSON) |
-| GraphQL | `/api-portal/{orgName}/views/{viewName}/api/{apiHandle}/docs/specification.graphql` | GraphQL schema (SDL) |
-| SOAP | `/api-portal/{orgName}/views/{viewName}/api/{apiHandle}/docs/specification.xml` | WSDL (XML) |
-| MCP server | `/api-portal/{orgName}/views/{viewName}/mcp/{apiHandle}/docs/specification.json` | Tool, resource, and prompt schema (JSON) |
-
-For REST, WebSocket, and WebSub APIs, the portal substitutes the API's live production and sandbox URLs into the specification it serves, so an agent doesn't have to resolve placeholder server entries.
+| Endpoint | Description |
+|---|---|
+| `/{orgName}/views/{viewName}/mcps` | MCP server catalog page |
+| `/{orgName}/views/{viewName}/mcp/{apiHandle}.md` | Full documentation for a specific MCP server in Markdown |
+| `/{orgName}/views/{viewName}/mcp/{apiHandle}/docs/specification.json` | MCP server specification |
 
-### API workflows
+### API Workflows
 
 | Endpoint | Description |
 |---|---|
-| `/api-portal/{orgName}/views/{viewName}/api-workflows.md` | Every published, agent-visible workflow as a single Markdown document |
-| `/api-portal/{orgName}/views/{viewName}/api-workflows/{handle}.md` | One workflow rendered as Markdown, including its steps and links to the APIs it calls |
-| `/api-portal/{orgName}/views/{viewName}/api-workflows/{handle}/arazzo.json` | The raw [Arazzo](https://spec.openapis.org/arazzo/latest.html) specification for one workflow |
-| `/api-portal/{orgName}/views/{viewName}/api-workflows/{handle}/prompt` | A JSON object holding the workflow's agent prompt, description, raw content, and source APIs |
+| `/{orgName}/views/{viewName}/api-workflows.md` | All published, agent-visible workflows as a single Markdown document |
+| `/{orgName}/views/{viewName}/api-workflows/{handle}/arazzo.json` | Machine readable Arazzo specification for a specific workflow |
 
-The `arazzo.json` endpoint returns `404` for a non-Arazzo workflow.
 
-## How agents navigate the portal
+## How Agents Navigate the Portal
 
 A typical agent discovery flow looks like this:
 
-1. **Start at `llms.txt`.** The agent fetches the portal's `llms.txt` for an overview of the available APIs, MCP servers, and workflows.
-2. **Browse a catalog.** If the index isn't detailed enough, the agent fetches `apis.md` or `mcps.md` to read every description at once.
-3. **Retrieve per-artifact documentation.** Once the agent identifies a relevant API, it fetches `/api/{apiHandle}.md` for the endpoints, authentication steps, plans, and inlined specification.
-4. **Read an attached document.** For prose the specification can't express—a getting-started guide, an authentication walkthrough, known limitations—the agent follows the document links in that Markdown file.
-5. **Fetch the specification separately.** When the agent needs the specification as a parseable file rather than as inlined text, it retrieves the `specification.*` endpoint for the API's type.
-6. **Follow a workflow.** If a published workflow matches the task, the agent retrieves the Arazzo specification and agent prompt, then follows a vetted, step-by-step call sequence instead of reasoning from scratch.
+1. **Start at `llms.txt`** — the agent fetches the portal's `llms.txt` to get an overview of available APIs and workflows.
+2. **Browse the API catalog** — if the agent needs more detail, it fetches `apis.md` to read descriptions of all APIs at once.
+3. **Retrieve per API documentation** — once the agent identifies a relevant API, it fetches `/{orgName}/views/{viewName}/api/{apiHandle}.md` for full documentation.
+4. **Fetch the specification** — the agent retrieves the OpenAPI, GraphQL, or AsyncAPI specification for the precise endpoint and parameter details needed to make a call.
+5. **Follow a workflow** — if a published workflow matches the task, the agent retrieves the Arazzo specification and agent prompt to follow a vetted, step-by-step call sequence rather than reasoning from scratch.
 
-The **Try with AI** button on an [API's overview page](discover-apis/browse-apis.md#open-an-api) hands this flow to an agent directly. It produces a prompt that points the agent at that API's `.md` URL and asks it to summarize the API before doing anything else.
 
-## Visibility controls
+## Visibility Controls
 
-Three separate controls decide what agents see:
+By default, all published APIs and MCP servers are agent-visible. API publishers can hide specific APIs from agent-facing surfaces without affecting their visibility to human users in the portal. Portal admins can also disable AI discoverability across the entire portal.
 
-- **Per-artifact agent visibility.** All published APIs, MCP servers, and workflows are agent-visible by default. Setting an artifact to hidden removes it from `llms.txt`, the catalogs, and every Markdown and specification endpoint, while leaving it visible to human users in the portal. For APIs, see [Make an API AI-Ready](../../cloud/develop-api-proxy/make-api-ai-ready.md). For workflows, see [Managing API Workflows](admin-settings/manage-api-workflows.md).
-- **Portal-wide AI discoverability.** Turning off **Portal is AI-discoverable** under [LLM Instructions](admin-settings/llm-instructions.md) makes every endpoint on this page return `404`, including `llms.txt` itself.
-- **Served artifact types.** A deployment that doesn't serve a given artifact type returns `404` for that type's catalog, Markdown, and specification endpoints. See [Artifact types](setting-up/artifact-types.md).
+For details on how visibility is controlled, see [Make an API AI-Ready](../../develop-api-proxy/make-api-ai-ready.md).
 
 ## Related
 
-- [LLM Instructions](admin-settings/llm-instructions.md): set the portal name and description at the top of `llms.txt`, and toggle AI discoverability
-- [Managing API Workflows](admin-settings/manage-api-workflows.md): publish workflows that guide agents through common multi-step use cases
-- [API Workflows](api-workflows.md): how agents discover and follow published workflows
-- [Make an API AI-Ready](../../cloud/develop-api-proxy/make-api-ai-ready.md): publisher guidance on descriptions, specifications, and visibility settings
-- [MCP Servers](mcp-servers/overview.md): how MCP servers are published, discovered, and connected to
-- [MCP Registry API](mcp-registry.md): discover the same servers in the Model Context Protocol registry format
+- [LLM Instructions](../admin-settings/llm-instructions.md) — configure the portal-level context that appears at the top of `llms.txt`
+- [Managing API Workflows](../admin-settings/managing-api-workflows.md) — publish workflows that guide agents through common multi-step use cases
+- [Consuming API Workflows](../api-workflows/consuming-api-workflows.md) — how agents discover and follow published workflows
+- [Make an API AI-Ready](../../develop-api-proxy/make-api-ai-ready.md) — publisher guidance on descriptions, specifications, and visibility settings
+- [MCP Servers](../../mcp-servers/get-started-with-mcp.md) — expose APIs as agent-native MCP tools
```

</details>
