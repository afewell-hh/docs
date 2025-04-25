---
title: fabric.cli API Reference
version: Hedgehog v1.0.0
type: Reference
---

# Hedgehog Fabric CLI Reference

> **Note:** This page documents the Hedgehog Fabric CLI (`kubectl fabric`). For the REST/gRPC API, see [Fabric API Reference](./fabric-api.md).

**Version:** v0.58.0 (see [release notes](../release-notes/index.md))

---

## Overview

The Hedgehog Fabric CLI is provided as a `kubectl` plugin: `kubectl fabric`.

This tool simplifies the management of Fabric resources in Kubernetes environments.
It wraps `kubectl` and the Kubernetes client, providing user-friendly commands for key Fabric operations.

> **Note:**
> `kubectl fabric` does not expose all API functionality. For advanced operations, use `kubectl` directly or consult the [Fabricator API documentation](https://github.com/githedgehog/fabricator/blob/master/docs/api.md).

---

## Installation & Prerequisites

- `kubectl fabric` is automatically installed on Hedgehog Control Nodes.
- Requires access to a Kubernetes cluster with Hedgehog Fabric deployed.
- See [Getting Started](../tutorial/getting-started.md) for setup instructions.

---

## Usage

```console
kubectl fabric [global options] command [command options]
```

### Global Options

| Option           | Description                                   |
|------------------|-----------------------------------------------|
| `--verbose, -v`  | Verbose output (includes debug; default: true)|
| `--help, -h`     | Show help                                     |
| `--version, -V`  | Print the version                             |

---

## Commands

### VPC (`vpc`)
Manage Virtual Private Clouds (VPCs).

#### Subcommands
- `create`: Create a new VPC
- `attach`: Attach a connection to a VPC
- `peer, peering`: Enable peering between VPCs
- `wipe`: Delete all VPCs, peerings, and attachments

#### Examples
Create a VPC with DHCP:
```console
kubectl fabric vpc create --name vpc-1 --subnet 10.0.1.0/24 --vlan 1001 --dhcp --dhcp-range-start 10.0.1.10
```
Attach a VPC to a server connection:
```console
kubectl fabric vpc attach --vpc-subnet vpc-1/default --connection server-01--mclag--leaf-01--leaf-02
```
Peer two VPCs:
```console
kubectl fabric vpc peer --vpc vpc-1 --vpc vpc-2
```

#### Options (for `create`)
| Option                                 | Description                |
|-----------------------------------------|----------------------------|
| `--name value, -n value`                | VPC name                   |
| `--subnet value`                        | Subnet CIDR                |
| `--vlan value`                          | VLAN ID                    |
| `--dhcp`                                | Enable DHCP                |
| `--dhcp-range-start value, --dhcp-start value` | DHCP range start   |
| `--dhcp-range-end value, --dhcp-end value`     | DHCP range end     |
| `--print, -p`                           | Print object YAML          |
| `--help, -h`                            | Show help                  |

> TODO: Validate all possible options and edge cases for VPC commands.

---

### Switch (`switch`, `sw`)
Manage Fabric switches.

#### Subcommands
- `ip`: Get switch management IP
- `ssh`: SSH into the switch
- `serial`: Serial console for the switch
- `reboot`: Reboot the switch
- `power-reset`: Power reset (unsafe)
- `reinstall`: Reinstall (reboot into ONIE)

#### Example: Get switch IP
```console
kubectl fabric switch ip --name <switch-name>
```

#### Example: SSH into a switch
```console
kubectl fabric switch ssh --name <switch-name>
```

> TODO: Add usage scenarios for `serial`, `reboot`, `power-reset`, `reinstall`.

---

### Connection (`connection`, `conn`)
Manage Fabric connections.

#### Subcommands
- `get`: List connections

#### Example
```console
kubectl fabric connection get management
```

> TODO: Document all available connection types and output formats.

---

### SwitchGroup (`switchgroup`, `sg`)
Manage switch groups.

#### Subcommands
- `create`: Create a SwitchGroup

#### Example
```console
kubectl fabric switchgroup create --name sg-1
```

---

### External (`external`, `ext`)
Manage external connections.

#### Subcommands
- `create`: Create an external resource
- `peer, peering`: Peer external and VPC

#### Example
```console
kubectl fabric external create --name ext-1 --ipv4-namespace ns1
```

---

### Wiring (`wiring`)
Helpers for wiring diagrams.

#### Subcommands
- `export`: Export wiring diagram

#### Example
```console
kubectl fabric wiring export --vpcs --externals
```

---

### Inspect (`inspect`, `i`)
Inspect Fabric API objects and primitives.

#### Subcommands
- `fabric`: Inspect overall fabric
- `switch`: Inspect a switch
- `port, switchport`: Inspect a switch port
- `server`: Inspect a server
- `connection, conn`: Inspect a connection
- `vpc, subnet, vpcsubnet`: Inspect VPC or subnet
- `ip`: Inspect an IP address
- `mac`: Inspect a MAC address
- `access`: Inspect access between endpoints

#### Example: Inspect a switch
```console
kubectl fabric inspect switch --name <switch-name>
```

#### Example: Inspect VPC
```console
kubectl fabric inspect vpc --name <vpc-name>
```

> TODO: Provide example outputs and advanced usage for each inspect subcommand.

---

## Cross-References
- [How to Deploy the CLI](../how-to/deploying-cli.md)
- [Getting Started Tutorial](../tutorial/getting-started.md)
- [Troubleshooting](../how-to/troubleshooting.md)

---

## TODOs & Open Questions
- [ ] Validate all command options and flags for each subcommand.
- [ ] Add real-world usage examples and expected outputs for each command.
- [ ] Confirm edge cases and error handling for destructive operations (e.g., `power-reset`, `wipe`).
- [ ] Document output formats for `inspect` commands.
- [ ] Cross-link to additional how-tos as they are authored.
- [ ] Confirm if command behaviors differ by Hedgehog release.

---

*This page is maintained according to the Diátaxis reference standards. Please flag any inaccuracies or gaps for audit and improvement.*
