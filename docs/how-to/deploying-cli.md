---
title: Deploying Hedgehog CLI
version: Hedgehog v1.0.0
type: How-to
---

## Overview

This guide provides detailed, step-by-step instructions for deploying the Hedgehog CLI (`hhfab`) on supported platforms. It covers prerequisites, obtaining access, installation, initial configuration, and basic validation. The goal is to ensure you can reliably install and prepare the CLI for use with Hedgehog Fabric and VLAB environments.

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

This creates a `fab.yaml` configuration file. Adjust settings as needed (credentials, modes, subnets, etc.).

---

## 7. Next Steps: Using the CLI

- **Generate VLAB Topology:**
  ```bash
  hhfab vlab gen
  ```
  This generates the default topology wiring file (`vlab.generated.yaml`).

- **Start VLAB:**
  Follow instructions in [Running VLAB](../vlab/running.md).

- **Reference:**
  - See [Fabric CLI Reference](../reference/cli.md) for command details.
  - See [VLAB Overview](../vlab/overview.md) for system requirements and architecture.

---

## Platform-Specific Notes

- **Linux:** Full support for all features, including VLAB.
- **macOS:** Supported for building installers/upgraders. VLAB is not supported.
- **Windows (WSL2):** May work but is not officially tested.

---

## Troubleshooting

- Ensure Docker and ORAS are installed and in your `PATH`.
- If you encounter permission issues, try running installation commands with `sudo` (Linux/macOS).
- For access issues, verify your credentials or contact Hedgehog Support.
- See [Troubleshooting Guide](troubleshooting.md) for more.

---

## Gaps
- [ ] Add screenshots for each step
- [ ] Add video walkthrough
- [ ] Add advanced configuration scenarios
- [ ] Confirm Windows/WSL2 compatibility details
- [ ] Link to release-specific installation notes

---

<!--
Diátaxis: How-to Guide
Version: Hedgehog v1.0.0
Last updated: 2025-04-22
-->
