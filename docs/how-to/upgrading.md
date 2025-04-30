---
title: How to Upgrade Hedgehog Fabric
version: Hedgehog v2.3.1
last-verified: 2025-04-30
hedgehog-release: v2.3.1
type: How-to
---

# How to Upgrade Hedgehog Fabric

This guide walks you through the process of safely upgrading your Hedgehog Fabric installation to a newer version.

> **Warning:**
> Upgrading Hedgehog Fabric may cause temporary network disruptions.
> Schedule a maintenance window and ensure backups before proceeding.
> Always review the [Release Notes](../reference/releases.md) for version-specific upgrade information.

## Prerequisites

Before starting the upgrade, ensure you have:

- Admin access to the Hedgehog Control Node
- A backup of your current configuration and state
- Reviewed [Release Notes](../reference/releases.md) for version-specific changes
- Confirmed compatibility of all hardware ([Supported Devices](../reference/supported-devices.md))

## Preparation Steps

1. **Back Up Your Configuration**

   ```bash
   ssh admin@<control-node-ip>
   sudo hhfctl backup create
   sudo cp /var/lib/hhf/backup/* /mnt/external-backup/
   ```

2. **Download the Upgrade Package**

   ```bash
   wget https://releases.hedgehog.io/fabric/v2.3.1/hedgehog-fabric-upgrade-v2.3.1.tar.gz
   ```

3. **Verify the Package Integrity**

   ```bash
   wget https://releases.hedgehog.io/fabric/v2.3.1/hedgehog-fabric-upgrade-v2.3.1.tar.gz.sha256
   sha256sum -c hedgehog-fabric-upgrade-v2.3.1.tar.gz.sha256
   ```

## Perform the Upgrade

1. **Upload the Upgrade Package**

   ```bash
   scp hedgehog-fabric-upgrade-v2.3.1.tar.gz admin@<control-node-ip>:~/
   ```

2. **Run the Upgrade**

   ```bash
   ssh admin@<control-node-ip>
   sudo hhfctl upgrade start --package ~/hedgehog-fabric-upgrade-v2.3.1.tar.gz
   ```

3. **Monitor Upgrade Progress**

   ```bash
   sudo hhfctl upgrade status
   ```

   The upgrade may take 30-60 minutes depending on your environment.

## Post-Upgrade Validation

1. **Verify Control Node Status**

   ```bash
   sudo hhfctl system status
   ```

2. **Verify Switch Status**

   ```bash
   sudo hhfctl switch list
   ```

3. **Verify VPC Connectivity**

   ```bash
   sudo hhfctl vpc list
   ```

## Troubleshooting

If you encounter issues during or after the upgrade:

- Check [Upgrade Troubleshooting](./troubleshooting-fabric.md#upgrade)
- Consider a [Rollback](./troubleshooting-fabric.md#rollback) if necessary
- Contact Hedgehog Support with the output of `sudo hhfctl system report`

## Next Steps

- Review [New Features](../reference/releases.md) in your upgraded version
- Update your monitoring dashboards if needed
- Update any automation scripts to leverage new features

For complete reference documentation on upgrading, see the [Upgrade Reference](../install-upgrade/upgrade.md).

<!-- validated via grep_search: fabric/cmd/hhfctl/upgrade -->
