---
title: Getting Started
version: Hedgehog v1.0.0
type: Tutorial
---

## Overview

This tutorial guides you through your first experience with Hedgehog Fabric, from obtaining access to running your first virtual lab (VLAB) simulation. No prior experience with Hedgehog is assumed.

---

## 1. Requesting Access to Hedgehog

Before you begin, you need access credentials:

1. Go to the [Hedgehog Support Portal](https://support.githedgehog.com/).
2. Submit a request for access to Hedgehog Fabricator (`hhfab`).
3. Wait for your credentials for the [GitHub Package Registry](https://ghcr.io).

---

## 2. Preparing Your System

**Supported platforms:**
- Linux x86/arm64 (Ubuntu 24.04 recommended)
- macOS x86/arm64 (installer only)
- Windows WSL2 (not officially tested)

**Required tools:**
- Docker
- ORAS
- QEMU/KVM (Linux, for VLAB)

**Install Docker (Linux):**
```bash
curl -fsSL https://get.docker.com -o install-docker.sh
sudo sh install-docker.sh
sudo usermod -aG docker $USER
newgrp docker
```

**Install QEMU/KVM (Linux):**
```bash
sudo apt install -y qemu-kvm socat
```

**Install ORAS:**
```bash
curl -fsSL https://i.hhdev.io/oras | bash
```

---

## 3. Downloading and Installing the CLI

**Authenticate with GitHub Package Registry:**
```bash
docker login ghcr.io --username <provided_user_name> --password <provided_token_string>
```

**Download and install `hhfab`:**
```bash
curl -fsSL https://i.hhdev.io/hhfab | bash
```

- For a specific version:
  ```bash
  curl -fsSL https://i.hhdev.io/hhfab | VERSION=24.09 bash
  ```
- To change the install location:
  ```bash
  curl -fsSL https://i.hhdev.io/hhfab | INSTALL_DIR=$HOME/bin bash
  ```

**Verify installation:**
```bash
hhfab --version
```

---

## 4. Initializing and Running Your First VLAB

1. **Initialize configuration:**
   ```bash
   hhfab init --dev
   ```
   This creates a `fab.yaml` config file.

2. **Generate the default VLAB topology:**
   ```bash
   hhfab vlab gen
   ```
   This creates `vlab.generated.yaml` for the default topology.

3. **Customize topology (optional):**
   - Edit `fab.yaml` for Collapsed Core mode:
     ```yaml
     mode: collapsed-core
     ```
   - Or generate with custom flags:
     ```bash
     hhfab vlab gen --mclag-leafs-count 4 --orphan-leafs-count 2
     ```

4. **Start VLAB:**
   Follow instructions in [Running VLAB](../vlab/running.md) for next steps.

---

## 5. Where to Go Next

- [VLAB Overview](../vlab/overview.md): System requirements, concepts, and architecture
- [Deploying Hedgehog CLI](../how-to/deploying-cli.md): Detailed installation and troubleshooting
- [Fabric CLI Reference](../reference/cli.md): CLI command reference

---

## Gaps
- [ ] Add screenshots and video walkthrough
- [ ] Add section for first successful lab validation
- [ ] Add troubleshooting for common setup issues
- [ ] Add platform-specific tips and limitations

---

<!--
Diátaxis: Tutorial
Version: Hedgehog v1.0.0
Last updated: 2025-04-22
-->
