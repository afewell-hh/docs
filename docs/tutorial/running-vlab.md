---
title: Running VLAB
version: Hedgehog v1.0.0
type: Tutorial
---

## Overview

This tutorial walks you through the process of running your first Hedgehog Virtual Lab (VLAB) simulation, from initializing the environment to launching and validating the lab. It assumes you have completed the "Getting Started" tutorial and have `hhfab` installed.

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
- This downloads all required artifacts from the OCI registry and prepares the installer.

---

## 5. Start VLAB

Launch the virtual lab:
```bash
hhfab vlab up
```
- Use `--kill-stale` to remove any old VMs:
  ```bash
  hhfab vlab up --kill-stale
  ```
- The command runs in the foreground. Press `Ctrl+C` to stop all VMs.

---

## 6. Validate VLAB is Running

Check the status of your VMs and fabric:
```bash
hhfab vlab status
```
- Look for all VMs in `running` state.
- Review installer logs for errors.

---

## 7. Next Steps

- Try out the [Demo Lab Walkthrough](demo-lab.md)
- Explore [Fabric CLI Reference](../reference/cli.md)
- Review [Troubleshooting](../how-to/troubleshooting.md) if you encounter issues

---

## Gaps
- [ ] Add screenshots and video walkthrough
- [ ] Add validation checklist for successful lab launch
- [ ] Add troubleshooting for common VLAB errors
- [ ] Add advanced topology scenarios

---

<!--
Diátaxis: Tutorial
Version: Hedgehog v1.0.0
Last updated: 2025-04-22
-->
