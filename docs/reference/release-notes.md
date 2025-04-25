---
title: Release Notes
version: Hedgehog v1.0.0
type: Reference
---

# Hedgehog Release Notes

> **Note:** This page summarizes Hedgehog Fabric and Fabricator releases, versioning scheme, and upgrade compatibility. For upgrade instructions, see [Upgrading Hedgehog Fabric](../how-to/upgrading.md).

---

## Versioning Scheme

Hedgehog uses a CalVer-style versioning system as of December 2024:

- `YY.MINOR.PATCH` where:
  - `YY`: short calendar year (24, 25, 26)
  - `MINOR`: zero-padded release number in the year (01, 02, 03)
  - `PATCH`: patch number for a release (1, 2, 3)

Example: `25.01` is the first release of 2025; `25.01.1` is its first patch.

API backward compatibility and in-place upgrades are guaranteed starting with the B1 release (Oct 24 2024).
Some new features may require manual intervention or a fresh install; such cases are explicitly noted in the release notes.

---

## Recent Releases

<!-- TODO: Insert table or list of recent releases and major features. -->

---

## Upgrade & Compatibility

- For upgrade instructions, see [Upgrading Hedgehog Fabric](../how-to/upgrading.md).
- For supported devices, see [Supported Devices](./supported-devices.md).
- For troubleshooting, see [Troubleshooting](../how-to/troubleshooting.md).

> **Security Notice:**
> Always review release notes for security-impacting changes before upgrading production environments.

---

## See Also
- [Upgrading Hedgehog Fabric](../how-to/upgrading.md)
- [Supported Devices](./supported-devices.md)
- [Troubleshooting](../how-to/troubleshooting.md)
- [Release Naming & History](./releases.md)

---

### Reference Checklist
- [x] Is this reference strictly descriptive (no how-to or explanation content)?
- [x] Is the versioning scheme clearly described?
- [x] Are all cross-links present and up-to-date?
- [x] Are security notes included where relevant?
- [x] Does this doc use semantic line breaks and consistent terminology?
- [x] Are TODOs and open questions clearly flagged for future work?

If you find any issues or gaps, please update this doc and the [tracking sheet](../_comparison-tracking.md).

---

*This page is maintained according to the Diátaxis reference standards. Please flag any inaccuracies or gaps for audit and improvement.*
