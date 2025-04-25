---
title: How to Safely Upgrade Hedgehog Fabric
version: Hedgehog v1.0.0
last-verified: 2025-04-25
hedgehog-release: v1.0.0
type: How-to
---

# How to Safely Upgrade Hedgehog Fabric

> **Warning:**
> Upgrading Hedgehog Fabric may disrupt network operations.
> Schedule a maintenance window and ensure backups before proceeding.
> Always review the [Release Notes](../reference/release-notes.md) for security-impacting changes and version-specific caveats.

## Prerequisites

- Admin access to the Hedgehog Control Node
- Backup of current configuration and state
- Review [Release Notes](../reference/release-notes.md) for version-specific changes
- Confirm compatibility of all hardware and integrations ([Supported Devices](../reference/supported-devices.md))
- Review [Upgrade Troubleshooting](./troubleshooting-fabric.md#upgrade)

---

## Step 1: Validate Current State and Backup

1. Check the current Fabric version:
   ```bash
   kubectl fabric version
   ```
   Sample output:
   ```console
   Hedgehog Fabric version: v1.0.0
   ```
2. Backup configuration and state:
   ```bash
   kubectl get -n fab all -o yaml > fabric-backup.yaml
   # Optionally, backup persistent volumes or etcd
   ```
3. Validate health:
   ```bash
   kubectl get pods -n fab
   kubectl fabric inspect all
   ```
   Sample output:
   ```console
   NAME      STATUS      UPTIME      ...
   leaf1     Ready       12:34:56    ...
   spine1    Ready       12:34:56    ...
   ...
   ```

---

## Step 2: Download and Stage the Upgrade

1. Download the new Fabricator CLI and images:
   ```bash
   curl -fsSL https://i.hhdev.io/hhfab | VERSION=<target-version> bash
   # Or use ORAS to pull images
   oras pull ghcr.io/githedgehog/fabric:<target-version>
   ```
2. Review and update manifests as needed (see [Release Notes](../reference/release-notes.md)).

---

## Step 3: Perform the Upgrade

1. Apply new manifests:
   ```bash
   kubectl apply -f fabric-manifests/<target-version>/
   ```
2. Monitor rollout:
   ```bash
   kubectl get pods -n fab -w
   ```
   Sample output:
   ```console
   NAME      READY   STATUS    RESTARTS   AGE
   leaf1     1/1     Running   0          1m
   spine1    1/1     Running   0          1m
   ...
   ```

If any pods fail to start or remain in a non-`Running` state, see [Troubleshooting Upgrades](./troubleshooting-fabric.md#upgrade).

---

## Step 4: Post-Upgrade Validation

1. Check that all pods are running and healthy:
   ```bash
   kubectl get pods -n fab
   ```
2. Verify network functionality (connectivity, VPCs, peering):
   ```bash
   kubectl fabric vpc get
   kubectl fabric inspect vpc --name <vpc-name>
   ```
   Sample output:
   ```console
   VPC NAME   STATUS    UPTIME      ...
   vpc1       Ready     12:34:56    ...
   vpc2       Ready     12:34:56    ...
   ...
   ```
3. Review logs for errors:
   ```bash
   kubectl logs -n fab <pod-name>
   ```
   Sample output:
   ```console
   ...
   ```

---

## Rollback and Restore (if needed)

If the upgrade fails and you need to restore the previous state:

1. Re-apply your backup manifest:
   ```bash
   kubectl apply -f fabric-backup.yaml
   ```
2. Restore persistent volumes or etcd snapshots as needed.
3. Monitor the cluster until all services are `Ready`.

For more details, see [Rollback Procedures](./troubleshooting-fabric.md#rollback).

---

## Troubleshooting

- See [Troubleshooting Upgrades](./troubleshooting-fabric.md#upgrade) for common upgrade issues.
- Consult [CLI Reference](../reference/fabric-cli.md) for command details.
- Review [Release Notes](../reference/release-notes.md) for known issues and workarounds.
- For conceptual background, see [Architecture Overview](../explanation/architecture.md) and [Security Model](../explanation/security-model.md).

---

## What’s Next?
- [Troubleshooting Upgrades](./troubleshooting-fabric.md#upgrade)
- [Rollback Procedures](./troubleshooting-fabric.md#rollback)
- [Release Notes](../reference/release-notes.md)
- [CLI Reference](../reference/fabric-cli.md)
- [Architecture Overview](../explanation/architecture.md)
- [Security Model](../explanation/security-model.md)

---

## How-to Quality Checklist
- [x] All prerequisites (access, backup, compatibility) are met
- [x] Current version and cluster health validated
- [x] Backup of configuration and state secured
- [x] Upgrade performed and rollout monitored
- [x] Rollback and restore procedures reviewed
- [x] Troubleshooting guides referenced if issues encountered
- [x] Cross-links to reference and explanation docs included
- [x] Semantic line breaks and active voice used
- [x] Instructions are actionable and strictly procedural

If you find any issues or gaps, please update this doc and the [tracking sheet](../_comparison-tracking.md).

---

*This document is maintained according to Diátaxis and Hedgehog quality standards. Please flag any inaccuracies or gaps for audit and improvement.*
