---
title: How to Replace a Device (Switch) in Hedgehog Fabric
version: Hedgehog v1.0.0
last-verified: 2025-04-25
hedgehog-release: v1.0.0
type: How-to
---

# How to Replace a Device (Switch) in Hedgehog Fabric

> **Warning:**
> Device replacement is a disruptive operation that may impact network connectivity and workloads.
> Always schedule maintenance windows and validate the replacement plan with all affected teams.
> Review [Release Notes](../reference/release-notes.md) and [Supported Devices](../reference/supported-devices.md) for model/version compatibility and caveats.

## Prerequisites

- Admin access to the Hedgehog Control Node with `kubectl fabric` installed
- Sufficient privileges to manage devices
- Knowledge of the target device (switch) name and replacement hardware details
- Backup of current Fabric configuration and state ([Upgrading Fabric](./upgrading-fabric.md#step-1-validate-current-state-and-backup))
- Review [Security Model](../explanation/security-model.md) and [Architecture Overview](../explanation/architecture.md)

---

## Step 1: Prepare for Replacement

1. Notify all affected users/teams and schedule a maintenance window.
2. Backup configuration and state:
   ```bash
   kubectl get -n fab all -o yaml > fabric-backup.yaml
   # Optionally backup persistent volumes or etcd
   ```
3. Identify the device to be replaced:
   ```bash
   kubectl fabric switch get
   kubectl fabric inspect switch --name <old-switch-name>
   ```

---

## Step 2: Remove the Old Device

1. Drain workloads or reroute traffic if possible.
2. Remove the device from Fabric:
   ```bash
   kubectl fabric switch delete --name <old-switch-name>
   ```
   Sample output:
   ```console
   [INFO] Switch '<old-switch-name>' deleted
   ```
3. Physically disconnect and remove the old device from the network.

---

## Step 3: Install and Register the Replacement Device

1. Physically install the new device and connect it to the appropriate network ports.
2. Register the new device in Fabric:
   ```bash
   kubectl fabric switch create --name <new-switch-name> --model <model> --mgmt-ip <ip-address> [other-params]
   ```
   Sample output:
   ```console
   [INFO] Switch '<new-switch-name>' created and registered
   ```
   - Use the correct model and parameters for your hardware ([Supported Devices](../reference/supported-devices.md)).
3. Inspect and validate the new device:
   ```bash
   kubectl fabric inspect switch --name <new-switch-name>
   ```
   Sample output:
   ```console
   NAME            STATUS      UPTIME      ...
   <new-switch-name> Ready     00:01:12    ...
   ```

---

## Step 4: Restore Configuration and Validate

1. Reapply any required configuration (VPCs, connections, policies):
   ```bash
   kubectl fabric vpc attach --vpc-subnet <vpc-name>/<subnet> --connection <new-switch-connection>
   # Repeat as needed for all required connections
   ```
2. Validate connectivity and status:
   ```bash
   kubectl fabric inspect switch --name <new-switch-name>
   kubectl fabric inspect vpc --name <vpc-name>
   ```
3. Test network functionality from connected servers:
   ```bash
   kubectl exec -it <server-pod> -- ping <gateway-ip>
   kubectl exec -it <server-pod> -- curl http://example.com
   ```
4. If issues occur, see [Troubleshooting Switch Recovery](./troubleshooting-fabric.md#switch-recovery) and [Troubleshooting External Connectivity](./troubleshooting-fabric.md#external-connectivity).

---

## Rollback (if needed)

If the replacement fails or the new device is not operational:

1. Re-apply the backup manifest:
   ```bash
   kubectl apply -f fabric-backup.yaml
   ```
2. Restore persistent volumes or etcd snapshots as needed.
3. Monitor until all services and devices return to `Ready` state.

---

## Troubleshooting

- See [Troubleshooting Switch Recovery](./troubleshooting-fabric.md#switch-recovery) for issues with device registration or status.
- Consult [Supported Devices](../reference/supported-devices.md) for model-specific requirements.
- Review [Release Notes](../reference/release-notes.md) for known issues and workarounds.
- Reference [CLI Reference: switch](../reference/fabric-cli.md#switch-sw) for command details.

---

## What’s Next?
- [Troubleshooting Switch Recovery](./troubleshooting-fabric.md#switch-recovery)
- [Supported Devices](../reference/supported-devices.md)
- [Release Notes](../reference/release-notes.md)
- [CLI Reference: switch](../reference/fabric-cli.md#switch-sw)
- [Upgrading Fabric](./upgrading-fabric.md)

---

## How-to Quality Checklist
- [x] All prerequisites (access, backup, compatibility, notification) are met
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

*This document is maintained according to Diátaxis and Hedgehog quality standards. Please flag any inaccuracies or gaps for audit and improvement.*
