<!-- Diátaxis: Reference -->

# Switch Profiles and Port Naming

> **Learning Objectives**
> By the end of this reference, you will:
> - Understand the structure and purpose of SwitchProfiles in Hedgehog
> - Interpret port naming conventions across supported hardware
> - Identify how to configure port speeds, groups, and breakouts

This reference explains the schema and conventions for switch profiles and port naming in Hedgehog Fabric. Use this as a lookup for supported features, configuration options, and naming standards.

## Switch Profiles

All supported switches have a `SwitchProfile` that defines the switch model, supported features, and available ports with supported configurations such as port group and speeds as well as port breakouts. SwitchProfiles available in-cluster or generated documentation can be found in the [Reference section](../reference/profiles.md).

Each switch used in the wiring diagram should have a `SwitchProfile` referenced in the `spec.profile` of the `Switch` object.

A switch profile defines what features and ports are available on the switch. Based on the ports data in the profile, it's possible to set port speeds (for non-breakout and non-group ports), port group speeds, and port breakout modes in the `Switch` object in the Fabric API.

## Port Naming

Each switch port is named using one of the following formats:

- `M<management-port-number>`
    - `<management-port-number>` is the management port number starting from `1` (usually only one named `1` for most switches)
- `E<asic-or-chassis-number>/<port-number>[/<breakout>][.<subinterface>]`
    - `<asic-or-chassis-number>` is the ASIC or chassis number (usually only one named `1` for most switches)
    - `<port-number>` is the port number on the ASIC or chassis, starting from `1`
    - optional `/<breakout>` is the breakout number for the port, starting from `1`, only for breakout ports and always consecutive numbers independent of the lanes allocation and other implementation details
    - optional `.<subinterface>` is the subinterface number for the port

**Examples:**
- `M1` — management port
- `E1/1` — port `1` on ASIC/chassis `1`
- `E1/55/1` — first breakout port of switch port `55` on ASIC/chassis `1`

## Available Port Types

Each switch profile defines a set of ports available on the switch. Ports may be divided into the following types:

### Directly Configurable Ports
Non-breakout and non-group ports. These have a reference to the port profile with default and available speeds. Configure by setting the speed in the `Switch` object:

```yaml
spec:
  portSpeeds:
    E1/1: 25G
```

### Port Groups
Some switches have port groups (e.g., 4 ports grouped together). Configure the group speed in the `Switch` object:

```yaml
spec:
  portGroups:
    - group: [E1/5, E1/6, E1/7, E1/8]
      speed: 100G
```

### Breakout Ports
For ports supporting breakouts, specify the breakout mode:

```yaml
spec:
  portBreakouts:
    E1/49: [25G, 25G, 25G, 25G]
```

> <details>
> <summary>Advanced: Reference Tables</summary>
> - See [Reference: Switch Profiles](../reference/profiles.md) for a complete list of supported switches, port layouts, and feature tables.
> - For vendor-specific details, consult the hardware appendix.
> </details>

---

> **Next:** [Devices](./devices.md)
