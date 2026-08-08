## Background

[Claude Code](https://claude.ai/code) is an AI coding assistant that supports **Skills** — slash commands defined as Markdown files in `.claude/commands/`. When a user types `/openyurt-deploy` inside the OpenYurt repository, Claude reads the skill file and executes the described steps interactively on behalf of the user.

Adding Skills to the OpenYurt repository would lower the barrier for operators who want to deploy OpenYurt or configure Raven on an existing Kubernetes cluster, without needing to read through the full documentation manually.

## Proposed Skills

### `/openyurt-deploy` — Deploy OpenYurt on an existing Kubernetes cluster

An interactive skill that:
1. Checks prerequisites (kubectl, Helm ≥ v3, Kubernetes ≥ 1.24)
2. Installs `yurt-manager` via Helm
3. Creates an Edge NodePool CR
4. Converts nodes to edge nodes using the label-driven `YurtNodeConversionController` mechanism (labels node with `apps.openyurt.io/nodepool=<name>`, waits for node-servant Job to complete)
5. Enables edge autonomy per node (`node.openyurt.io/autonomy-duration`)
6. Verifies the `Autonomy` condition on each edge node

### `/openyurt-raven` — Configure Raven for cross-region networking

An interactive skill that:
1. Verifies OpenYurt is already deployed
2. Installs `raven-agent` DaemonSet via Helm (from the `openyurtio/raven` repository)
3. Generates a VPN PSK with `openssl rand -hex 64`
4. Creates Gateway CRs for each NodePool (`raven.openyurt.io/v1beta1`)
5. Supports both `PublicIP` and `LoadBalancer` expose types
6. Supports enabling/disabling L3 tunnel and L7 proxy independently
7. Verifies cross-NodePool connectivity

## Implementation

The implementation adds `.claude/commands/` to the repository root:

```
.claude/commands/
├── openyurt-deploy.md
├── openyurt-raven.md
└── README.md
```

These are static Markdown files — no build changes, no code changes. The skills are picked up automatically by Claude Code when working inside the repository.

## Why This Is Useful

- **Lower onboarding friction**: operators can deploy OpenYurt end-to-end with a single slash command, with Claude executing and verifying each step
- **Accurate and versioned**: skills live in the repo alongside the code, so they can be updated with each release
- **Handles edge cases**: skills include error handling guidance (e.g. libreswan requirement for Raven, PSK mismatch, conversion Job failure diagnosis)

## Related

- Label-driven node conversion: #2533
- Native service topology: #2550
- Helm chart: `charts/yurt-manager/`, `charts/yurthub/`
- Raven: https://github.com/openyurtio/raven
