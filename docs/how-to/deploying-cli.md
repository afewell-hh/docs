---
title: Deploying Hedgehog Fabricator (hhfab)
version: Hedgehog v1.0.0
last-verified: 2025-04-29
hedgehog-release: v1.0.0
type: How-to
---

## Overview

**Note:** This guide covers the `hhfab` fabricator utility. To install the Fabric CLI plugin (`kubectl fabric`), see [Deploying Fabric CLI](deploying-fabric-cli.md).

**Learning Objectives**
- Install the Hedgehog Fabricator CLI (`hhfab`)
- Authenticate hhfab with GitHub Package Registry
- Initialize VLAB topology with hhfab

**Prerequisites**
- Docker installed and running
- ORAS CLI for OCI registries
- QEMU/KVM for VLAB
- Design Partner Agreement (early access)

This guide provides detailed, step-by-step instructions for deploying the Hedgehog CLI (`hhfab`) on supported platforms.
It covers prerequisites, obtaining access, installation, initial configuration, and basic validation.
The goal is to ensure you can reliably install and prepare the CLI for use with Hedgehog Fabric and VLAB environments.

> **Security Warning:**
> When using `curl | sh` or other install scripts, always review the script before running it.
> Download scripts from trusted sources only.
> See the [official install instructions](../getting-started/download.md) and [Security Model](../explanation/security-model.md) for more details.

---

## Prerequisites

- **Operating System:**
  - Linux x86/arm64 (tested on Ubuntu 24.04)
  - macOS x86/arm64 (latest major release)
  - Windows WSL2 (Ubuntu; not officially tested)
- **Docker:** Required for registry access and some deployment scenarios.
- **ORAS:** Required for downloading binaries from OCI registries.
- **QEMU/KVM:** Required for VLAB (Linux only).
- **Design Partner Agreement:** Required for early access (pre-GA).
- Review [Release Notes](../reference/release-notes.md) for version-specific caveats.

---

## 1. Requesting Access

1. Navigate to the [Hedgehog Support Portal](https://support.githedgehog.com/).
2. Submit a ticket requesting access to Hedgehog Fabricator (`hhfab`).
3. Upon approval, you will receive credentials for the [GitHub Package Registry](https://ghcr.io).

---

## 2. Authenticating with GitHub Package Registry

Use your provided credentials to authenticate Docker with the registry:

```bash
docker login ghcr.io --username <provided_user_name> --password <provided_token_string>
```

---

## 3. Installing ORAS (if not already installed)

[ORAS](https://oras.land/) is required to pull binaries from OCI registries. Install it with:

**Linux/macOS:**
```bash
curl -sSL https://install.oras.land/sh | sh
```

**Homebrew (macOS/Linux):**
```bash
brew install oras
```

> **Tip:** Always review installation scripts before executing them.
> For advanced installation or troubleshooting, see the [ORAS documentation](https://oras.land/docs/).

---

## 4. Downloading and Installing `hhfab`

- **Latest Stable Version:**
  ```bash
  curl -fsSL https://i.hhdev.io/hhfab | bash
  ```
- **Specific Version (e.g., 24.09):**
  ```bash
  curl -fsSL https://i.hhdev.io/hhfab | VERSION=24.09 bash
  ```
- **Custom Installation Directory:**
  ```bash
  curl -fsSL https://i.hhdev.io/hhfab | INSTALL_DIR=$HOME/bin bash
  ```

By default, `hhfab` is installed to `/usr/local/bin`. Use the `INSTALL_DIR` environment variable to override.

---

## 5. Verifying Installation

Check that `hhfab` is installed and accessible:

```bash
hhfab --version
```

Expected output (example):
```
Hedgehog Fabricator version=v0.36.1
```

---

## 6. Initializing Configuration

Before deploying or running VLAB, initialize the configuration:

```bash
hhfab init --dev
```

This creates a `fab.yaml` configuration file. Adjust settings as needed (credentials, modes, subnets, etc).

---

## 7. Troubleshooting

If you encounter issues during installation or authentication:
- Ensure your credentials are current and copied exactly (no whitespace).
- Check for Docker or ORAS installation errors; reinstall if needed.
- Ensure your network/firewall allows access to `ghcr.io` and the OCI registry.
- For common issues, see [Troubleshooting Fabric Deployments](../how-to/troubleshooting-fabric.md).
- Review [Release Notes](../reference/release-notes.md) for known issues.

---

## 8. Next Steps: Using the CLI

- **Generate VLAB Topology:**
  ```bash
  hhfab vlab gen
  ```
  This generates the default topology wiring file (`vlab.generated.yaml`).

- **Start VLAB:**
  Follow instructions in [Running VLAB](../vlab/running.md).

- **Reference:**
  - See [Fabric CLI Reference](../reference/fabric-cli.md) for command details.
  - See [VLAB Overview](../vlab/overview.md) for system requirements and architecture.

---

## What’s Next?
- [Getting Started: Deploy Your First Virtual Lab](../tutorial/getting-started-lab.md)
- [Demo Lab Walkthrough](../tutorial/demo-lab.md)
- [Reference: Fabric CLI](../reference/fabric-cli.md)
- [Troubleshooting Fabric Deployments](../how-to/troubleshooting-fabric.md)
- [Release Notes](../reference/release-notes.md)
- [Security Model](../explanation/security-model.md)

---

## Platform-Specific Notes

- **Linux:** Full support for all features, including VLAB.
- **macOS:** Supported for building installers/upgraders. VLAB is not supported.
- **Windows (WSL2):** May work but is not officially tested.

---

## How-to Quality Checklist
- [x] All prerequisites (OS, Docker, ORAS, credentials, security review) are met
- [x] Step-by-step, active voice used
- [x] Semantic line breaks throughout
- [x] Code samples, versioned and current
- [x] Explicit warnings and validation steps present
- [x] Cross-links to reference, troubleshooting, explanation docs
- [x] Consistent terminology and Diátaxis-compliant structure
- [x] No passive voice constructions
- [x] Instructions are actionable and strictly procedural

If you find any issues or gaps, please update this doc and the [tracking sheet](../_comparison-tracking.md).

---

<!--
Diátaxis: How-to Guide
Version: Hedgehog v1.0.0
Last verified: 2025-04-29
-->

*This document is maintained according to Diátaxis and Hedgehog quality standards. Please flag any inaccuracies or gaps for audit and improvement.*
