---
title: How to Add External Connectivity to a Hedgehog Fabric VPC
version: Hedgehog v1.0.0
last-verified: 2025-04-25
hedgehog-release: v1.0.0
type: How-to
---

# How to Add External Connectivity to a Hedgehog Fabric VPC

> **Warning:**
> Exposing a VPC to external networks (WAN, internet, or other clouds) increases security risk.
> Validate all policies and review security considerations before proceeding.
> Review [Security Model](../explanation/security-model.md) and [Release Notes](../reference/release-notes.md) for version-specific and security-impacting changes.

## Prerequisites

- Admin access to the Hedgehog Control Node with `kubectl fabric` installed
- Sufficient privileges to manage external resources
- Knowledge of the target VPC and external network details (e.g., VLAN, subnet, gateway)
- Review [Security Model](../explanation/security-model.md) and [VPC Peering](../explanation/vpc-peering.md)
- Confirm device compatibility ([Supported Devices](../reference/supported-devices.md))

---

## Step 1: Define the External Resource

1. Create an external resource in Fabric:
   ```bash
   kubectl fabric external create --name ext-wan --vlan 2000 --subnet 192.0.2.0/24 --gateway 192.0.2.1
   ```
   Sample output:
   ```console
   [INFO] External resource 'ext-wan' created with VLAN 2000, subnet 192.0.2.0/24, gateway 192.0.2.1
   ```
   - Replace VLAN/subnet/gateway with your external network parameters.
2. Inspect the external resource:
   ```bash
   kubectl fabric inspect external --name ext-wan
   ```
   Sample output:
   ```console
   NAME      VLAN   SUBNET         GATEWAY      STATUS
   ext-wan   2000   192.0.2.0/24   192.0.2.1    Ready
   ```

---

## Step 2: Attach VPC to External Resource

1. Attach the VPC to the external connection:
   ```bash
   kubectl fabric vpc attach --vpc-subnet vpc-1/default --connection ext-wan--leaf-01
   ```
   Sample output:
   ```console
   [INFO] VPC 'vpc-1' attached to external connection 'ext-wan--leaf-01'
   ```
   - Use the appropriate connection string for your topology.
2. Validate attachment:
   ```bash
   kubectl fabric inspect vpc --name vpc-1
   kubectl fabric inspect connection --name ext-wan--leaf-01
   ```
   Sample output:
   ```console
   CONNECTION NAME      STATUS      ...
   ext-wan--leaf-01     Ready       ...
   ```

---

## Step 3: Validate Connectivity

1. From a server in the VPC, test external reachability:
   ```bash
   kubectl exec -it server-01 -- ping 192.0.2.1
   kubectl exec -it server-01 -- curl http://example.com
   ```
   Sample output:
   ```console
   PING 192.0.2.1 (192.0.2.1): 56 data bytes
   64 bytes from 192.0.2.1: icmp_seq=0 ttl=64 time=0.23 ms
   ...
   curl: (6) Could not resolve host: example.com  # if DNS/firewall is not configured
   ...
   ```
2. Check routing and interface configuration:
   ```bash
   kubectl exec -it server-01 -- ip route
   kubectl exec -it server-01 -- ip addr
   ```
   Sample output:
   ```console
   default via 192.0.2.1 dev eth0
   ...
   ```

If connectivity fails, see [Troubleshooting External Connectivity](./troubleshooting-fabric.md#external-connectivity).

---

## Rollback: Detach VPC or Delete External Resource

If you need to remove external connectivity:

1. Detach the VPC:
   ```bash
   kubectl fabric vpc detach --vpc-subnet vpc-1/default --connection ext-wan--leaf-01
   ```
   Sample output:
   ```console
   [INFO] VPC 'vpc-1' detached from external connection 'ext-wan--leaf-01'
   ```
2. Delete the external resource:
   ```bash
   kubectl fabric external delete --name ext-wan
   ```
   Sample output:
   ```console
   [INFO] External resource 'ext-wan' deleted
   ```

---

## Troubleshooting

- See [Troubleshooting External Connectivity](./troubleshooting-fabric.md#external-connectivity) for common issues.
- Consult [CLI Reference: external](../reference/fabric-cli.md#external-ext) for command details.
- Review [Security Model](../explanation/security-model.md) for best practices.
- Reference [Release Notes](../reference/release-notes.md) for version-specific caveats.

---

## What’s Next?
- [Troubleshooting External Connectivity](./troubleshooting-fabric.md#external-connectivity)
- [Security Model](../explanation/security-model.md)
- [CLI Reference: external](../reference/fabric-cli.md#external)
- [VPC Peering](../explanation/vpc-peering.md)
- [Release Notes](../reference/release-notes.md)
- [Supported Devices](../reference/supported-devices.md)

---

## How-to Quality Checklist
- [x] All prerequisites (access, privileges, network details, security review) are met
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
