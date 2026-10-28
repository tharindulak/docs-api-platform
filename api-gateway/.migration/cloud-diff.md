# API Gateway: Cloud pages against the main line

The main line is seeded from the newest Self-hosted line; pages found only in the Cloud sub-section are added and marked Cloud only (Platform-by-platform walkthrough, rule 4). A Cloud page with the same name as a main-line page is **not** added: the main line keeps its own text, and the Cloud page's legacy URL maps to it. This report lists those pairs so the team can decide each one by PR. Converted from `wso2/docs-api-platform@e9987cde09f3f6859357429a051aa04ee461c13b`.

- Pairs: 2 (0 identical, **2 differ**)
- Cloud-only pages added: 14
- Cloud-only pages whose file name several pages share (possible counterparts, not paired): 1

| Cloud page (legacy) | Main-line page | Paired by | Word F1 | Lines +/− | |
|---|---|---|---|---|---|
| [cloud/api-platform-gateway/overview.md](https://wso2.com/api-platform/docs/cloud/api-platform-gateway/overview/) | `docs/index.mdx` (from api-gateway/next/overview.md) | same path | 0.360 | +111 / −58 | **differs** |
| [cloud/api-platform-gateway/writing-a-custom-policy.md](https://wso2.com/api-platform/docs/cloud/api-platform-gateway/writing-a-custom-policy/) | `docs/guides/policies/custom-policies/writing-a-custom-policy.mdx` (from api-gateway/next/policies/custom-policies/writing-a-custom-policy.md) | same file name | 0.969 | +10 / −3 | **differs** |

## Possible counterparts (not paired)

- `cloud/api-platform-gateway/publish-apis/overview.md` (added as Cloud only); same file name as `api-gateway/next/deployment/deployment-modes/kubernetes/overview.md`, `api-gateway/next/gateway-controller-management-api/overview.md`, `api-gateway/next/observability/metrics/overview.md`, `api-gateway/next/observability/tracing/overview.md`, `api-gateway/next/performance/overview.md`, `api-gateway/next/policies/overview.md`

## Differences

Each diff reads from the main-line text (`-`) to the Cloud text (`+`), front matter left out.

### cloud/api-platform-gateway/overview.md

Main-line page `docs/index.mdx`; word F1 0.360.

<details><summary>Diff</summary>

```diff
--- main line: api-gateway/next/overview.md
+++ Cloud: cloud/api-platform-gateway/overview.md
@@ -1,75 +1,128 @@
 # API Platform Gateway Overview
 
-API Platform Gateway is the complete API gateway system for managing, securing, and routing API traffic to your backend services.
+API Platform provides two types of API Platform gateways powered by WSO2, giving you flexibility to choose the deployment model that best fits your requirements. Both gateway types are managed through API Platform's unified control plane, ensuring consistent API management, policy enforcement, and monitoring across all your environments.
 
-## Components
+## Gateway Types
 
-| Component | Purpose |
-|-----------|---------|
-| **Gateway-Controller** | Control plane that manages API configurations and dynamically configures the Router |
-| **Gateway-Runtime** | Data plane (Envoy Proxy) that routes HTTP/HTTPS traffic to backend services and Processes requests/responses through configurable policies (authentication, rate limiting, etc.)|
-| **Policy Builder** | Build-time tooling for compiling custom policy implementations |
+### API Platform Cloud Gateway (SaaS)
 
-### CLI Tool (ap)
+The API Platform Cloud Gateway is a fully managed, WSO2-hosted gateway that requires zero infrastructure management on your part.
 
-The `ap` CLI provides a command-line interface for managing gateways, APIs, and MCP proxies. Key capabilities include:
+| Aspect | Description |
+|--------|-------------|
+| **Deployment** | WSO2-managed cloud infrastructure |
+| **Management** | Fully managed by WSO2 |
+| **Availability** | High availability with automatic failover |
+| **Scaling** | Automatic scaling based on traffic |
+| **Maintenance** | Zero maintenance required |
 
-- Gateway management (add, list, remove, health check)
-- API lifecycle management (apply, list, get, delete)
-- MCP proxy management (generate, list, get, delete)
+**Best for:**
 
-For the complete list of CLI commands and usage examples, see the [CLI Reference](../../tools/cli/reference.md).
+- Teams wanting to get started quickly without infrastructure setup
+- Organizations preferring a fully managed solution
+- Projects where time-to-market is critical
+- Workloads without strict data residency requirements
 
-## Default Ports
+### Self-Hosted Gateway
 
-| Port | Service | Description |
-|------|---------|-------------|
-| 8080 | Router | HTTP traffic |
-| 8443 | Router | HTTPS traffic |
-| 9090 | Gateway-Controller | REST API |
-| 9094 | Gateway-Controller Admin | Health and admin endpoints |
+The Self-Hosted Gateway is a containerized instance of the API Platform Gateway that you deploy and manage in your own infrastructure—on-premises, in a private cloud, or in any public cloud provider.
 
-## Architecture
-
-![Architecture diagram showing Gateway Controller with REST API, Configuration Transformer, xDS Server, and Repository Controller above, and Gateway Runtime with Envoy Router, Policy Engine, and Python Executor below](../../assets/img/api-gateway/gateway-architecture.png)
-<!-- image source: https://docs.google.com/drawings/d/1pgADdQNpNcvLrLVvV1fx2hxQOb3syoU0DEBhJd2N6Aw/edit?usp=sharing -->
-
-The API Gateway consists of two main components: **Gateway Controller** and **Gateway Runtime**.
-
-- **Gateway Controller** is the control plane that manages API configurations and pushes them to the Gateway Runtime via the xDS protocol.
-- **Gateway Runtime** is the data plane that processes API traffic. It contains three sub-components:
-  - **Router** (Envoy proxy) — handles traffic routing, load balancing, and TLS termination.
-  - **Policy Engine** — an ext_proc filter that executes request/response policies. **Go-based** policies are compiled into the Policy Engine binary at image build time by the Gateway Builder.
-  - **Python Executor** — a dedicated runtime component that dynamically evaluates Python-based policies, allowing developers to leverage the extensive Python ecosystem for custom logic.
-
-The Gateway Controller configures the Gateway Runtime by pushing API and route configurations through xDS. When a request arrives, the Router forwards it to the Policy Engine for policy evaluation, then routes it to the upstream backend.
-
-### How it works
+| Aspect | Description |
+|--------|-------------|
+| **Deployment** | Your infrastructure (Kubernetes, Docker, VM) |
+| **Management** | You manage the runtime; API Platform manages configuration |
+| **Availability** | You control redundancy and failover |
+| **Scaling** | You control scaling based on your needs |
+| **Maintenance** | You handle runtime updates and patches |
 
-1. User verifies the Gateway-Controller admin health endpoint
-2. User submits API configuration (YAML/JSON) to the Gateway-Controller REST API
-3. Gateway-Controller validates and persists the configuration
-4. Router receives the updated configuration and starts routing traffic
+**Best for:**
 
-### Policies
+- Organizations with strict compliance or data residency requirements
+- Workloads requiring low-latency access to on-premises backends
+- Environments with private/non-public backend services
+- Teams needing full control over the gateway runtime
 
-Policies allow you to intercept and transform API traffic at the Gateway-Runtime (Envoy Proxy). The Gateway offers a flexible, dual-language approach to policy development, empowering teams to build custom API logic tailored to their performance and ecosystem needs.
+## Comparison
 
-- **Go:** Compiled directly into the Policy Engine binary, Go provides maximum execution performance, strict type safety, and minimal latency for critical path operations.
-- **Python:** Executed dynamically by the integrated Python Executor, Python is particularly ideal for AI/ML use cases and complex data transformations due to its extensive ecosystem support and specialized libraries.
+| Feature | API Platform Cloud Gateway | Self-Hosted Gateway |
+|---------|---------------------|---------------------|
+| Infrastructure management | WSO2 | You |
+| Data residency control | WSO2 cloud regions | Your choice |
+| Backend connectivity | Public endpoints | Public and private |
+| Setup time | Instant | Requires deployment |
+| Scaling | Automatic | Manual or auto (your infra) |
+| Cost model | Usage-based | Infrastructure + usage |
+| Unified control plane | ✓ | ✓ |
+| Policy Hub integration | ✓ | ✓ |
+| Monitoring & analytics | ✓ | ✓ |
 
-Policies can be applied to request and response flows to handle concerns like authentication, rate limiting, header manipulation, and more.
-
-The complete and up-to-date policy catalogue — with configuration references and examples — is maintained in the gateway-controllers repository: https://github.com/wso2/gateway-controllers/blob/main/docs/README.md
-
-You can extend the gateway with your own policies or include specific policies from the catalogue by building a custom gateway image using the `ap` CLI. See [Building the Gateway with Custom Policies](./policies/custom-policies/building-gateway-with-custom-policies.md).
-
-## High Availability Setup
-
-In a production HA deployment:
-
-- **Gateway Controller** instances connect to a shared external database (**PostgreSQL** or **SQL Server**) for persistent storage of API configurations, subscriptions, and other metadata.
-- **Gateway Runtime** instances connect to a shared **Redis** instance used for distributed rate limiting, ensuring rate limit counters are synchronized across all runtime instances.
+## Architecture
 
-![HA diagram with two Gateway Controller replicas sharing PostgreSQL, three Gateway Runtime replicas sharing Redis, and all runtimes reporting to Moesif analytics](../../assets/img/api-gateway/gateway-ha-setup.png)
-<!-- image source: https://docs.google.com/drawings/d/1CIH3V8Uc2YxCWEGS7yUz3qyBfSpdLK1VpWK0NgmP4OQ/edit?usp=sharing -->
+Both gateway types connect to API Platform's unified control plane:
+
+```
+┌─────────────────────────────────────────────────────────────────┐
+│                     API Platform Control Plane                  │
+│  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────────┐  │
+│  │ API Manager │  │ Policy Hub  │  │ Monitoring & Analytics  │  │
+│  └─────────────┘  └─────────────┘  └─────────────────────────┘  │
+└───────────┬───────────────────────────────────┬─────────────────┘
+            │                                   │
+            ▼                                   ▼
+┌───────────────────────────────┐    ┌───────────────────────────┐
+│  API Platform Cloud Gateway   │    │    Your Environment       │
+│  (WSO2-Managed)               │    │  ┌─────────────────────┐  │
+│  ┌─────────────────┐          │    │  │  Self-Hosted Gateway│  │
+│  │  Gateway Cluster│          │    │  │  ┌─────┐ ┌─────┐    │  │
+│  └─────────────────┘          │    │  │  │ GW1 │ │ GW2 │    │  │
+└───────────────────────────────┘    │  │  └─────┘ └─────┘    │  │
+                                     │  └─────────────────────┘  │
+                                     │           │               │
+                                     │           ▼               │
+                                     │  ┌─────────────────────┐  │
+                                     │  │  Backend Services   │  │
+                                     │  └─────────────────────┘  │
+                                     └───────────────────────────┘
+```
+
+## Common Features
+
+Both gateway types share these capabilities through the unified control plane:
+
+| Feature | Description |
+|---------|-------------|
+| **Unified Management** | Manage all APIs and gateways from a single control plane |
+| **Centralized Policies** | Define and enforce policies through the Policy Hub |
+| **Real-time Sync** | Automatic synchronization of API configurations and policies |
+| **Health Monitoring** | Monitor gateway health and performance |
+| **Analytics** | Unified API analytics and insights |
+| **Developer Portal** | Expose APIs to developers through the portal |
+
+## Getting Started
+
+### Using API Platform Cloud Gateway
+
+The API Platform Cloud Gateway is available by default in your organization. Simply deploy your APIs and they will be routed through the managed gateway.
+
+1. Create an API proxy in the API Platform Console.
+2. Deploy the API to an environment.
+3. The API is automatically available through the cloud gateway.
+
+For more details, see [API Platform Cloud Gateway](cloud-gateway.md).
+
+### Using Self-Hosted Gateway
+
+To deploy a Self-Hosted Gateway in your environment:
+
+1. **[Getting Started](getting-started.md)**: Quick start guide to set up your first gateway.
+2. **[Setting Up](setting-up.md)**: Detailed configuration for VM, Docker, and Kubernetes.
+3. **[Adding and Managing Policies](manage-policies.md)**: Configure and enforce policies.
+4. **[Analytics](analytics.md)**: Monitor API traffic and performance.
+
+## What's Next?
+
+- [Getting Started](getting-started.md): Quick start guide for Self-Hosted Gateway
+- [Setting Up](setting-up.md): Configure for VM, Docker, or Kubernetes
+- [Adding and Managing Policies](manage-policies.md): Configure and enforce policies
+- [Analytics](analytics.md): Monitor API traffic and performance
+- [Troubleshooting](troubleshooting.md): Common issues and solutions
```

</details>

### cloud/api-platform-gateway/writing-a-custom-policy.md

Main-line page `docs/guides/policies/custom-policies/writing-a-custom-policy.mdx`; word F1 0.969.

<details><summary>Diff</summary>

```diff
--- main line: api-gateway/next/policies/custom-policies/writing-a-custom-policy.md
+++ Cloud: cloud/api-platform-gateway/writing-a-custom-policy.md
@@ -1,8 +1,13 @@
-# Writing a Custom Policy
+# Writing a Custom Policy for the Self-Hosted Gateway
 
-This guide shows how to write a custom policy in API Platform Gateway.
+This guide shows how to build a custom policy using the gateway SDK.
 
 For full API details, see the [API Platform Gateway's Custom Policy SDK Documentation](https://pkg.go.dev/github.com/wso2/api-platform/sdk/core/policy/v1alpha2).
 
+## What is a Policy?
+
+Policies allow you to enforce security, rate limiting, transformation, and other governance requirements on your APIs.
+
+
 ## How It Works
 
@@ -352,3 +357,5 @@ policies:
 ## What's Next?
 
-- [Building the Gateway with Custom Policies](building-gateway-with-custom-policies.md): Build a gateway image that includes your custom policy
+- [Building the Gateway with Custom Policies](build-gateway-with-custom-policies.md): Build a gateway image that includes your custom policy
+- [Apply Custom Policies to APIs](apply-custom-policies-to-apis.md): Sync your custom policy to the organization and apply it to APIs
+- [Writing an AI Policy](../ai-workspace/policies/writing-an-ai-policy.md): Learn how to write policies for LLM traffic
```

</details>
