<!-- Diátaxis: How-to Guide -->

# Connections

> **Learning Objectives**
> By the end of this guide, you will:
> - Define and manage logical/physical connections in the Hedgehog Fabric
> - Use YAML and kubectl to create all supported connection types
> - Understand server, switch, and external connection requirements
> - Validate port naming and redundancy group prerequisites

`Connection` objects represent logical and physical connections between devices in the Fabric (`Switch`, `Server`, and `External` objects) and are required to define all connections in the Wiring Diagram.

All connections reference switch or server ports. Only port names defined by switch profiles can be used in the wiring diagram for switches. NOS (or any other) port names are not supported. Currently, server ports are only validated for uniqueness. See [Switch Profiles and Port Naming](../user-guide/profiles.md) for more details.

There are several types of connections:

## 1. Workload Server Connections

### a. Unbundled
Connect a server to a single switch using a single port.

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Connection
metadata:
  name: server-4--unbundled--s5248-02
spec:
  unbundled:
    link:
      server:
        port: server-4/enp2s1
      switch:
        port: s5248-02/E1/1
```

### b. Bundled (LAG)
Connect a server to a single switch using multiple ports (LAG/802.3ad).

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Connection
metadata:
  name: server-3--bundled--s5248-01
spec:
  bundled:
    links:
      - server:
          port: server-3/enp2s1
        switch:
          port: s5248-01/E1/1
      - server:
          port: server-3/enp2s2
        switch:
          port: s5248-01/E1/2
```

### c. MCLAG (Dual-homing)
Connect a server to a pair of switches using multiple ports. Switches must be in the same `mclag` redundancy group and have a `mclag-domain` connection. Server interfaces must use 802.3ad LACP.

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Connection
metadata:
  name: server-1--mclag--s5248-01--s5248-02
spec:
  mclag:
    links:
      - server:
          port: server-1/enp2s1
        switch:
          port: s5248-01/E1/1
      - server:
          port: server-1/enp2s2
        switch:
          port: s5248-02/E1/1
```

### d. ESLAG (Multi-homing)
Connect a server to 2–4 switches using multiple ports. Switches must be in the same `eslag` redundancy group. Server interfaces must use 802.3ad LACP.

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Connection
metadata:
  name: server-1--eslag--s5248-01--s5248-02
spec:
  eslag:
    links:
      - server:
          port: server-1/enp2s1
        switch:
          port: s5248-01/E1/1
      - server:
          port: server-1/enp2s2
        switch:
          port: s5248-02/E1/1
```

## 2. Switch Connections (Fabric-facing)

Switch connections connect switches to each other and provide "service" connectivity for fabric features.

### a. Fabric
Connect a spine and leaf switch (all wires between them).

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Connection
metadata:
  name: s5232-01--fabric--s5248-01
spec:
  fabric:
    links:
      - switch1:
          port: s5232-01/E1/1
        switch2:
          port: s5248-01/E1/1
      - switch1:
          port: s5232-01/E1/2
        switch2:
          port: s5248-01/E1/2
```

### b. MCLAG Domain Peer Link
Connects a pair of MCLAG switches for peer communication. Both switches must be in the same `mclag` group.

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Connection
metadata:
  name: s5248-01--mclag-domain--s5248-02
spec:
  mclagDomain:
    peerLinks:
      - switch1:
          port: s5248-01/E1/12
        switch2:
          port: s5248-02/E1/12
```

### c. ESLAG Domain Peer Link
Connects switches for ESLAG redundancy groups (2–4 switches).

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Connection
metadata:
  name: s5248-01--eslag-domain--s5248-02--s5248-03
spec:
  eslagDomain:
    peerLinks:
      - switch1:
          port: s5248-01/E1/13
        switch2:
          port: s5248-02/E1/13
      - switch1:
          port: s5248-01/E1/14
        switch2:
          port: s5248-03/E1/14
```

## 3. External Connections

Connect Border Leaf switches to Edge devices for external peering. See [External Peering](external.md) for details.

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Connection
metadata:
  name: borderleaf--external--edge01
spec:
  external:
    link:
      switch:
        port: borderleaf/E1/48
      external:
        name: edge01
```

> <details>
> <summary>Troubleshooting & Advanced Tips</summary>
> - Use `kubectl get connection -o yaml` to review all current connections.
> - Ensure all referenced ports match the switch profile exactly.
> - For MCLAG/ESLAG, verify redundancy groups are pre-defined.
> - Use `kubectl describe connection <name>` for status and events.
> </details>

---

> **Next:** [FAQ](../faq/overview.md)
