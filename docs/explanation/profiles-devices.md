---
title: Profiles & Devices Explained
version: Hedgehog v1.0.0
type: Explanation
---

# Understanding Profiles and Supported Devices in Hedgehog

## What is a Profile?
A **profile** in Hedgehog defines a set of hardware characteristics, supported features, and configuration conventions for a given network switch model. Profiles abstract away vendor-specific details, enabling consistent deployment and automation across heterogeneous hardware.

- **Profile Name:** Used in the switch object's `.spec.profile` field.
- **Other Names:** Alternate vendor/model designations.
- **Supported Roles:** Defines if a switch can act as spine, leaf, or limited-leaf.
- **Silicon:** The ASIC or switching silicon present in the device.
- **Ports:** Physical port types, counts, and breakout capabilities.
- **Features:** Capabilities such as subinterfaces, VXLAN, ACLs, etc.

## Why Profiles Matter
Profiles are essential for:
- Ensuring configuration compatibility across devices.
- Automating fabric deployment and upgrades.
- Enforcing feature parity and role suitability.
- Supporting multi-vendor, open networking environments.

## How Devices are Supported
A device is considered "supported" if:
- It is listed in the [Switch Catalog](../reference/profiles.md) for the current Hedgehog release.
- Its profile is validated against the codebase and continuous integration tests.
- It meets all requirements for the intended role (spine, leaf, limited-leaf).

> **Note:** Some devices may support only a subset of features or roles (e.g., "limited-leaf"). See the [Switch Catalog](../reference/profiles.md) for details.

## Example: Interpreting a Switch Profile
Below is an excerpt from the authoritative [Switch Catalog](../reference/profiles.md):

```markdown
| Switch | Supported Roles | Silicon | Ports |
|--------|-----------------|---------|-------|
| Celestica DS3000 (Seastone2) | spine, leaf | Broadcom TD3-X7 3.2T | 32xQSFP28-100G, 1xSFP28-10G |
```

- **Celestica DS3000 (Seastone2):**
  - Can be used as a spine or leaf in the fabric.
  - Uses Broadcom TD3-X7 silicon.
  - Has 32x100G QSFP28 and 1x10G SFP28 ports.

For a full breakdown of port groups, supported breakout modes, and features, refer to the detailed tables in the [Switch Catalog](../reference/profiles.md).

## Versioning and Compatibility
- Always consult the [Release Notes](../reference/release-notes.md) for device and profile compatibility with your Hedgehog version.
- New hardware support and feature changes are versioned and documented.
- Upgrades may introduce or deprecate profiles—review upgrade guides before deploying new hardware.

## Cross-References
- [Switch Catalog (Reference)](../reference/profiles.md)
- [Supported Devices (Reference)](../reference/supported-devices.md)
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
