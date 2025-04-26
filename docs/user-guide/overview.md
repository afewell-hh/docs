<!-- Diátaxis: Explanation -->

# Overview

> **Learning Objectives**
> By the end of this explanation, you will:
> - Understand the core architectural concepts of Hedgehog Fabric
> - Recognize the roles of switches, servers, connections, and VPCs
> - See how major features interrelate within the fabric

This chapter provides an architectural overview of Hedgehog Fabric and its main features. Use this as a conceptual map before diving into how-to guides, tutorials, or reference details.

## Hedgehog Fabric Core Concepts

- **Switches and Servers** ([details](devices.md))
  - The foundational elements of the fabric, including supported hardware and virtual platforms, configuration models, and role assignments.
- **Connections** ([details](connections.md))
  - The logical and physical links between servers, switches, and external networks, including workload connections, switch interconnects, and external peering links.
- **VPCs and Namespaces** ([details](vpcs.md))
  - Virtual private cloud configurations, subnet management, isolation/restriction, and peering mechanisms.
- **External Peering** ([details](external.md))
  - Methods for connecting the fabric to outside networks and services, typically via border leaf peering.
- **Fabric Shrink/Expand** ([details](shrink-expand.md))
  - Procedures for adding, removing, or replacing switches and scaling the fabric.
- **Switch Profiles and Port Naming** ([details](profiles.md))
  - Definitions for switch profiles, port naming conventions, and supported hardware/software configurations.
- **Grafana Dashboards** ([details](grafana.md))
  - Monitoring and visualization tools for tracking fabric performance, health, and events.

> **Tip:** Each section above links to a dedicated how-to or reference guide for actionable steps and configuration details.

---

> **Next:** [Connections](./connections.md)
