<!-- Diátaxis: How-to Guide -->

# Fabric Shrink/Expand

> **Doc Type:** How-to Guide
> **Learning Objectives**
> By the end of this guide, you will:
> - Add new switches to an existing Hedgehog Fabric
> - Remove switches and update fabric topology safely
> - Use YAML and kubectl to manage fabric expansion and contraction
> - Understand prerequisites for redundancy and group membership

This guide explains how to add or remove switches within the fabric using the Hedgehog Fabric API, and how to manage connections between them.

> **Note:** Manipulating API objects assumes that target devices are correctly cabled and connected.

See also: [Hedgehog Concepts](../concepts/overview.md), [User Guide](overview.md), and [Fabric API Reference](../reference/api.md).

## 1. Add a Switch to the Fabric

To add a switch:
1. Ensure the switch is physically cabled and powered on.
2. Create a corresponding `Switch` object. (See [Devices](devices.md) for details.)
3. For a new leaf, increment the largest ASN and IPv4 address by one. For a new spine, use the same ASN as existing spines and increment the IP.
4. If the switch will join an ESLAG or MCLAG group, ensure the group exists and is referenced in the `Switch` object.

**Example: Expanding the Fabric**

Extract the configuration of an existing switch of the same role:

```bash
kubectl get switch/leaf-05 -o yaml > new_switch.yaml
```

Edit the resulting YAML file, incrementing the `asn`, `name`, and `ip` fields as appropriate. Example:

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Switch
metadata:
  name: leaf-06
spec:
  asn: 65105
  boot:
    mac: 0c:20:12:ff:06:00
  mgmt:
    ip: 10.0.0.106/24
  # ... other fields copied from template
```

Apply the new object:
```bash
kubectl apply -f new_switch.yaml
```

> <details>
> <summary>Advanced: Adding to Redundancy Groups</summary>
> - Update the `groups` field in the `Switch` object to add ESLAG/MCLAG membership.
> - Ensure the group exists before referencing it.
> </details>

## 2. Remove a Switch from the Fabric

To remove a switch:
1. Ensure the switch is not part of any required redundancy group, or update group membership accordingly.
2. Delete the `Switch` object:
   ```bash
   kubectl delete switch/leaf-06
   ```
3. Remove or update any related `Connection` or group objects as needed.

> **Tip:** Always check for dependencies (e.g., VPCs, groups) before deleting a switch.

## 3. Replace a Switch in the Fabric

To replace a switch:
1. Edit the existing `Switch` object to update the `MAC` address or `Serial` number of the new hardware.
2. Reinstall the switch, following the boot `ONIE` process used when it was first added to the fabric.

> **Note:** This process does not require removing and re-adding the switch.

---

> **Next:** [Connections](./connections.md)

> **Related Topics:**
> - [Hedgehog Concepts](../concepts/overview.md)
> - [User Guide](overview.md)
> - [Fabric API Reference](../reference/api.md)
> - [Devices](devices.md)

> **Last Updated:** [Insert Date]
