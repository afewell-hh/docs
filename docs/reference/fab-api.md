# Hedgehog Fabric CLI Reference

> **Note:** This page documents the Hedgehog Fabric CLI (`kubectl fabric`). For the REST/gRPC API, see [Fabric API Reference](./fabric-api.md).

---

**Version:** v0.58.0  
**Source:** [Hedgehog Fabricator CLI Docs (latest)](https://github.com/githedgehog/fabricator/blob/master/docs/api.md)

---

## Overview

The Hedgehog Fabric CLI is provided as a `kubectl` plugin: `kubectl fabric`.
This tool simplifies the management of Fabric resources in Kubernetes environments.
It wraps `kubectl` and the Kubernetes client, providing user-friendly commands for key Fabric operations.

> **Security Notice:**
> Some CLI commands (e.g., `power-reset`, `wipe`) may disrupt fabric operations or alter network state.
> Only run these commands in trusted environments and with appropriate permissions. See [Security Model](../explanation/security-model.md).

---

## Installation & Prerequisites

- `kubectl fabric` is automatically installed on Hedgehog Control Nodes.
- Requires access to a Kubernetes cluster with Hedgehog Fabric deployed.
- See [Getting Started](../tutorial/getting-started.md) for setup instructions.

---

## Usage

```console
kubectl fabric [global options] command [command options]
```

### Global Options

| Option           | Description                                   |
|------------------|-----------------------------------------------|
| `--verbose, -v`  | Verbose output (includes debug; default: true)|
| `--help, -h`     | Show help                                     |
| `--version, -V`  | Print the version                             |

---

## Commands Overview

- `create`: Create an external resource
- `peer, peering`: Peer external and VPC
- `wiring`: Helpers for wiring diagrams
- `inspect, i`: Inspect Fabric API objects and primitives

For a full list of commands and options, see the auto-generated CLI help:

```console
kubectl fabric --help
```

---

## Example Usage

Inspect a switch:
```console
kubectl fabric inspect switch --name <switch-name>
```

Inspect a VPC:
```console
kubectl fabric inspect vpc --name <vpc-name>
```

---

## Cross-References
- [How to Deploy the CLI](../how-to/deploying-cli.md)
- [Getting Started Tutorial](../tutorial/getting-started.md)
- [Troubleshooting](../how-to/troubleshooting.md)
- [Fabric API Reference](./fabric-api.md)
- [Release Notes](./release-notes.md)
- [Security Model](../explanation/security-model.md)

---

### Reference Checklist
- [x] Is this reference strictly descriptive (no how-to or explanation content)?
- [x] Is the CLI version and source clearly stated?
- [x] Are all cross-links present and up-to-date?
- [x] Are security notes included for potentially disruptive commands?
- [x] Does this doc use semantic line breaks and consistent terminology?
- [x] Are TODOs and open questions clearly flagged for future work?

If you find any issues or gaps, please update this doc and the [tracking sheet](../_comparison-tracking.md).

---

*This page is maintained according to the Diátaxis reference standards. Please flag any inaccuracies or gaps for audit and improvement.*
