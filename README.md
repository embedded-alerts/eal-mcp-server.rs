# Embedded Alerts MCP Server

    Read-only MCP diagnostics for embedding rules, events, delivery, and acknowledgement contracts. The server is a Rust MCP process over stdio. Stdout is exclusively the JSON-RPC wire; structured diagnostics go to stderr and optional OTLP.

    ## Tools

    - `eal_fleet_map`
- `eal_plan`
- `eal_runtime_readiness`
- `eal_shared_platform`
- `eal_lifecycle_state`
- `eal_safety_boundary`

    Every tool is read-only. Planning accepts a closed workload enum plus bounded numeric fields. The server has no arbitrary URL, command, filesystem, database, GitHub mutation, cluster mutation, or secret-value input.

    ## Product topology

    - `eal-api` — rule and delivery-state API
- `eal-interfaces` — embedding, rule, event, and transport contracts
- `embedded-alerts-libs` — provider, evaluation, delivery, and policy libraries
- `eal-sync` — offline-first alert and acknowledgement sync
- `eal-infra` — Kubernetes and bounded Cloudflare edge infrastructure

    ## Security boundary

    - The MCP surface never emits alerts, modifies rules, or acknowledges delivery.
- Embedding inputs and alert payloads are excluded from tools and telemetry.
- Provider readiness is presence-only and does not claim successful authentication.

    The shared core is pinned at `c6101656c8227251d1dbd61df54f03a186b42ade`. It provides bounded MCP framing, explicit OTLP/gRPC traces, metrics and logs, JSON stderr diagnostics, redaction, low-cardinality tool metrics, and the formal runtime lifecycle. Each tool also owns an explicit span with `skip_all`; arguments and results are never recorded. Configuration readiness reports environment-variable presence only and performs no authentication or network request.

    This server contains no authenticated HTTP client. If a future tool adds one, it must use fixed or strictly validated HTTP(S) origins, reject credentials/query/fragment/private/metadata targets, disable redirects and ambient proxies, keep credentials in sensitive headers, cap every response, and add adversarial tests before merge.

    ## Shared platform knowledge

    The bounded `shared_platform` tool documents ORE Kubernetes, shared definitions, dpm, Cloudflare/Squarespace, Supabase, and Fiducia without exposing a mutation or credential surface.

    ## Validate

    ```sh
    cargo fmt --all -- --check
    cargo clippy --locked --all-targets --all-features -- -D warnings
    cargo test --locked --all-targets --all-features
    cargo build --locked --release
    cargo audit --deny warnings
    ```
