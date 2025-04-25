---
title: VPC Peering and Isolation
version: Hedgehog v1.0.0
type: Explanation
---

# How VPC Peering and Isolation Work in Hedgehog Fabric

Virtual Private Clouds (VPCs) provide isolated network domains within Hedgehog Fabric. Peering enables controlled connectivity between VPCs while maintaining strong isolation and security boundaries.

## What is VPC Peering?

VPC peering is the process of connecting two or more VPCs so that resources in one VPC can communicate with resources in another, without traversing external networks. Peering is used for multi-tenant applications, shared services, and hybrid cloud scenarios.

- **Direct communication:** Peered VPCs can exchange traffic directly at Layer 3 (IP), without NAT or external routing.
- **No transitive peering:** By default, peering is not transitive—if VPC-A peers with VPC-B, and VPC-B peers with VPC-C, A cannot automatically reach C.

## How Peering is Implemented

- **Fabric Control Plane:** Peering is configured via the CLI or API, which updates routing and access control policies.
- **Overlay Networks:** Peering leverages the Fabric’s overlay (VXLAN or similar) to securely connect VPCs while preserving isolation from other tenants.
- **Access Control:** Security groups and routing policies ensure only explicitly peered VPCs can communicate.

## Isolation Principles

- **Layer 2/3 Segmentation:** Each VPC is assigned a unique subnet and VLAN, ensuring traffic separation at both Layer 2 and Layer 3.
- **Policy Enforcement:** The Fabric controller enforces isolation; only allowed routes and ACLs are programmed for peered VPCs.
- **No Shared Broadcast Domains:** Peered VPCs do not share broadcast or multicast domains, reducing attack surface.

## Example: Peering Two VPCs

```bash
kubectl fabric vpc create --name vpc-a --subnet 10.0.10.0/24 --vlan 1010
kubectl fabric vpc create --name vpc-b --subnet 10.0.20.0/24 --vlan 1020
kubectl fabric vpc peer --from vpc-a --to vpc-b
```

This example demonstrates creating and peering two VPCs using the CLI. Communication is only possible if allowed by policy.

## Versioning and Compatibility
- Peering and isolation features may evolve between Hedgehog releases. Always consult the [Release Notes](../reference/release-notes.md) for compatibility and upgrade considerations.
- Upgrades may introduce new peering modes or policy controls—review upgrade guides before changing peering relationships.

## Cross-References
- [Security Model Overview](./security-model.md)
- [Fabric API Reference](../reference/fabric-api.md)
- [Fabric CLI Reference](../reference/fabric-cli.md)
- [Release Notes](../reference/release-notes.md)
- [Upgrading Hedgehog Fabric](../how-to/upgrading.md)
- [Troubleshooting](../how-to/troubleshooting.md)

---

### Explanation Checklist
- [x] Is this explanation focused on concepts, not procedures or reference data?
- [x] Are all cross-links present and up-to-date?
- [x] Are examples versioned and accurate?
- [x] Is terminology consistent with the reference docs?
- [x] Are open questions and TODOs clearly flagged for future improvement?

If you find any issues or gaps, please update this doc and the [tracking sheet](../_comparison-tracking.md).

---

*This page is maintained according to the Diátaxis explanation standards. Please flag inaccuracies or gaps for audit and improvement.*
