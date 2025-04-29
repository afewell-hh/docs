---
title: Deploy Fabric CLI (kubectl plugin)
version: Hedgehog v1.0.0
last-verified: 2025-04-29
type: How-to
---

## Overview

This guide explains how to verify and use the Hedgehog Fabric CLI plugin (`kubectl fabric`). It covers checking installation, basic operations, and troubleshooting common issues.

**Learning Objectives**
- Verify Fabric CLI plugin installation
- Execute core Fabric CLI commands
- Diagnose and resolve CLI issues

**Prerequisites**
- `kubectl` configured for your Kubernetes cluster with Hedgehog Fabric deployed
- Optional: `hhfab` CLI tool for plugin installation (see [Deploy Fabricator CLI](deploying-cli.md))

## 1. Verifying Installation

Run:
```bash
kubectl fabric version
```
Expected output:
```console
v0.58.0
```

If the command is unrecognized:
1. Install via fabricator CLI:
   ```bash
   hhfab cli install
   ```
2. Alternatively, use control node access where the plugin is pre-installed.

## 2. Common Commands

### List VPCs
```bash
kubectl fabric vpc list
```

### Create a VPC
```bash
kubectl fabric vpc create my-vpc --subnet 10.1.0.0/16
```

### Inspect a Switch
```bash
kubectl fabric inspect switch --name leaf-01
```

## 3. Troubleshooting

- Ensure `KUBECONFIG` points to a valid cluster.
- Confirm plugin binary is in your `$PATH` (e.g., `~/.kubectl/plugins/`).
- Review plugin errors with:
  ```bash
  kubectl fabric --help
  ```

## Cross-References
- [Fabric CLI Reference](../reference/fabric-cli.md)
- [Getting Started](../tutorial/getting-started.md)
- [Fabric API Reference](../reference/fabric-api.md)
- [Deploy Fabricator CLI](deploying-cli.md)

---

## How-to Quality Checklist
- [x] Step-by-step, active voice
- [x] Code samples versioned and accurate
- [x] Cross-links to reference and related docs
- [x] Prerequisites and learning objectives defined

*This guide follows Diátaxis How-to standards.*
