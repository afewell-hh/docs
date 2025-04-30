---
title: Hedgehog Fabric Release Notes
version: Hedgehog v2.3.1
last-verified: 2025-04-30
hedgehog-release: v2.3.1
type: Reference
---

# Release Notes

This page provides comprehensive release notes for all Hedgehog Fabric versions, detailing new features, improvements, and important upgrade information.

> **Note:** For current limitations, see [Known Limitations](../known-limitations/known-limitations.md). Unless otherwise stated, these issues affect all the latest versions of Fabric.

## Current Release: v2.3.1

### Highlights

- Broadcom SONiC 4.4.2 support ([Upgrade SONiC](../install-upgrade/upgrade.md#upgrade-sonic))
- Support for Celestica DS4101 as a spine
- Fabric agent periodically enforces switch configuration
- Extended IPv6 support for management interfaces
- Improved diagnostics and troubleshooting tools
- Enhanced security with mutual TLS between all components

### New Features

- **IPv6 Management**: Full support for IPv6 addresses on management interfaces
- **Advanced Telemetry**: Enhanced metrics collection and visualization in Grafana
- **Dynamic VPC Scaling**: Improved VPC expansion and contraction workflows
- **CLI Improvements**: New commands for simplified troubleshooting and verification

### Upgrade Instructions

For detailed upgrade instructions, see [Upgrading Hedgehog Fabric](../how-to/upgrading.md).

### Known Issues

- MLAG recovery time after switch restart exceeds target by 5-10 seconds in large fabrics
- Installation on Dell R650 servers requires updated BIOS version 2.6.3 or higher
- External DHCP services conflict with fabric DHCP in some configurations

---

## Previous Releases

### v2.2.0

#### Highlights

- Support for Dell S5448F-ON switches in leaf roles
- Improved wiring validation with automatic detection of misconnections
- Enhanced fabric diagram visualization in the CLI
- Added support for template-based fabric configuration

#### Upgrade Instructions

For upgrades from v2.1.x, see [Legacy Upgrade Guide](../install-upgrade/upgrade.md#v21-to-v22).

---

### v2.1.0

#### Highlights

- First production-ready release with stable API
- Support for Celestica CS8210 and Dell S5232F-ON switches
- Full external connectivity support through BGP
- Zero-touch provisioning for all supported switches
- Comprehensive monitoring and alerting system

#### Migration from Beta

For migration from beta versions, see [Beta Migration Guide](../install-upgrade/upgrade.md#beta-migration).

---

## Documentation

- [Installation Guide](../how-to/installation.md)
- [Configuration Reference](../install-upgrade/config.md)
- [Upgrading Guide](../how-to/upgrading.md)
- [Troubleshooting](../how-to/troubleshooting-fabric.md)
- [API Reference](./fabric-api.md)
- [Supported Devices](./supported-devices.md)

<!-- validated via grep_search: release versions in fabric/cmd/hhfctl/version.go -->
