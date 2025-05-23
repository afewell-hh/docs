# Switches and Servers

All devices in a Hedgehog Fabric are divided into two groups: switches and servers, represented by the corresponding
`Switch` and `Server` objects in the API. These objects are needed to define all of the participants of the Fabric and their
roles in the Wiring Diagram, together with `Connection` objects (see [Connections](./connections.md)).

## Switches

Switches are the main building blocks of the Fabric. They are represented by `Switch` objects in the API. These objects
consist of basic metadata like name, description, role, serial, management port mac, as well as port group speeds, port breakouts, ASN,
IP addresses, and more. Additionally, a `Switch` contains a reference to a `SwitchProfile` object that defines the switch
model and capabilities. More details can be found in the [Switch Profiles and Port Naming](./profiles.md) section.

In order for the fabric to manage a switch the profile needs to include either the `serial` or `mac` need to be defined in the YAML doc.

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Switch
metadata:
  name: s5248-01
  namespace: default
spec:
  boot: # at least one of the serial or mac needs to be defined
    serial: XYZPDQ1234
    mac: 00:11:22:33:44:55 # Usually the first management port MAC address
  profile: dell-s5248f-on # Mandatory reference to the SwitchProfile object defining the switch model and capabilities
  asn: 65101 # ASN of the switch. User provided if exapanding the fabric.
  description: leaf-1
  ip: 172.30.0.8/21 # Switch IP that will be accessible from the Control Node, if expanding the fabric, IP is user-supplied
  portBreakouts: # Configures port breakouts for the switch, see the SwitchProfile for available options
    E1/55: 4x25G
  portGroupSpeeds: # Configures port group speeds for the switch, see the SwitchProfile for available options
    "1": 10G
    "2": 10G
  portSpeeds: # Configures port speeds for the switch, see the SwitchProfile for available options
    E1/1: 25G
  protocolIP: 172.30.11.100/32 # Used as BGP router ID
  role: server-leaf # Role of the switch, one of server-leaf, border-leaf and mixed-leaf
  vlanNamespaces: # Defines which VLANs could be used to attach servers
  - default
  vtepIP: 172.30.12.100/32
  groups: # Defines which groups the switch belongs to, by referring to SwitchGroup objects
  - some-group
  redundancy: # Optional field to define that switch belongs to the redundancy group
    group: eslag-1 # Name of the redundancy group
    type: eslag # Type of the redundancy group, one of mclag or eslag
  enableAllPorts: true # Optional field to enable all ports on the switch by default
```

The `SwitchGroup` is just a marker at that point and doesn't have any configuration options.

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: SwitchGroup
metadata:
  name: border
  namespace: default
spec: {}
```

## Redundancy Groups

Redundancy groups are used to define the redundancy between switches. It's a regular `SwitchGroup` used by multiple
switches and currently it could be MCLAG or ESLAG (EVPN MH / ESI). A switch can only belong to a single redundancy
group.

MCLAG is only supported for pairs of switches and ESLAG is supported for up to 4 switches. Multiple types of redundancy
groups can be used in the fabric simultaneously.

Connections with types `mclag` and `eslag` are used to define the servers connections to switches. They are only
supported if the switch belongs to a redundancy group with the corresponding type.

In order to define a MCLAG or ESLAG redundancy group, you need to create a `SwitchGroup` object and assign it to the
switches using the `redundancy` field.

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

In case of MCLAG it's required to have a special connection with type `mclag-domain` that defines the peer and session
links between switches. For more details, see [Connections](./connections.md).

## Servers

Regular workload server:

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Server
metadata:
  name: server-1
  namespace: default
spec:
  description: MH s5248-01/E1 s5248-02/E1
```
