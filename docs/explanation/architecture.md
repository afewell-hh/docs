---
title: Architecture Overview
version: Hedgehog v1.0.0
type: Explanation
---

# Hedgehog Fabric Virtual Networking Architecture

Hedgehog Fabric provides a programmable, cloud-native network fabric for data centers and labs. Its architecture is designed for flexibility, automation, and reliability.

## Core Concepts

- **VPC (Virtual Private Cloud):**
  Logical network segments, providing isolated Layer 2/3 domains for workloads. Each VPC can have its own subnets, VLAN, and DHCP configuration.
- **Switch:**
  A physical or virtual network device managed by the Fabric control plane. Switches connect servers, other switches, and external networks.
- **Connection:**
  Represents a link between endpoints—servers, switches, or external resources. Connections are the building blocks of topology.
- **SwitchGroup:**
  Logical grouping of switches for redundancy or topology management (e.g., MCLAG pairs).
- **External:**
  Represents connectivity to outside networks or services (e.g., WAN, internet, other clouds).
- **Wiring:**
  The logical and physical interconnection map, which can be exported for documentation or automation.

## Control Plane and Data Plane

- **Control Plane:**
  The Hedgehog Fabricator (controller) manages network state, pushes configuration to switches, and exposes both a REST/gRPC API and a CLI (`kubectl fabric`).
- **Data Plane:**
  The actual forwarding of packets, handled by the switches (physical or virtual), based on the configuration received from the control plane.

## How the CLI and API Relate

- The **CLI** (`kubectl fabric`) is a user-friendly wrapper for common operations—creating VPCs, attaching connections, inspecting objects. It is ideal for day-to-day tasks and scripting.
- The **API** provides full programmatic access for automation, integration, and advanced use cases. Some advanced features are only available via the API.
- Both interfaces interact with the same backend state, ensuring consistency.

## Example: Creating a VPC and Attaching a Server

```bash
kubectl fabric vpc create my-vpc --subnet 10.10.0.0/16
kubectl fabric connection create my-vpc --endpoint server01 --port eth0
```

This example demonstrates how to create a new VPC and attach a server using the CLI. For more advanced automation, use the [Fabric API Reference](../reference/fabric-api.md).

## Versioning and Compatibility
- The architecture and supported features may evolve between Hedgehog releases. Always consult the [Release Notes](../reference/release-notes.md) for compatibility and upgrade considerations.
- New architectural features are introduced in a backward-compatible manner whenever possible.

## Cross-References
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
