<!-- Diátaxis: Reference -->

# Switches and Servers

> **Learning Objectives**
> By the end of this reference, you will:
> - Understand the structure and required fields for Switch and Server objects in Hedgehog
> - Recognize how devices are modeled and referenced in the wiring diagram
> - Identify key configuration options, roles, and grouping mechanisms

All devices in a Hedgehog Fabric are divided into two groups: switches and servers, represented by the corresponding `Switch` and `Server` objects in the API. These objects define all participants in the Fabric and their roles in the Wiring Diagram, together with `Connection` objects (see [Connections](./connections.md)).

## Switches

Switches are the main building blocks of the Fabric. They are represented by `Switch` objects in the API, which consist of:
- Metadata: name, description, role, serial, management port MAC
- Configuration: port group speeds, port breakouts, ASN, IP addresses, protocol IP, VTEP IP, VLAN namespaces, groups
- Reference to a `SwitchProfile` object defining the switch model and capabilities ([see profiles](./profiles.md))

At least one of `serial` or `mac` must be defined in the YAML for management. Example:

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Switch
metadata:
  name: s5248-01
  namespace: default
spec:
  boot:
    serial: XYZPDQ1234
    mac: 00:11:22:33:44:55
  profile: dell-s5248f-on
  asn: 65101
  description: leaf-1
  ip: 172.30.0.8/21
  portBreakouts:
    E1/55: 4x25G
  portGroupSpeeds:
    "1": 10G
    "2": 10G
  portSpeeds:
    E1/1: 25G
  protocolIP: 172.30.11.100/32
  role: server-leaf
  vlanNamespaces:
    - default
  vtepIP: 172.30.12.100/32
  groups:
    - some-group
  redundancy:
    group: eslag-1
    type: eslag
  enableAllPorts: true
```

> <details>
> <summary>Advanced: Redundancy and Grouping</summary>
> - `groups` refers to `SwitchGroup` objects for logical grouping.
> - `redundancy` defines membership in MCLAG or ESLAG redundancy groups.
> - `enableAllPorts` enables all ports by default.
> </details>

## Servers

Servers are represented by `Server` objects. These define workload nodes in the Fabric and support various roles and connection types. Example:

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Server
metadata:
  name: server-01
  namespace: default
spec:
  mac: 00:aa:bb:cc:dd:ee
  ip: 172.30.20.101/21
  os: ubuntu-22.04
  groups:
    - workload-group
  description: "Test workload server"
```

> <details>
> <summary>Advanced: Server Groups and Metadata</summary>
> - `groups` can be used for logical grouping and automation.
> - `description` is free-form and aids inventory or automation.
> </details>

## SwitchGroup

The `SwitchGroup` is a logical grouping object for switches. It currently acts as a marker and does not have configuration options, but is referenced in `Switch` objects and for advanced features (e.g., peering, redundancy).

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: SwitchGroup
metadata:
  name: border
  namespace: default
spec: {}
```

## Redundancy Groups

Redundancy groups are used to define the redundancy between switches. It's a regular `SwitchGroup` used by multiple switches and currently it could be MCLAG or ESLAG (EVPN MH / ESI). A switch can only belong to a single redundancy group.

MCLAG is only supported for pairs of switches and ESLAG is supported for up to 4 switches. Multiple types of redundancy groups can be used in the fabric simultaneously.

Connections with types `mclag` and `eslag` are used to define the servers connections to switches. They are only supported if the switch belongs to a redundancy group with the corresponding type.

In order to define a MCLAG or ESLAG redundancy group, you need to create a `SwitchGroup` object and assign it to the switches using the `redundancy` field.

Example of switch configured for ESLAG:

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: SwitchGroup
metadata:
  name: eslag-1
  namespace: default
spec: {}
---
apiVersion: wiring.githedgehog.com/v1beta1
kind: Switch
metadata:
  name: s5248-03
  namespace: default
spec:
  ...
  redundancy:
    group: eslag-1
    type: eslag
  ...
```

And example of switch configured for MCLAG:

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: SwitchGroup
metadata:
  name: mclag-1
  namespace: default
spec: {}
---
apiVersion: wiring.githedgehog.com/v1beta1
kind: Switch
metadata:
  name: s5248-01
  namespace: default
spec:
  ...
  redundancy:
    group: mclag-1
    type: mclag
  ...
```

In case of MCLAG it's required to have a special connection with type `mclag-domain` that defines the peer and session links between switches. For more details, see [Connections](./connections.md).

---

> **Next:** [Connections](./connections.md)
