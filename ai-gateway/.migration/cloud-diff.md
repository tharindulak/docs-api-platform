# AI Gateway: Cloud pages against the main line

The main line is seeded from the newest Self-hosted line; pages found only in the Cloud sub-section are added and marked Cloud only (Platform-by-platform walkthrough, rule 4). A Cloud page with the same name as a main-line page is **not** added: the main line keeps its own text, and the Cloud page's legacy URL maps to it. This report lists those pairs so the team can decide each one by PR. Converted from `wso2/docs-api-platform@e9987cde09f3f6859357429a051aa04ee461c13b`.

- Pairs: 7 (0 identical, **7 differ**)
- Cloud-only pages added: 26
- Cloud-only pages whose file name several pages share (possible counterparts, not paired): 2

| Cloud page (legacy) | Main-line page | Paired by | Word F1 | Lines +/− | |
|---|---|---|---|---|---|
| [cloud/ai-gateway/analytics/analytics-header-filter.md](https://wso2.com/api-platform/docs/cloud/ai-gateway/analytics/analytics-header-filter/) | `docs/guides/analytics/analytics-header-filter.mdx` (from ai-gateway/next/analytics/analytics-header-filter.md) | same path | 0.965 | +3 / −5 | **differs** |
| [cloud/ai-gateway/analytics/index.md](https://wso2.com/api-platform/docs/cloud/ai-gateway/analytics/) | `docs/guides/analytics/index.mdx` (from ai-gateway/next/analytics/index.md) | same path | 0.284 | +4 / −13 | **differs** |
| [cloud/ai-gateway/analytics/moesif-analytics.md](https://wso2.com/api-platform/docs/cloud/ai-gateway/analytics/moesif-analytics/) | `docs/guides/analytics/moesif-analytics.mdx` (from ai-gateway/next/analytics/moesif-analytics.md) | same path | 0.721 | +44 / −81 | **differs** |
| [cloud/ai-gateway/overview.md](https://wso2.com/api-platform/docs/cloud/ai-gateway/overview/) | `docs/index.mdx` (from ai-gateway/next/overview.md) | same path | 0.441 | +96 / −17 | **differs** |
| [cloud/ai-gateway/llm/llm-templates.md](https://wso2.com/api-platform/docs/cloud/ai-gateway/llm/llm-templates/) | `docs/reference/llm-templates.mdx` (from ai-gateway/next/reference/llm-templates.md) | same file name | 0.817 | +48 / −114 | **differs** |
| [cloud/ai-gateway/llm/semantic-caching.md](https://wso2.com/api-platform/docs/cloud/ai-gateway/llm/semantic-caching/) | `docs/guides/semantic-caching.mdx` (from ai-gateway/next/semantic-caching.md) | same file name | 0.188 | +282 / −16 | **differs** |
| [cloud/ai-gateway/observability/tracing.md](https://wso2.com/api-platform/docs/cloud/ai-gateway/observability/tracing/) | `docs/guides/logging-and-tracing/tracing.mdx` (from ai-gateway/next/logging-and-tracing/tracing.md) | same file name | 0.999 | +4 / −3 | **differs** |

## Possible counterparts (not paired)

- `cloud/ai-gateway/llm/quick-start-guide.md` (added as Cloud only); same file name as `ai-gateway/next/agent-governance/quick-start-guide.md`, `ai-gateway/next/quick-start-guide.md`
- `cloud/ai-gateway/mcp/quick-start-guide.md` (added as Cloud only); same file name as `ai-gateway/next/agent-governance/quick-start-guide.md`, `ai-gateway/next/quick-start-guide.md`

## Differences

Each diff reads from the main-line text (`-`) to the Cloud text (`+`), front matter left out.

### cloud/ai-gateway/analytics/analytics-header-filter.md

Main-line page `docs/guides/analytics/analytics-header-filter.mdx`; word F1 0.965.

<details><summary>Diff</summary>

```diff
--- main line: ai-gateway/next/analytics/analytics-header-filter.md
+++ Cloud: cloud/ai-gateway/analytics/analytics-header-filter.md
@@ -46,10 +46,8 @@ Each filter parameter (`requestHeadersToFilter` and `responseHeadersToFilter`) i
 ## System Requirements
 
-* Analytics must be enabled globally via `config.toml` (`analytics.enabled = true`)
+* Analytics must be enabled globally via `config.yaml` (`analytics.enabled: true`)
 * The policy must be explicitly applied to the API policy chain
 * If analytics is disabled at the system level, this policy has no effect
 
-For the full set of analytics system parameters, including the publishers to enable and whether payloads are collected, see the [Analytics Header Filter policy](https://wso2.com/api-platform/policy-hub/policies/analytics-header-filter) in Policy Hub.
-
 
 ## API Definition Example
@@ -62,5 +60,5 @@ curl -X POST http://localhost:9090/llm-providers \
   -H "Authorization: Basic <base64-credentials>" \
   --data-binary @- <<'EOF'
-apiVersion: gateway.api-platform.wso2.com/v1
+apiVersion: gateway.api-platform.wso2.com/v1alpha1
 kind: LlmProvider
 metadata:
@@ -83,5 +81,5 @@ spec:
         policies:
           - name: analytics-header-filter
-            version: v0.1.0
+            version: v1
             params:
               requestHeadersToFilter:
```

</details>

### cloud/ai-gateway/analytics/index.md

Main-line page `docs/guides/analytics/index.mdx`; word F1 0.284.

<details><summary>Diff</summary>

```diff
--- main line: ai-gateway/next/analytics/index.md
+++ Cloud: cloud/ai-gateway/analytics/index.md
@@ -1,17 +1,8 @@
 # Analytics
 
-Analytics tells you how your APIs are used over time. Logging and tracing tell you what the gateway did with a single request; analytics aggregates traffic so you can see usage, cost, and trends across many of them. For the other two, see [Gateway logs](../logging-and-tracing/gateway-logs.md) and [Gateway tracing](../logging-and-tracing/tracing.md).
+The AI Gateway analytics docs explain how to publish request and response metadata to external analytics systems.
 
-The gateway publishes request and response data to an external analytics backend. You choose the backend, and you control which headers travel with the data.
+## In This Section
 
-## In this section
-
-This section contains the following pages:
-
-| Page | What it covers |
-|------|----------------|
-| [Moesif analytics](moesif-analytics.md) | Configure Moesif in API Platform AI Gateway to capture and publish API request and response data. |
-| [OpenTelemetry analytics](opentelemetry-analytics.md) | Export analytics events as OpenTelemetry Protocol (OTLP) log records to an OpenTelemetry Collector or any OTLP-compatible backend. |
-| [Analytics header filter](analytics-header-filter.md) | Control which request and response headers are sent to analytics backends using allow or deny mode in API Platform AI Gateway. |
-
-Moesif analytics and the analytics header filter configure a policy from the [Policy Hub](https://wso2.com/api-platform/policy-hub), the versioned reference for every API Platform policy. For policy categories and how policies chain, see the [Policy Hub overview](../../../policy-hub/overview.md).
+- [Moesif Analytics](moesif-analytics.md) for platform-level analytics collection and publishing
+- [Analytics Header Filter](analytics-header-filter.md) for filtering analytics data before export
```

</details>

### cloud/ai-gateway/analytics/moesif-analytics.md

Main-line page `docs/guides/analytics/moesif-analytics.mdx`; word F1 0.721.

<details><summary>Diff</summary>

```diff
--- main line: ai-gateway/next/analytics/moesif-analytics.md
+++ Cloud: cloud/ai-gateway/analytics/moesif-analytics.md
@@ -5,5 +5,5 @@
 The Analytics feature enables the API Platform to capture, process, and publish API request and response data for observability and business insights. Analytics data is collected asynchronously from the gateway without impacting request latency and is published to an external analytics platform for further analysis and visualization.
 
-This capability allows platform administrators and business stakeholders to gain visibility into LLM Proxy and MCP Proxy usage patterns, traffic behavior, latency characteristics, and consumer activity across the platform.
+This capability allows platform administrators and business stakeholders to gain visibility into API usage patterns, traffic behavior, latency characteristics, and consumer activity across the platform.
 
 
@@ -20,12 +20,11 @@ This capability allows platform administrators and business stakeholders to gain
 ## Prerequisites
 
-- Active Moesif Account and an Application ID.
-    For obtaining the Application ID, follow these steps:
-    - Step 1: Sign up in [Moesif](https://www.moesif.com/)
-    - Sept 2: Follow the onboarding wizard.
-    - Sept 3: During the sign up process, you will receive a Collector Application ID for your configured application. Copy this value and keep it saved.
+ - Active Moesif Account and an Application ID
+> **Note:** For obtaining the Application ID:
+> - Step 1: Sign up in [Moesif](https://www.moesif.com/)
+> - Sept 2: Follow the onboarding wizard.
+> - Sept 3: During the sign up process, you will receive a Collector Application ID for your configured application. Copy this value and keep it saved.
 
-!!! note
-    For more detailed instructions and advanced configuration options, refer to the [official Moesif Documentation](https://www.moesif.com/docs).
+> For more detailed instructions and advanced configuration options, refer to the [official Moesif Documentation](https://www.moesif.com/docs).
 
 
@@ -34,11 +33,4 @@ This capability allows platform administrators and business stakeholders to gain
 Analytics is configured entirely through the gateway `config.toml` file and is enabled at a system level.
 
-!!! note
-    Analytics is a **consumer** of a shared data-capture pipeline called the **collector**. The
-    collector has no `enabled` flag of its own — it activates automatically whenever `analytics.enabled`
-    (or `traffic_logging.enabled`) is `true`. See [Log requests and responses](../logging-and-tracing/log-requests-and-responses.md)
-    for the other consumer of this same pipeline, which writes a stdout JSON line per request instead
-    of publishing to an external SaaS.
-
 ### System Parameters (`config.toml`)
 
@@ -47,55 +39,25 @@ Analytics is configured entirely through the gateway `config.toml` file and is e
 | Parameter | Type    | Required | Default | Description                            |
 | --------- | ------- | -------- |-------- | -------------------------------------- |
-| `enabled` | boolean | Yes      | false   | Enables or disables analytics globally, and activates the collector. |
-| `enabled_publishers` | array of strings | No | `["moesif"]` | Publisher names to activate. Currently only `moesif` is supported. |
+| `enabled` | boolean | Yes      | false   | Enables or disables analytics globally |
 
 #### Publishers
 
-Each entry in `enabled_publishers` must have a matching configuration table under
-`[analytics.publishers.<name>]`.
-
-##### Moesif (`[analytics.publishers.moesif]`)
-
 | Parameter              | Type    | Required | Description                               |
 | ---------------------- | ------- | -------- | ----------------------------------------- |
-| `application_id`       | string  | Yes      | Moesif application identifier |
-| `moesif_base_url`      | string  | No       | Moesif ingestion endpoint (default `https://api.moesif.net`) |
-| `publish_interval`     | int     | Yes       | Interval (seconds) between publish cycles |
-| `event_queue_size`     | int     | Yes       | Maximum events held in memory             |
-| `batch_size`           | int     | Yes       | Maximum events per batch                  |
-| `timer_wakeup_seconds` | int     | Yes       | Publisher timer resolution                |
+| `type`                 | string  | Yes      | Analytics publisher type (Currently limited only to ```moesif``` )                  |
+| `enabled`              | boolean | Yes      | Enables the publisher                     |
+| `settings`             | object | Yes       | Map of Publisher specific attributes required for configuring the publisher client                     |
 
-#### Data capture (`[collector]`)
+#### gRPC Event Server
 
-Analytics captures request/response headers and bodies through the shared `[collector]` section (also
-used by Traffic Logging). Capture is off by default — enable only what Moesif needs:
-
-| Parameter | Type | Default | Description |
-|---|---|---|---|
-| `request_body` | boolean | `false` | Capture the full request body and attach it to published events. |
-| `response_body` | boolean | `false` | Capture the full response body and attach it to published events. |
-| `request_headers` | boolean | `false` | Capture all request headers and attach them to published events. |
-| `response_headers` | boolean | `false` | Capture all response headers and attach them to published events. |
-| `ignore_path_prefixes` | array of strings | `[]` | Path prefixes (e.g. `/health`, `/metrics`) for which no analytics event is produced at all. |
-
-!!! note
-    Masking/redaction is a per-consumer, presentation-time concern, not a collector guarantee — the
-    collector hands every enabled consumer the same raw captured data. Moesif always receives unmasked
-    headers, regardless of any `masked_headers` configuration used by Traffic Logging.
-
-#### ALS transport (`[collector.server]`)
-
-This section configures both the Envoy access log streaming settings and the ALS (Access Log Service)
-server that receives those logs. It is shared with Traffic Logging — the controller reads it to
-configure Envoy's gRPC access-log sink, and the policy-engine reads it to configure the receiving ALS
-server.
+This section configures both the Envoy access log streaming settings and the ALS (Access Log Service) server that receives those logs. The ALS server runs within the policy-engine component.
 
 | Parameter               | Type     | Required | Default | Description                      |
 | ----------------------- | -------- | -------- |---- | -------------------------------- |
-| `mode`                  | string   | No       | `"uds"` | Transport mode: `"uds"` (Unix domain socket) or `"tcp"`. |
 | `buffer_flush_interval` | duration | No       | `1000000000`| Maximum time Envoy waits(in nanoseconds) before flushing buffered access log entries.|
 | `buffer_size_bytes`     | int      | No       | `16384` | Maximum size of the in-memory buffer used to batch access log entries before sending them to ALS server.                  |
 | `grpc_request_timeout`  | duration | No       | `20000000000` | Timeout duration Envoy waits(in nanoseconds) for a response from the ALS server before considering the log delivery attempt failed.            |
-| `shutdown_timeout`      | duration | No       | `"600s"` | Maximum time allowed for the ALS server to gracefully shut down while completing in-flight log processing. |
+| `server_port`           | int     | Yes      | - | gRPC port on which the ALS server listens for incoming access log streams from Envoy.      |
+| `shutdown_timeout`      | int     | No       | `600` | Maximum time allowed for the ALS server to gracefully shut down while completing in-flight log processing(in seconds). |
 | `als_plain_text`        | boolean | No       | `true` | Use plaintext gRPC        |
 | `public_key_path`       | string | No       | - | Path to the public key used for securing ALS communication when transport-level encryption or authentication is enabled.        |
@@ -104,22 +66,5 @@ server.
 | `max_header_limit`      | int     | No       | `8192` | Maximum allowed size of request or response headers processed by the ALS server      |
 
-!!! note
-    The ALS gRPC port is fixed at `18090` and is not configurable — this guarantees the controller and
-    policy-engine sides can never disagree on it. The hostname for the ALS connection is automatically
-    derived from the policy-engine configuration. The internal log name identifier is set to
-    `"envoy_access_log"` and is not configurable.
-
-#### Deprecated keys
-
-The following `[analytics]` keys still work, but are deprecated in favor of the shared `[collector]` /
-`[collector.server]` sections above. They are migrated automatically at load time with a warning, so
-existing configs keep working unchanged:
-
-| Deprecated key | Migrated onto | Notes |
-|---|---|---|
-| `analytics.allow_payloads` | `collector.request_body` + `collector.response_body` | Directional flags (below) win over `allow_payloads`. |
-| `analytics.send_request_body` / `send_response_body` | `collector.request_body` / `response_body` | — |
-| `analytics.grpc_event_server.*` | `collector.server.*` | Whole-section migration, applied only while `[collector.server]` is unset and `analytics.enabled = true`. |
-| `analytics.access_logs_service.*` | `collector.server.*` | Same migration as above; `server_port` is dropped since the ALS port is now a fixed constant. |
+**Note:** The hostname for the ALS connection is automatically derived from the policy-engine configuration. The internal log name identifier is set to `"envoy_access_log"` and is not configurable.
 
 
@@ -128,23 +73,39 @@ existing configs keep working unchanged:
 #### Integrate Moesif Publisher
 
-```toml
-[collector]
-request_headers = true
-response_headers = true
+For Moesif analytics integration, the following publisher-specific attributes must be configured under the `settings` section. These parameters control authentication, batching behavior, and publish intervals for efficient analytics delivery. The required attributes are as follows.
+
+| Parameter              | Type    | Required | Description                               |
+| ---------------------- | ------- | -------- | ----------------------------------------- |
+| `application_id`       | string  | Yes      | Analytics platform application identifier |
+| `publish_interval`     | int     | Yes       | Interval (seconds) between publish cycles |
+| `event_queue_size`     | int     | Yes       | Maximum events held in memory             |
+| `batch_size`           | int     | Yes       | Maximum events per batch                  |
+| `timer_wakeup_seconds` | int     | Yes       | Publisher timer resolution                |
 
-[collector.server]
-mode = "uds"
 
+```toml
 [analytics]
 enabled = true
-enabled_publishers = ["moesif"]
 
-[analytics.publishers.moesif]
+[[analytics.publishers]]
+type = "moesif"
+enabled = true
+
+[analytics.publishers.settings]
 application_id = "<MOESIF_APPLICATION_ID>"
-moesif_base_url = "https://api.moesif.net"
 publish_interval = 5
 event_queue_size = 10000
 batch_size = 50
 timer_wakeup_seconds = 3
+
+[analytics.grpc_event_server]
+buffer_flush_interval = 1000000000
+buffer_size_bytes = 16384
+grpc_request_timeout = 20000000000
+server_port = 18090
+shutdown_timeout = 600
+als_plain_text = true
+max_message_size = 1000000000
+max_header_limit = 8192
 ```
 
@@ -152,6 +113,8 @@ timer_wakeup_seconds = 3
 ## Use Cases
 
-* **API Usage Visibility** – Understand how LLM Proxies and MCP Proxies are consumed across tenants and applications.
+* **API Usage Visibility** – Understand how APIs are consumed across tenants and applications.
 * **Operational Insights** – Observe traffic volume, response behavior, and latency trends.
 * **Business Intelligence** – Support product and business decisions using API analytics data.
 * **Platform Monitoring** – Gain observability into API behavior without impacting performance.
+
+
```

</details>

### cloud/ai-gateway/overview.md

Main-line page `docs/index.mdx`; word F1 0.441.

<details><summary>Diff</summary>

```diff
--- main line: ai-gateway/next/overview.md
+++ Cloud: cloud/ai-gateway/overview.md
@@ -1,25 +1,104 @@
-# API Platform AI Gateway
+# AI Gateway Overview
 
-A gateway for managing and securing AI traffic, including Large Language Model (LLM) APIs, Model Context Protocol (MCP) servers, and Agent2Agent (A2A) agents.
+The AI Gateway is the standalone runtime plane for routing, securing, and observing AI traffic. It handles Large Language Model (LLM) APIs and Model Context Protocol (MCP) servers, and can run independently or connect to the AI Workspace control plane for centralized management.
 
-## Why use the AI Gateway
+## Quick Start
 
-Run the AI Gateway when AI traffic needs the controls you already apply to your APIs. With it, you can:
+- [LLM Quick Start Guide](llm/quick-start-guide.md) - Set up the gateway, verify the controller admin health endpoint, and route traffic to LLM providers like OpenAI
+- [MCP Quick Start Guide](mcp/quick-start-guide.md) - Set up the gateway, verify the controller admin health endpoint, and route traffic to MCP servers
 
-- Apply guardrails that validate, filter, or transform content before it reaches a model or a client. See [Guardrails](guardrails/index.md).
-- Serve one OpenAI-compatible endpoint that routes requests to multiple LLM providers. See [Multi-provider routing](routing/multi-provider-routing.md).
-- Expose MCP servers through a central gateway, and apply authentication and access control to MCP traffic. See [MCP proxy](gateway-artifacts/mcp-proxy.md).
-- Give an A2A agent one governed address, serve its Agent Card from the gateway, and apply policies to individual A2A operations. See [Agent governance](agent-governance/index.md).
-- Collect logs, traces, and analytics for the traffic the gateway handles. See [Gateway logs](logging-and-tracing/gateway-logs.md).
-- Run the gateway on its own, or register it with AI Workspace to govern the gateways across your organization. See [Connect to AI Workspace](setup-and-deployment/production-deployment/control-plane-connection.md).
+## Key Concepts
 
-## Who it is for
+### LLM Provider Template
 
-Two roles share the gateway. A platform administrator configures LLM providers, the credentials they use, and the policies that apply organization-wide. An AI developer creates LLM proxies on top of those providers, and adds the policies a single application needs.
+An LLM Provider Template defines the characteristics and behaviors specific to an AI service provider, such as OpenAI, Azure OpenAI, or other LLM platforms. It describes how the gateway should interpret and extract usage and operational metadata, including prompt, completion, total, and remaining token information, as well as request and response model metadata.
 
-## Where to go next
+Following templates are shipped out-of-the-box
 
-- To install the gateway and route a first request through it, see [Quick Start Guide](quick-start-guide.md).
-- To learn which artifacts a request passes through, see [How it works](how-it-works.md).
-- To expose an MCP server through the gateway, see [MCP proxy](gateway-artifacts/mcp-proxy.md).
-- To put an A2A agent behind the gateway, see [Agent governance](agent-governance/index.md).
+- OpenAI
+- Azure OpenAI
+- Anthropic
+- AWS Bedrock
+- Azure AI Foundry
+- Gemini
+
+### LLM Provider
+
+An LLM Provider represents a connection from the gateway runtime to an AI backend service such as OpenAI, Azure OpenAI, or other LLM APIs. Administrators configure LLM Providers to define:
+
+- The LLM Provider Template
+- The upstream LLM service URL
+- Authentication credentials (API keys, tokens)
+- Access control rules for which endpoints are exposed
+- Budget control policies, such as token-based rate limiting
+- Organization-wide policies such as guardrails
+
+Once configured, the LLM Provider allows traffic to flow through the gateway to the AI backend.
+
+### LLM Proxy
+
+An LLM Proxy allows developers to create custom API endpoints that consume an LLM Provider, while inheriting administrator-enforced access control, budgeting and organization-wide policies defined at the provider level. Each proxy gets its own URL context (e.g., `/assistant`) and can have its own policies applied. This enables:
+
+- Multiple AI applications to share a single LLM Provider
+- Per-application policies such as prompt management and guardrails
+- Separation between platform administration and application development
+
+### MCP Proxy
+
+An MCP Proxy routes Model Context Protocol traffic to MCP servers. MCP is a protocol that enables AI assistants to interact with external tools and data sources. With MCP Proxies, you can:
+
+- Expose MCP servers through a centralized gateway
+- Apply authentication and access control to MCP traffic
+- Manage multiple MCP servers from a single control plane
+
+## Control Plane Integration
+
+The AI Gateway can be managed in two ways:
+
+- Directly through the Gateway-Controller API for standalone deployments
+- Through the [AI Workspace](../ai-workspace/overview.md), which acts as the control plane for connected gateway runtimes
+
+Use AI Workspace when you want a UI-driven control plane for gateway registration, provider and proxy management, policy configuration, and deployment workflows.
+
+## Default Ports
+
+| Port | Service | Description |
+|------|---------|-------------|
+| 8080 | Router | HTTP traffic |
+| 8443 | Router | HTTPS traffic |
+| 9090 | Gateway-Controller | REST API |
+| 9094 | Gateway-Controller Admin | Health and admin endpoints |
+
+## Architecture
+
+```
+                           ┌─────────────────┐
+                           │ LLM Providers   │
+                           │ (OpenAI, etc.)  │
+                           └────────▲────────┘
+                                    │
+┌──────────┐    ┌──────────────┐    │
+│ AI Apps  │───▶│  AI Gateway  │────┤
+└──────────┘    └──────────────┘    │
+                                    │
+                           ┌────────▼────────┐
+                           │  MCP Servers    │
+                           └─────────────────┘
+```
+
+**How it works:**
+
+1. Administrators verify the Gateway-Controller admin health endpoint and configure the gateway either through the Gateway-Controller API or through AI Workspace
+2. Developers create LLM Proxies to build AI applications on top of available providers
+3. The gateway routes traffic, applies policies, and manages authentication
+
+## Documentation
+
+| Section | Description |
+|---------|-------------|
+| [llm/](llm/index.md) | LLM provider configuration, guardrails, prompt management, and semantic caching |
+| [mcp/](mcp/index.md) | MCP proxy setup and policies |
+| [observability/](observability/index.md) | Logging and tracing configuration |
+| [analytics/](analytics/index.md) | Analytics integrations (Moesif) |
+| [Gateway-Controller API](gateway-controller-api.md) | Standalone gateway REST API usage for providers and proxies |
+| [AI Workspace](../ai-workspace/overview.md) | Control plane for managing connected AI Gateway runtimes |
```

</details>

### cloud/ai-gateway/llm/llm-templates.md

Main-line page `docs/reference/llm-templates.mdx`; word F1 0.817.

<details><summary>Diff</summary>

```diff
--- main line: ai-gateway/next/reference/llm-templates.md
+++ Cloud: cloud/ai-gateway/llm/llm-templates.md
@@ -9,6 +9,4 @@ LLM Provider Templates define the characteristics and behaviors specific to an A
 - **Rate Limiting Data**: Remaining token allowances from response
 
-This page is the reference for that extraction mechanism: which templates ship, what each one reads out of a provider response, and how to define a template of your own. It does not carry the settings that connect the gateway to a provider. Every template below has a page under Supported Providers that covers the upstream URL, the authentication, and a provider definition you can deploy. Each template's section links its own.
-
 ## Out-of-the-Box Supported Templates
 
@@ -22,5 +20,5 @@ The API Platform Gateway ships with the following pre-configured LLM provider te
 | `gemini` | Gemini | Google Gemini Provider |
 | `mistralai` | MistralAI | Mistral AI Provider |
-| `awsbedrock` | AWS Bedrock | AWS Bedrock Provider |
+| `awsbedrock` | AWS Bedrock | Amazon Bedrock Provider |
 | `azureai-foundry` | Azure AI Foundry | Microsoft Azure AI Foundry Provider |
 
@@ -32,5 +30,5 @@ Each LLM provider template follows a standard YAML structure:
 
 ```yaml
-apiVersion: gateway.api-platform.wso2.com/v1
+apiVersion: gateway.api-platform.wso2.com/v1alpha1
 kind: LlmProviderTemplate
 metadata:
@@ -38,25 +36,22 @@ metadata:
 spec:
   displayName: <Display Name>
-  groupId: <template-family-id>
-  managedBy: <template-owner>
-  version: <template-version>
   # Provider characteristics
   promptTokens:
-    location: <payload|header|queryParam|pathParam>
+    location: <payload|header|pathParam>
     identifier: <extraction-pattern>
   completionTokens:
-    location: <payload|header|queryParam|pathParam>
+    location: <payload|header|pathParam>
     identifier: <extraction-pattern>
   totalTokens:
-    location: <payload|header|queryParam|pathParam>
+    location: <payload|header|pathParam>
     identifier: <extraction-pattern>
   remainingTokens:
-    location: <payload|header|queryParam|pathParam>
+    location: <payload|header|pathParam>
     identifier: <extraction-pattern>
   requestModel:
-    location: <payload|header|queryParam|pathParam>
+    location: <payload|header|pathParam>
     identifier: <extraction-pattern>
   responseModel:
-    location: <payload|header|queryParam|pathParam>
+    location: <payload|header|pathParam>
     identifier: <extraction-pattern>
 ```
@@ -64,9 +59,8 @@ spec:
 ### Metadata Extraction Patterns
 
-Templates support four types of extraction locations:
+Templates support three types of extraction locations:
 
 - **`payload`**: Extract from JSON response body using JSONPath expressions (e.g., `$.usage.prompt_tokens`)
 - **`header`**: Extract from HTTP response headers using header name (e.g., `x-ratelimit-remaining-tokens`)
-- **`queryParam`**: Extract from a URL query parameter
 - **`pathParam`**: Extract from URL path using regular expressions (e.g., `(?<=models/)[a-zA-Z0-9.\-]+`)
 
@@ -75,8 +69,8 @@ Templates support four types of extraction locations:
 ### OpenAI
 
-The OpenAI template extracts metadata from OpenAI API responses. To connect the gateway to OpenAI, see [OpenAI](../gateway-artifacts/llm-provider/supported-providers/openai.md).
+The OpenAI template extracts metadata from OpenAI API responses.
 
 ```yaml
-apiVersion: gateway.api-platform.wso2.com/v1
+apiVersion: gateway.api-platform.wso2.com/v1alpha1
 kind: LlmProviderTemplate
 metadata:
@@ -84,7 +78,4 @@ metadata:
 spec:
   displayName: OpenAI
-  groupId: wso2-openai
-  managedBy: wso2
-  version: v1.0
   promptTokens:
     location: payload
@@ -105,21 +96,12 @@ spec:
     location: payload
     identifier: $.model
-  resourceMappings:
-    resources:
-      - resource: /responses
-        promptTokens:
-          location: payload
-          identifier: $.usage.input_tokens
-        completionTokens:
-          location: payload
-          identifier: $.usage.output_tokens
 ```
 
 ### Azure OpenAI
 
-The Azure OpenAI template is compatible with Microsoft's Azure OpenAI Service API. To connect the gateway to Azure OpenAI, see [Azure OpenAI](../gateway-artifacts/llm-provider/supported-providers/azure-openai.md).
+The Azure OpenAI template is compatible with Microsoft's Azure OpenAI Service API.
 
 ```yaml
-apiVersion: gateway.api-platform.wso2.com/v1
+apiVersion: gateway.api-platform.wso2.com/v1alpha1
 kind: LlmProviderTemplate
 metadata:
@@ -127,13 +109,10 @@ metadata:
 spec:
   displayName: Azure OpenAI
-  groupId: wso2-azure-openai
-  managedBy: wso2
-  version: v1.0
   promptTokens:
     location: payload
-    identifier: $.usage.prompt_tokens
+    identifier: $.usage.input_tokens
   completionTokens:
     location: payload
-    identifier: $.usage.completion_tokens
+    identifier: $.usage.output_tokens
   totalTokens:
     location: payload
@@ -148,21 +127,12 @@ spec:
     location: payload
     identifier: $.model
-  resourceMappings:
-    resources:
-      - resource: /responses
-        promptTokens:
-          location: payload
-          identifier: $.usage.input_tokens
-        completionTokens:
-          location: payload
-          identifier: $.usage.output_tokens
 ```
 
 ### Anthropic
 
-The Anthropic template extracts metadata from Anthropic Claude API responses. To connect the gateway to Anthropic, see [Anthropic](../gateway-artifacts/llm-provider/supported-providers/anthropic.md).
+The Anthropic template extracts metadata from Anthropic Claude API responses.
 
 ```yaml
-apiVersion: gateway.api-platform.wso2.com/v1
+apiVersion: gateway.api-platform.wso2.com/v1alpha1
 kind: LlmProviderTemplate
 metadata:
@@ -170,7 +140,4 @@ metadata:
 spec:
   displayName: Anthropic
-  groupId: wso2-anthropic
-  managedBy: wso2
-  version: v1.0
   promptTokens:
     location: payload
@@ -192,8 +159,8 @@ spec:
 ### Gemini
 
-The Gemini template is designed for Google's Gemini API. To connect the gateway to Gemini, see [Gemini](../gateway-artifacts/llm-provider/supported-providers/gemini.md).
+The Gemini template is designed for Google's Gemini API.
 
 ```yaml
-apiVersion: gateway.api-platform.wso2.com/v1
+apiVersion: gateway.api-platform.wso2.com/v1alpha1
 kind: LlmProviderTemplate
 metadata:
@@ -201,7 +168,4 @@ metadata:
 spec:
   displayName: Gemini
-  groupId: wso2-gemini
-  managedBy: wso2
-  version: v1.0
   promptTokens:
     location: payload
@@ -226,8 +190,8 @@ spec:
 ### MistralAI
 
-The MistralAI template supports Mistral AI's API. To connect the gateway to Mistral AI, see [MistralAI](../gateway-artifacts/llm-provider/supported-providers/mistralai.md).
+The MistralAI template supports Mistral AI's API.
 
 ```yaml
-apiVersion: gateway.api-platform.wso2.com/v1
+apiVersion: gateway.api-platform.wso2.com/v1alpha1
 kind: LlmProviderTemplate
 metadata:
@@ -235,7 +199,4 @@ metadata:
 spec:
   displayName: MistralAI
-  groupId: wso2-mistralai
-  managedBy: wso2
-  version: v1.0
   promptTokens:
     location: payload
@@ -260,8 +221,8 @@ spec:
 ### AWS Bedrock
 
-The AWS Bedrock template is designed for the AWS Bedrock unified API. To connect the gateway to Bedrock with either bearer or AWS Signature Version 4 (SigV4) authentication, see [AWS Bedrock](../gateway-artifacts/llm-provider/supported-providers/aws-bedrock.md).
+The AWS Bedrock template is designed for Amazon Bedrock's unified API.
 
 ```yaml
-apiVersion: gateway.api-platform.wso2.com/v1
+apiVersion: gateway.api-platform.wso2.com/v1alpha1
 kind: LlmProviderTemplate
 metadata:
@@ -269,7 +230,4 @@ metadata:
 spec:
   displayName: AWS Bedrock
-  groupId: wso2-awsbedrock
-  managedBy: wso2
-  version: v1.0
   promptTokens:
     location: payload
@@ -283,16 +241,16 @@ spec:
   requestModel:
     location: pathParam
-    identifier: model/(.+)$
+    identifier: (?<=model/)[a-zA-Z0-9.:-]+(?=/)
   responseModel:
     location: pathParam
-    identifier: model/(.+)$
+    identifier: (?<=model/)[a-zA-Z0-9.:-]+(?=/)
 ```
 
 ### Azure AI Foundry
 
-The Azure AI Foundry template supports Microsoft's Azure AI Foundry platform. To connect the gateway to Azure AI Foundry, see [Azure AI Foundry](../gateway-artifacts/llm-provider/supported-providers/azure-ai-foundry.md).
+The Azure AI Foundry template supports Microsoft's Azure AI Foundry platform.
 
 ```yaml
-apiVersion: gateway.api-platform.wso2.com/v1
+apiVersion: gateway.api-platform.wso2.com/v1alpha1
 kind: LlmProviderTemplate
 metadata:
@@ -300,7 +258,4 @@ metadata:
 spec:
   displayName: Azure AI Foundry
-  groupId: wso2-azureai-foundry
-  managedBy: wso2
-  version: v1.0
   promptTokens:
     location: payload
@@ -321,13 +276,4 @@ spec:
     location: payload
     identifier: $.model
-  resourceMappings:
-    resources:
-      - resource: /responses
-        promptTokens:
-          location: payload
-          identifier: $.usage.input_tokens
-        completionTokens:
-          location: payload
-          identifier: $.usage.output_tokens
 ```
 
@@ -336,10 +282,12 @@ spec:
 To create an LLM provider using any of the out-of-the-box templates:
 
+For local or development environments only, the default credentials may be `admin:admin` encoded as `YWRtaW46YWRtaW4=`.
+
 ```bash
-curl -X POST http://localhost:9090/api/management/v1/llm-providers \
+curl -X POST http://localhost:9090/llm-providers \
   -H "Content-Type: application/yaml" \
-  -u "$ADMIN_USERNAME:$ADMIN_PASSWORD" \
+  -H "Authorization: Basic <BASE64_CREDENTIAL>" \
   --data-binary @- <<'EOF'
-apiVersion: gateway.api-platform.wso2.com/v1
+apiVersion: gateway.api-platform.wso2.com/v1alpha1
 kind: LlmProvider
 metadata:
@@ -349,5 +297,4 @@ spec:
   version: v1.0
   template: <template-id>
-  context: /<provider-context>
   upstream:
     url: https://api.openai.com/v1
@@ -372,5 +319,4 @@ Replace the placeholders:
 - `<display-name>`: Human-readable name (e.g., `My OpenAI Provider`)
 - `<template-id>`: One of the supported template IDs (`openai`, `azure-openai`, `anthropic`, `gemini`, `mistralai`, `awsbedrock`, `azureai-foundry`)
-- `<provider-context>`: Base path for the provider routes (e.g., `openai/latest`)
 - `<auth-header>`: Authentication header name (e.g., `Authorization` for most providers)
 - `<key>`: Your API key with appropriate prefix (e.g., `Bearer sk-...` for OpenAI)
@@ -389,6 +335,6 @@ To list all available LLM provider templates:
 
 ```bash
-curl -X GET http://localhost:9090/api/management/v1/llm-provider-templates \
-  -u "$ADMIN_USERNAME:$ADMIN_PASSWORD"
+curl -X GET http://localhost:9090/llm-provider-templates \
+  -H "Authorization: Basic <BASE64_CREDENTIAL>"
 ```
 
@@ -398,18 +344,18 @@ To retrieve details of a specific template:
 
 ```bash
-curl -X GET http://localhost:9090/api/management/v1/llm-provider-templates/openai \
-  -u "$ADMIN_USERNAME:$ADMIN_PASSWORD"
+curl -X GET http://localhost:9090/llm-provider-templates/openai \
+  -H "Authorization: Basic <BASE64_CREDENTIAL>"
 ```
 
 ### Creating Custom Templates
 
-Platform administrators can create custom templates for LLM providers not covered by the out-of-the-box templates. For the end-to-end procedure, from defining the template to deploying a provider that uses it, see [Custom provider](../gateway-artifacts/llm-provider/supported-providers/custom-provider.md).
+Platform administrators can create custom templates for LLM providers not covered by the out-of-the-box templates:
 
 ```bash
-curl -X POST http://localhost:9090/api/management/v1/llm-provider-templates \
+curl -X POST http://localhost:9090/llm-provider-templates \
   -H "Content-Type: application/yaml" \
-  -u "$ADMIN_USERNAME:$ADMIN_PASSWORD" \
+  -H "Authorization: Basic <BASE64_CREDENTIAL>" \
   --data-binary @- <<'EOF'
-apiVersion: gateway.api-platform.wso2.com/v1
+apiVersion: gateway.api-platform.wso2.com/v1alpha1
 kind: LlmProviderTemplate
 metadata:
@@ -417,7 +363,4 @@ metadata:
 spec:
   displayName: Custom Provider
-  groupId: custom-provider
-  managedBy: customer
-  version: v1.0
   totalTokens:
     location: payload
@@ -431,9 +374,9 @@ To update an existing custom template:
 
 ```bash
-curl -X PUT http://localhost:9090/api/management/v1/llm-provider-templates/custom-provider \
+curl -X PUT http://localhost:9090/llm-provider-templates/custom-provider \
   -H "Content-Type: application/yaml" \
-  -u "$ADMIN_USERNAME:$ADMIN_PASSWORD" \
+  -H "Authorization: Basic <BASE64_CREDENTIAL>" \
   --data-binary @- <<'EOF'
-apiVersion: gateway.api-platform.wso2.com/v1
+apiVersion: gateway.api-platform.wso2.com/v1alpha1
 kind: LlmProviderTemplate
 metadata:
@@ -441,7 +384,4 @@ metadata:
 spec:
   displayName: Custom Provider Updated
-  groupId: custom-provider
-  managedBy: customer
-  version: v1.0
   promptTokens:
     location: payload
@@ -456,6 +396,6 @@ To delete a custom template:
 
 ```bash
-curl -X DELETE http://localhost:9090/api/management/v1/llm-provider-templates/custom-provider \
-  -u "$ADMIN_USERNAME:$ADMIN_PASSWORD"
+curl -X DELETE http://localhost:9090/llm-provider-templates/custom-provider \
+  -H "Authorization: Basic <BASE64_CREDENTIAL>"
 ```
 
@@ -464,15 +404,10 @@ curl -X DELETE http://localhost:9090/api/management/v1/llm-provider-templates/cu
 ## Template Field Reference
 
-Use this table to configure an `LlmProviderTemplate` resource.
-
 | Field | Type | Required | Description |
 |-------|------|----------|-------------|
-| `apiVersion` | string | Yes | API version, must be `gateway.api-platform.wso2.com/v1` |
+| `apiVersion` | string | Yes | API version, must be `gateway.api-platform.wso2.com/v1alpha1` |
 | `kind` | string | Yes | Resource kind, must be `LlmProviderTemplate` |
 | `metadata.name` | string | Yes | Unique identifier for the template (used as template ID) |
 | `spec.displayName` | string | Yes | Human-readable name for the template |
-| `spec.groupId` | string | No | Stable family identifier shared by versions of the same template; defaults to `metadata.name` |
-| `spec.managedBy` | string | No | Template owner; built-in templates use `wso2`, while custom templates default to `customer` |
-| `spec.version` | string | No | Template content version; defaults to `v1.0` |
 | `spec.promptTokens` | object | No | Configuration for extracting prompt/input token count |
 | `spec.completionTokens` | object | No | Configuration for extracting completion/output token count |
@@ -481,5 +416,4 @@ Use this table to configure an `LlmProviderTemplate` resource.
 | `spec.requestModel` | object | No | Configuration for extracting request model identifier |
 | `spec.responseModel` | object | No | Configuration for extracting response model identifier |
-| `spec.resourceMappings` | object | No | Resource-specific extraction overrides, such as token paths for `/responses` |
 
 ### Extraction Configuration Object
@@ -489,4 +423,4 @@ Each extraction configuration object has the following structure:
 | Field | Type | Values | Description |
 |-------|------|--------|-------------|
-| `location` | string | `payload`, `header`, `queryParam`, `pathParam` | Where to extract the value from |
-| `identifier` | string | - | JSONPath (for payload), header or query parameter name, or regex pattern (for pathParam) |
+| `location` | string | `payload`, `header`, `pathParam` | Where to extract the value from |
+| `identifier` | string | - | JSONPath (for payload), header name (for header), or regex pattern (for pathParam) |
```

</details>

### cloud/ai-gateway/llm/semantic-caching.md

Main-line page `docs/guides/semantic-caching.mdx`; word F1 0.188.

<details><summary>Diff</summary>

```diff
--- main line: ai-gateway/next/semantic-caching.md
+++ Cloud: cloud/ai-gateway/llm/semantic-caching.md
@@ -1,27 +1,293 @@
-# Semantic caching
+# Semantic Caching
 
-People ask the same question in different words. A conventional cache misses every one of those, because it matches on the exact string and the strings differ. A semantic cache compares meaning instead, so a prompt that means what an earlier prompt meant is answered from the cache.
+## Overview
 
-A cache hit skips the upstream call entirely. That removes the latency of the model round trip and the tokens it would have charged for.
+The Semantic Cache policy enables intelligent response caching for LLM (Large Language Model) APIs using vector similarity search. Unlike traditional key-based caching, semantic caching understands the meaning of requests and can serve cached responses for semantically similar queries, even when the exact wording differs. This dramatically improves performance and reduces costs by avoiding redundant API calls to upstream LLM services.
 
-## Where the cache sits in the request path
+The policy uses embedding models to convert request text into high-dimensional vectors, then performs similarity searches in a vector database to find previously cached responses. If a similar request is found within the configured similarity threshold, the cached response is returned immediately without calling the upstream service.
 
-The `Semantic Cache` policy converts the prompt into a vector, searches a vector store for a previously answered prompt above a similarity threshold, and returns that stored response when it finds one. A miss goes upstream as normal, and the response is stored for next time.
+## Features
 
-Attach it on an `LlmProxy` to cache one application's traffic, or on an `LlmProvider` to cache every proxy that consumes it. The policy needs an embedding provider to produce the vectors and a vector store to hold them; the Policy Hub page lists the backends it supports and the threshold and expiry settings that decide how readily it treats two prompts as equivalent.
+- **Vector-based similarity matching**: Uses embeddings to find semantically similar requests, not just exact matches
+- **Multiple embedding provider support**: Works with OpenAI, Mistral, and Azure OpenAI embedding services
+- **Multiple vector database support**: Supports Redis and Milvus as vector storage backends
+- **Configurable similarity threshold**: Control cache hit sensitivity (0.0 to 1.0)
+- **JSONPath extraction**: Extract specific fields from request body for embedding generation
+- **Automatic cache management**: Stores successful responses (200) automatically after upstream calls
+- **Immediate response on cache hit**: Returns cached response with `X-Cache-Status: HIT` header without upstream call
+- **TTL support**: Configurable time-to-live for cache entries
 
-Set that threshold deliberately. Too loose and the gateway answers one question with another question's answer.
+## How It Works
 
-## Caching policies
+### Request Phase
 
-This policy is documented in the [Policy Hub](https://wso2.com/api-platform/policy-hub), the versioned reference for every API Platform policy. For policy categories and how policies chain, see the [Policy Hub overview](../../policy-hub/overview.md).
+1. **Text Extraction**: Extracts text from the request body using JSONPath (if configured) or uses the entire request body
+2. **Embedding Generation**: Generates a vector embedding from the extracted text using the configured embedding provider
+3. **Cache Lookup**: Searches the vector database for semantically similar cached responses using cosine similarity
+4. **Threshold Check**: If a similar embedding is found with similarity >= similarityThreshold, returns the cached response immediately
+5. **Cache Miss**: If no similar response is found, the request proceeds to the upstream service
 
-| Policy | What it does |
-|--------|--------------|
-| [Semantic Cache](https://wso2.com/api-platform/policy-hub/policies/semantic-cache) | Caches LLM responses using vector similarity, returning cached results for semantically equivalent prompts |
+### Response Phase
 
-## Related topics
+1. **Success Check**: Only processes responses with 200 status codes
+2. **Embedding Retrieval**: Retrieves the embedding generated during the request phase from metadata
+3. **Response Storage**: Stores the response payload along with its embedding in the vector database
+4. **TTL Application**: Applies the configured TTL to the cache entry
 
-- [Set up a governed multi-model LLM proxy](../../guides/ai-and-mcp/set-up-a-governed-multi-model-llm-proxy-with-cost-controls-and-failover.md) — distributes traffic across models behind one proxy, with per-team token budgets, PII masking, and semantic caching.
-- [Cost control and budgets](cost-control-and-budgets.md) — put a monetary ceiling on the calls that do reach a model.
-- [Prompt management](prompt-management.md) — compress a prompt to reduce the tokens a cache miss costs.
+## Configuration
+
+### Policy Parameters
+
+| Parameter | Type | Required | Default | Description |
+|-----------|------|----------|---------|-------------|
+| `similarityThreshold` | number | Yes | - | Similarity threshold for cache hits (0.0 to 1.0). Higher values require more similarity. For example, 0.9 means 90% similarity required. Recommended: 0.85-0.95 for strict matching, 0.70-0.85 for more flexible matching. |
+| `jsonPath` | string | No | `""` | JSONPath expression to extract text from request body for embedding generation. If empty, uses the entire request body. Example: `"$.messages[0].content"` to extract the first message's content. |
+
+### System Parameters (Required)
+
+These parameters are typically configured at the gateway level and automatically injected, or you can override those values from the params section in the api artifact definition file as well:
+
+#### Embedding Provider Configuration
+
+| Parameter | Type | Required | Description |
+|-----------|------|----------|-------------|
+| `embeddingProvider` | string | Yes | Embedding provider type. Must be one of: `OPENAI`, `MISTRAL`, `AZURE_OPENAI` |
+| `embeddingEndpoint` | string | Yes | Endpoint URL for the embedding service. Examples: OpenAI: `https://api.openai.com/v1/embeddings`, Mistral: `https://api.mistral.ai/v1/embeddings`, Azure OpenAI: Your Azure OpenAI endpoint URL |
+| `embeddingModel` | string | Conditional | - | Embedding model name. **Required for OPENAI and MISTRAL**, not required for AZURE_OPENAI (deployment name is in endpoint URL). Examples: OpenAI: `text-embedding-ada-002` or `text-embedding-3-small`, Mistral: `mistral-embed` |
+| `embeddingDimension` | integer | Yes | Dimension of embedding vectors. Common values: 1536 (OpenAI ada-002), 1024 (Mistral). Must match the model's output dimension. |
+| `apiKey` | string | Yes | API key for the embedding service authentication. The authentication header is automatically set to `api-key` for Azure OpenAI and `Authorization` for other providers. |
+
+#### Vector Database Configuration
+
+| Parameter | Type | Required | Description |
+|-----------|------|----------|-------------|
+| `vectorStoreProvider` | string | Yes | Vector database provider. Must be one of: `REDIS`, `MILVUS` |
+| `dbHost` | string | Yes | Vector database host address |
+| `dbPort` | integer | Yes | Vector database port number |
+| `username` | string | No | Database username for authentication (if required) |
+| `password` | string | No | Database password for authentication (if required) |
+| `database` | string | No | Database name or index number (for Redis) |
+| `ttl` | integer | No | Time-to-live for cache entries in seconds. Default is 3600 (1 hour). Set to 0 for no expiration. |
+
+
+### Configuring System Parameters in config.toml
+
+System parameters can be configured globally in the gateway's `config.toml` file. These values serve as defaults for all Semantic Cache policy instances and can be overridden per-policy in the API configuration if needed.
+
+#### Location in config.toml
+
+Add the following configuration section to your `config.toml` file:
+
+```toml
+embedding_provider = "MISTRAL" # Supported: MISTRAL, OPENAI, AZURE_OPENAI
+embedding_provider_endpoint = "https://api.mistral.ai/v1/embeddings"
+embedding_provider_model = "mistral-embed"
+embedding_provider_dimension = 1024
+embedding_provider_api_key = ""
+
+vector_db_provider = "REDIS" # Supported: REDIS, MILVUS
+vector_db_provider_host = "redis"
+vector_db_provider_port = 6379
+vector_db_provider_database = "0"
+vector_db_provider_username = "default"
+vector_db_provider_password = "default"
+vector_db_provider_ttl = 3600
+```
+
+## JSONPath Support
+
+The policy supports JSONPath expressions to extract specific text from request bodies before generating embeddings. This is useful for:
+- Extracting message content from chat completion requests
+- Focusing on specific prompt fields while ignoring metadata
+- Handling structured JSON payloads
+
+### Common JSONPath Examples
+
+- `$.messages[0].content` - First message's content in chat completions
+- `$.messages[-1].content` - Last message's content
+- `$.prompt` - Extract prompt field from completions API
+- `$.input` - Extract input field from embeddings API
+- `$` - Entire request body (default if jsonPath is not specified)
+
+## Examples
+
+### Example 1: OpenAI Embeddings with Redis
+
+Deploy an LLM provider with semantic caching using OpenAI embeddings and Redis vector store:
+
+For local or development environments only, the default credentials may be `admin:admin` encoded as `YWRtaW46YWRtaW4=`.
+
+```bash
+curl -X POST http://localhost:9090/llm-providers \
+  -H "Content-Type: application/yaml" \
+  -H "Authorization: Basic <BASE64_CREDENTIAL>" \
+  --data-binary @- <<'EOF'
+apiVersion: gateway.api-platform.wso2.com/v1alpha1
+kind: LlmProvider
+metadata:
+  name: cached-chat-provider
+spec:
+  displayName: OpenAI Cached Provider
+  version: v1.0
+  template: openai
+  vhost: openai
+  upstream:
+    url: "https://api.openai.com/v1"
+    auth:
+      type: api-key
+      header: Authorization
+      value: Bearer <openai-apikey>
+  accessControl:
+    mode: deny_all
+    exceptions:
+      - path: /chat/completions
+        methods: [POST]
+  policies:
+    - name: semantic-cache
+      version: v1
+      paths:
+        - path: /chat/completions
+          methods: [POST]
+          params:
+            similarityThreshold: 0.85
+            jsonPath: "$.messages[0].content"
+EOF
+```
+
+**Test the semantic cache:**
+
+**Note**: Ensure that "openai" is mapped to the appropriate IP address (e.g., 127.0.0.1) in your `/etc/hosts` file, or remove the vhost from the LLM provider configuration and use localhost to invoke.
+
+```bash
+# First request - cache miss, will call upstream
+curl -X POST http://openai:8080/chat/completions \
+  -H "Content-Type: application/json" \
+  -H "Host: openai" \
+  -d '{
+    "model": "gpt-4",
+    "messages": [
+      {
+        "role": "user",
+        "content": "Explain quantum computing in simple terms"
+      }
+    ]
+  }'
+
+# Second request with similar but different wording - cache hit!
+curl -X POST http://openai:8080/chat/completions \
+  -H "Content-Type: application/json" \
+  -H "Host: openai" \
+  -d '{
+    "model": "gpt-4",
+    "messages": [
+      {
+        "role": "user",
+        "content": "Can you describe quantum computing using simple language?"
+      }
+    ]
+  }'
+# Response will include: X-Cache-Status: HIT
+```
+
+## Use Cases
+
+1. **Cost Reduction**: Reduce API costs by serving cached responses for similar queries, especially valuable for expensive LLM API calls.
+
+2. **Latency Improvement**: Return cached responses in milliseconds instead of waiting for LLM processing (typically 1-5 seconds), significantly improving user experience.
+
+3. **Rate Limit Management**: Reduce the number of upstream API calls, helping stay within rate limits and avoiding throttling.
+
+4. **Consistency**: Ensure users receive consistent responses for semantically equivalent queries, improving predictability.
+
+5. **Offline Resilience**: Serve cached responses even when upstream services experience temporary outages.
+
+6. **A/B Testing**: Compare cached vs. fresh responses to evaluate prompt engineering improvements.
+
+7. **Development/Testing**: Speed up development cycles by reusing cached responses during testing.
+
+8. **High-Traffic Applications**: Handle high volumes of similar queries efficiently without overwhelming upstream services.
+
+## Similarity Threshold Guidelines
+
+The `similarityThreshold` parameter controls how similar requests must be to trigger a cache hit:
+
+- **0.95-1.0**: Very strict matching. Only near-identical requests will hit cache. Use for exact-match scenarios.
+- **0.85-0.94**: Recommended for most use cases. Catches semantically equivalent requests with some wording variation.
+- **0.75-0.84**: More flexible matching. Useful for broader conceptual similarity.
+- **0.60-0.74**: Very flexible. May return cached responses for loosely related queries.
+- **Below 0.60**: Not recommended. Risk of returning irrelevant cached responses.
+
+**Recommendation**: Start with 0.85 and adjust based on your use case. Monitor cache hit rates and response relevance to fine-tune.
+
+## Cache Behavior
+
+### Cache Hit
+
+When a similar request is found:
+- Returns cached response immediately (no upstream call)
+- Adds `X-Cache-Status: HIT` header to response
+- Status code: 200 (from cached response)
+- Response time: Typically < 50ms (vs. 1-5 seconds for LLM APIs)
+
+### Cache Miss
+
+When no similar request is found:
+- Request proceeds to upstream service normally
+- Response is cached after successful upstream call (200 status)
+- Subsequent similar requests may hit the cache
+
+### Cache Storage
+
+- Only successful responses (200 status code) are cached
+- Responses are stored with their embeddings in the vector database
+- TTL is applied to all cache entries
+- Each route/API maintains a separate cache namespace to avoid cross-contamination
+
+## Error Handling
+
+The policy is designed to be resilient:
+
+- **Embedding Generation Failure**: If embedding generation fails, the request proceeds to upstream (cache is skipped)
+- **Vector Database Unavailable**: If the vector database is unreachable, requests proceed to upstream
+- **Cache Storage Failure**: If storing a response fails, the response is still returned to the client (cache operation is non-blocking)
+- **Invalid JSONPath**: If JSONPath extraction fails, the entire request body is used for embedding generation
+
+These behaviors ensure that caching failures do not block legitimate requests. The system gracefully degrades to direct upstream calls when caching is unavailable.
+
+## Performance Considerations
+
+1. **Embedding Generation Latency**: Generating embeddings adds ~100-500ms to request processing. This is offset by cache hits that save 1-5 seconds.
+
+2. **Vector Database Performance**: 
+   - Redis with RedisSearch: Fast queries, good for smaller datasets (< 1M vectors)
+   - Milvus: Optimized for large-scale vector search, better for > 1M vectors
+
+3. **Cache Hit Rate**: Aim for 20-40% cache hit rate for cost-effective caching. Below 10% may not justify the overhead.
+
+4. **Embedding Dimension**: Higher dimensions (e.g., 1536) provide better accuracy but increase storage and search time. Choose based on your quality requirements.
+
+5. **Index Creation**: Vector database indexes are created automatically on first use. This may take a few seconds for large datasets.
+
+## Notes
+
+- The policy requires both request and response phases to function properly (generates embeddings in request phase, stores responses in response phase).
+
+- Embedding generation adds latency to each request (~100-500ms). This overhead is typically offset by the performance gains from cache hits.
+
+- Cache entries are scoped per route/API to prevent cross-contamination between different APIs or routes.
+
+- Only responses with 200 status code are cached. Errors and non-200 responses are never cached.
+
+- The similarity search uses cosine similarity to compare embeddings. This is optimal for semantic similarity matching.
+
+- Vector database indexes are created automatically when the policy is first used. Ensure your vector database has sufficient resources.
+
+- The policy maintains provider instances per route for efficiency. Configuration changes require policy reinitialization.
+
+- TTL of 0 means no expiration. Use with caution as it may lead to unbounded cache growth.
+
+- JSONPath extraction is optional. If not specified, the entire request body (as string) is used for embedding generation.
+
+- The policy stores embeddings in metadata between request and response phases. Ensure metadata persistence is enabled in your gateway configuration.
+
+- For production deployments, monitor cache hit rates, embedding generation latency, and vector database performance metrics to optimize configuration.
```

</details>

### cloud/ai-gateway/observability/tracing.md

Main-line page `docs/guides/logging-and-tracing/tracing.mdx`; word F1 0.999.

<details><summary>Diff</summary>

```diff
--- main line: ai-gateway/next/logging-and-tracing/tracing.md
+++ Cloud: cloud/ai-gateway/observability/tracing.md
@@ -1,3 +1,3 @@
-# Gateway tracing
+# Gateway Tracing
 
 This guide explains how to implement and configure distributed tracing for the API Platform Gateway components.
@@ -75,5 +75,5 @@ To run only the core gateway services without the demonstration tracing stack:
 
 ```bash
-docker compose up
+docker compose up -d
 ```
 
@@ -874,4 +874,5 @@ This provides complete observability:
 - [OpenTelemetry Collector Documentation](https://opentelemetry.io/docs/collector/)
 - [W3C Trace Context Specification](https://www.w3.org/TR/trace-context/)
-- [Gateway logs](gateway-logs.md)
+- [Gateway Overview](../overview.md)
+- [Gateway Logging Guide](logging.md)
 - [Docker Compose Profiles](https://docs.docker.com/compose/profiles/)
```

</details>
