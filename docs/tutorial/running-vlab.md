---
title: Running VLAB
version: Hedgehog v1.0.0
type: Tutorial
---

<!-- validated via grep_search: fabricator/cmd/hhfab/vlab.go#L45 -->

## Learning Objectives
- Launch a Hedgehog Virtual Lab environment
- Generate and customize VLAB topologies
- Validate VLAB status and troubleshoot common issues

## Prerequisites
- Complete the "Getting Started" tutorial
- Hedgehog CLI (`hhfab`) v1.0.0 installed and in your PATH
- Docker Desktop (macOS) or Docker Engine with QEMU/KVM enabled (Linux)

## Overview

This tutorial walks you through the process of running your first Hedgehog Virtual Lab (VLAB) simulation, from initializing the environment to launching and validating the lab. It assumes you have completed the "Getting Started" tutorial and have `hhfab` installed.

> **Security Warning:**
> Running VLAB simulations may overwrite existing configuration files and consume significant system resources.
> Only use these instructions in a safe, non-production environment.
> See [VLAB safety guidelines](../known-limitations/known-limitations.md) for more information.

---

## 1. Prerequisites

- Complete the steps in [Getting Started](getting-started.md)
- Ensure your system meets [VLAB requirements](../vlab/overview.md)
- Docker, QEMU/KVM, and ORAS installed (Linux)

---

## 2. Initialize VLAB Configuration

Run the following command to create the initial configuration:

```bash
hhfab init --dev
```
- This generates `fab.yaml` (main config file).
- Adjust credentials, modes, subnets, as needed.

---

## 3. Generate VLAB Topology

Create the default topology:
```bash
hhfab vlab gen
```
Sample output:
```console
[INFO] Generating VLAB topology: spine-leaf (2 spines, 2 MCLAG leaves, 1 non-MCLAG leaf)
[INFO] Output written to vlab.generated.yaml
```
- This creates `vlab.generated.yaml` for a spine-leaf topology (2 spines, 2 MCLAG leaves, 1 non-MCLAG leaf).

**Customize topology:**
- For Collapsed Core:
  1. Edit `fab.yaml`, set `mode: collapsed-core`
  2. Re-run:
     ```bash
     hhfab vlab gen
     ```
- For custom leaf/spine counts:
  ```bash
  hhfab vlab gen --mclag-leafs-count 4 --orphan-leafs-count 2
  ```

---

## 4. Build Installer and Artifacts

Download artifacts and build the installer:
```bash
hhfab build
```
Sample output:
```console
[INFO] Downloading artifacts from OCI registry...
[INFO] Preparing installer...
[INFO] Build complete.
```
- This downloads all required artifacts from the OCI registry and prepares the installer.

---

## 5. Launch VLAB

Bring up the VLAB environment:
```bash
hhfab vlab up
```
Sample output:
```console
[INFO] Launching VLAB...
[INFO] All nodes started successfully.
```

Validate lab status:
```bash
hhfab vlab status
```
Sample output:
```console
[INFO] VLAB status: running
[INFO] Nodes: 5/5 up
```

If you encounter errors, see [Troubleshooting Fabric Deployments](../how-to/troubleshooting-fabric.md).

---

## 6. Validate VLAB is Running

Check the status of your VMs and fabric:
```bash
hhfab vlab status
```
- Look for all VMs in `running` state.
- Review installer logs for errors.

---

## 7. Cleaning Up

To remove your VLAB environment and free resources, run:
```bash
hhfab vlab down
```
Sample output:
```console
[INFO] Shutting down VLAB...
[INFO] All nodes stopped and resources cleaned.
```

---

## What’s Next?
- [Demo Lab Walkthrough](demo-lab.md)
- [Troubleshooting Fabric Deployments](../how-to/troubleshooting-fabric.md)
- [How to Add External Connectivity](../how-to/add-external-connectivity.md)
- [Architecture Overview](../explanation/architecture.md)

---

## Quality Checklist
- [ ] You have completed the prerequisites and system requirements
- [ ] You have initialized the VLAB configuration
- [ ] You have generated and customized the topology as needed
- [ ] You have built all required artifacts
- [ ] You have launched and validated your VLAB environment
- [ ] You have reviewed the security warning
- [ ] You have cleaned up your VLAB environment using `hhfab vlab down`

---

<!--
Diátaxis: Tutorial
Version: Hedgehog v1.0.0
Last updated: 2025-04-30
-->
