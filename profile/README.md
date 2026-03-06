# TinySystems

**Kubernetes-native workflow engine for building data pipelines, API servers, and automations.**

Design flows visually. Deploy as Kubernetes operators. Scale with your cluster.

---

### How it works

Each **flow** is a graph of connected **nodes**. Each node is an instance of a **component** — a small, focused piece of logic (HTTP server, router, Slack sender, K8s deployment scaler, etc.). Components are packaged into **modules** that run as Kubernetes operators.

```
HTTP Request → Router → Slack Notify
                     → Scale Deployment
```

- Nodes within the same module communicate via Go channels (zero serialization)
- Nodes across modules communicate via gRPC (automatic discovery)
- State lives in CRDs — no external database required in your cluster
- Blocking I/O — responses flow back through the same call chain

### Get started

1. **Use the platform** — [tinysystems.io](https://tinysystems.io) provides a visual editor, module directory, and cluster management
2. **Use the desktop client** — open-source [Wails app](https://github.com/tiny-systems/desktop-client) that connects directly to your cluster
3. **Build your own module** — install the [SDK](https://github.com/tiny-systems/module) and implement the `Component` interface:

```go
func (c *MyComponent) Handle(ctx context.Context, output module.Handler, port string, msg any) any {
    req := msg.(Request)
    result := process(req)
    return output(ctx, "response", Response{Context: req.Context, Data: result})
}
```

```shell
helm repo add tinysystems https://tiny-systems.github.io/module/
helm install my-module tinysystems/tinysystems-operator \
  --set controllerManager.manager.image.repository=myregistry/my-module
```

### Core repositories

| Repository | Description |
|---|---|
| [module](https://github.com/tiny-systems/module) | Go SDK — Kubebuilder-based library for building modules |
| [common-module](https://github.com/tiny-systems/common-module) | Router, ticker, cron, signal, KV store, array split |
| [http-module](https://github.com/tiny-systems/http-module) | HTTP server and client |
| [kubernetes-module](https://github.com/tiny-systems/kubernetes-module) | Pod watch, deployment scale/restart, configmap patch |
| [communication-module](https://github.com/tiny-systems/communication-module) | Slack, email (SMTP/SendGrid) |
| [encoding-module](https://github.com/tiny-systems/encoding-module) | JSON encode/decode, Go templates |
| [googleapis-module](https://github.com/tiny-systems/googleapis-module) | Firestore, Google APIs |
| [grpc-module](https://github.com/tiny-systems/grpc-module) | gRPC client with reflection-based discovery |
| [js-module](https://github.com/tiny-systems/js-module) | JavaScript evaluation |
| [desktop-client](https://github.com/tiny-systems/desktop-client) | Wails desktop app |
| [otel-collector](https://github.com/tiny-systems/otel-collector) | In-memory OpenTelemetry collector for real-time metrics |
| [ajson](https://github.com/tiny-systems/ajson) | JSONPath library powering expression evaluation |

### Key design decisions

- **Flow-based programming** — each node does one thing well (Unix philosophy)
- **Blocking I/O** — HTTP server blocks until response flows back through the graph
- **No central database** — all runtime state in Kubernetes CRDs
- **Modules are operators** — standard Kubernetes deployment, scaling, and RBAC
- **Expressions, not code** — data mapping between nodes uses `{{$.field}}` JSONPath syntax
- **Leader-reader pattern** — horizontal scaling with leader election for stateful operations

### Links

- [Documentation](https://docs.tinysystems.io/)
- [Platform](https://tinysystems.io)
