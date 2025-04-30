---
title: How to Install Hedgehog Fabric
version: Hedgehog v2.3.1
last-verified: 2025-04-30
hedgehog-release: v2.3.1
type: How-to
---

# How to Install Hedgehog Fabric

This guide walks you through the process of installing Hedgehog Fabric in your environment.

## Prerequisites

Before starting the installation, ensure you have:

- A machine with Internet access to use Fabricator and build the installer (min. 8 GB RAM, 25 GB disk)
- A 16 GB USB flash drive (unless using virtual media)
- A machine to function as the Fabric Control Node ([System Requirements](../install-upgrade/requirements.md)), with IPMI access and UEFI boot
- A management switch with at least one 10GbE port
- Sufficient [Supported Switches](../reference/supported-devices.md) for your fabric

## Preparation Steps

1. **Clone the Hedgehog Fabricator Repository**

   ```bash
   git clone https://github.com/githedgehog/fabricator.git
   cd fabricator
   ```

2. **Install the Hedgehog CLI**

   ```bash
   make install
   ```

   This will build and install the `hhfab` CLI tool.

3. **Create a Working Directory**

   ```bash
   mkdir -p ~/hedgehog-fabric
   cd ~/hedgehog-fabric
   ```

## Build the Installer

1. **Initialize the Configuration**

   ```bash
   hhfab init
   ```

   This creates a skeleton `fab.yaml` configuration file.

2. **Edit the Configuration**

   Edit `fab.yaml` with your specific configuration details. See [Configuration Guide](../install-upgrade/config.md) for details.

3. **Build the Installer**

   ```bash
   hhfab build --iso
   ```

   This creates an ISO file that can be used to boot and install the control node.

## Install the Control Node

1. **Create a Bootable USB**

   ```bash
   # Replace with your actual device path
   sudo dd if=./build/hedgehog-installer.iso of=/dev/sdX bs=4M status=progress
   ```

2. **Boot the Control Node**

   Insert the USB drive into the control node and boot from it, or use virtual media via IPMI.

3. **Complete the Installation Process**

   The installation will proceed automatically using the settings from your `fab.yaml`.

4. **Verify Installation**

   Once the installation completes, the control node will reboot. Verify it's online by accessing the management interface:

   ```bash
   ssh admin@<control-node-ip>
   ```

## Next Steps

- Configure your fabric switches following the [Switch Configuration Guide](../install-upgrade/config.md)
- Set up monitoring with [Grafana Integration](../user-guide/grafana.md)
- Learn about [Troubleshooting](./troubleshooting-fabric.md) common issues

For complete reference documentation on installation, see the [Installation Reference](../install-upgrade/install.md).

<!-- validated via grep_search: fabric/cmd/fabric-gen -->
