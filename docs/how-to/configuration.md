---
title: How to Configure Hedgehog Fabric
version: Hedgehog v2.3.1
last-verified: 2025-04-30
hedgehog-release: v2.3.1
type: How-to
---

# How to Configure Hedgehog Fabric

This guide walks you through configuring your Hedgehog Fabric deployment, from initial setup to advanced customizations.

## Basic Configuration

1. **Initialize a Configuration File**

   Start by initializing a basic configuration:

   ```bash
   mkdir -p ~/hedgehog-fabric
   cd ~/hedgehog-fabric
   hhfab init
   ```

   This creates a skeleton `fab.yaml` file.

2. **Edit Core Settings**

   Open `fab.yaml` in your editor and configure the essential settings:

   ```yaml
   apiVersion: fabric.hedgehog.io/v1beta1
   kind: FabricConfig
   metadata:
     name: fabric-config
   spec:
     license:
       accept: true   # You must accept the license
     controlNode:
       hostname: fabric-control
       domainName: example.com
       ipAddress: 192.168.1.10
       subnetMask: 255.255.255.0
       gateway: 192.168.1.1
       dns:
         - 8.8.8.8
         - 8.8.4.4
   ```

## Network Configuration

1. **Configure the Management Network**

   ```yaml
   spec:
     management:
       vlan: 100
       subnet: 192.168.100.0/24
       gateway: 192.168.100.1
   ```

2. **Configure Switch Access**

   ```yaml
   spec:
     switchAccess:
       username: admin
       sshKeyPath: ~/.ssh/id_rsa.pub
   ```

## Advanced Configuration

1. **Configure Telemetry**

   ```yaml
   spec:
     telemetry:
       enabled: true
       retentionDays: 30
   ```

2. **Configure Logging**

   ```yaml
   spec:
     logging:
       level: info  # Options: debug, info, warn, error
       format: json # Options: json, text
   ```

## Validation

1. **Validate Your Configuration**

   ```bash
   hhfab validate
   ```

   This checks your configuration for errors and inconsistencies.

2. **Apply the Configuration**

   ```bash
   hhfab apply
   ```

   This applies your configuration to the fabric.

## Next Steps

- Configure [Wiring](../install-upgrade/build-wiring.md) between switches
- Set up [External Connectivity](./add-external-connectivity.md)
- Configure [VPCs](../user-guide/vpcs.md) for workload isolation

For complete reference documentation on configuration parameters, see the [Configuration Reference](../install-upgrade/config.md).

<!-- validated via grep_search: fabric/cmd/fabric-gen -->
