<!-- Diátaxis: Tutorial -->

# Install Hedgehog Fabric

> **Learning Objectives**
> By the end of this tutorial, you will:
> - Prepare all hardware and prerequisites for a Hedgehog Fabric deployment
> - Build and install a control node using `hhfab`
> - Connect management and fabric switches for automatic provisioning
> - Validate a successful installation and know how to proceed

## Prerequisites

- A machine with Internet access to use Fabricator and build the installer (min. 8 GB RAM, 25 GB disk)
- A 16 GB USB flash drive (unless using virtual media)
- A machine to function as the Fabric Control Node ([System Requirements](./requirements.md)), with IPMI access and UEFI boot
- A management switch with at least one 10GbE port
- Sufficient [Supported Switches](./supported-devices.md) for your fabric

!!! tip "Control nodes on virtual machines"
    Running control nodes on virtual machines is possible, although not officially supported. If you use virtual
    machines, make sure to use UEFI boot.

## Overview of Install Process

This tutorial guides you through installing Hedgehog Fabric on bare-metal control node(s) and switches, including preparation and configuration. For VLAB installation, see [VLAB Overview](../vlab/overview.md).

Download and install `hhfab` following instructions from the [Download](../getting-started/download.md) section.

### Installation Steps

1. **Install `hhfab` on your build machine**
    - [Prepare Wiring Diagram](./build-wiring.md)
    - [Select Fabric Configuration](./config.md)
    - Build control node configuration and installer (see below)
2. **Install the Control Node**
    - Insert USB with control-os image into the Fabric Control Node
    - Boot the node from USB to start installation
3. **Prepare the Management Network**
    - Connect management switch to the Fabric control node
    - Connect 1GbE management ports of switches to the management switch
4. **Prepare Supported Switches**
    - Ensure switch serial numbers and/or first management interface MAC addresses are recorded in the wiring diagram
    - Boot switches into ONIE Install Mode for automatic provisioning

---

## Build Control Node Configuration and Installer

Hedgehog provides the `hhfab` CLI to generate wiring diagrams and fabric configuration, validate them, and generate an installation image (.img or .iso) for USB or IPMI virtual media. Start with:

```sh
hhfab init --wiring wiring-lab.yaml
```

This generates the main configuration file, `fab.yaml`, which manages most fabric configuration except wiring. Use `-h` with any `hhfab` command or subcommand for help (e.g., `hhfab init -h`).

### Example: Make a Bootable Image

```sh
hhfab build --output control-os.img fab.yaml
```

Write the resulting image to a USB drive or mount via IPMI virtual media.

---

## Install the Control Node

1. Insert the USB or mount the image on the control node.
2. Boot from the USB/image to start the installer.
3. Follow on-screen prompts to complete installation.
4. **Remove the USB image** after shutdown and before the OS boots.
5. On first boot, the fabric installation will start automatically.
    - If using the insecure `--dev` flag, default passwords are:
        - `core`: `HHFab.Admin!`
        - Switch `admin`: `HHFab.Admin!`
        - Switch `op`: `HHFab.Op!`
    - Monitor with:

    ```sh
    journalctl -f -u fabric-install.service
    ```

---

## Next Steps

- [Upgrade Hedgehog Fabric](./upgrade.md)
- [Configuration](./config.md)
- [Build Wiring](./build-wiring.md)

---

> **See Also:**
> - [System Requirements](./requirements.md)
> - [Supported Devices](./supported-devices.md)
> - [Release Notes](../release-notes/index.md)

---

> **Next:** [Upgrade Hedgehog Fabric](./upgrade.md)
