# Hedgehog Documentation: New vs. Legacy Comparison Tracking

_Last updated: 2025-04-23_

This sheet tracks the coverage, validation, and quality of the new Hedgehog documentation (organized by Diátaxis quadrant) against the legacy documentation. Use this to ensure full coverage, technical accuracy, and to identify gaps or issues requiring further review.

| Quadrant      | Topic / Document                 | New Doc Path                               | Legacy Doc Path                               | Coverage / Enhancement Notes                                                                                                                                             | Validation Status (Legacy/Code/Needs Review) | Issues / Actions |
|--------------|----------------------------------|--------------------------------------------|-----------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------|------------------|
| Reference    | Fabric CLI Reference             | reference/fabric-cli.md                    | reference/cli.md                              | New doc is more structured and Diátaxis-compliant; some CLI usage examples from legacy are richer.                                 | Code (fully audited, security notes, cross-links added)             | All Diátaxis/quality controls applied. More CLI usage examples can be added as future enhancement. |
| Reference    | Fabric API Reference             | reference/fabric-api.md                    | reference/fabric-api.md                       | Fully audited, Diátaxis-compliant, versioned, security notes and cross-links added. Pure reference.                               | Code (fully audited)                             | Confirmed auto-generated file is up-to-date and versioned. |
| Reference    | Fab API Reference (CLI)          | reference/fab-api.md                       | reference/fab-api.md                          | Fully audited, Diátaxis-compliant, clearly labeled as CLI reference. Security notes, cross-links, checklist included.              | Code (fully audited)                             | All Diátaxis/quality controls applied. |
| Reference    | Profiles Reference (Switch Catalog)| reference/profiles.md                     | reference/profiles.md                         | New doc matches and expands legacy; both have detailed tables. Needs periodic code validation for new models.                      | Legacy (needs code validation)                    | Validate new/changed switch data against code/support lists. Ensure versioning/checklist. |
| Reference    | Release Notes                    | reference/release-notes.md                 | reference/releases.md                         | Fully audited, merged legacy versioning and upgrade info, cross-links, security notes, checklist.                                 | Code (fully audited)                             | All Diátaxis/quality controls applied. |
| Reference    | Supported Devices                | reference/supported-devices.md             | install-upgrade/supported-devices.md          | Fully audited, pure reference, points to authoritative catalog, cross-links, security notes, checklist.                           | Code (fully audited)                             | All Diátaxis/quality controls applied. |
| Reference    | Deprecated Stubs                 | reference/releases.md                      | reference/releases.md                         | No changes.                                                                                                                        | Legacy                                       |                  |
| Tutorials    | Getting Started Lab              | tutorial/getting-started-lab.md            | getting-started/download.md                   |                                                                                              |                                              |                  |
| Tutorials    | Demo Lab                         | tutorial/demo-lab.md                       | vlab/demo.md                                 |                                                                                              |                                              |                  |
| Tutorials    | Running VLAB                     | tutorial/running-vlab.md                   | vlab/running.md                               |                                                                                              |                                              |                  |
| How-to Guide | Power-Reset a Switch             | how-to/power-reset-switch.md               |                                               |                                                                                              |                                              |                  |
| How-to Guide | Upgrade Hedgehog Fabric           | how-to/upgrading-fabric.md                 | install-upgrade/upgrade.md                    |                                                                                              |                                              |                  |
| How-to Guide | Add External Connectivity        | how-to/add-external-connectivity.md        |                                               |                                                                                              |                                              |                  |
| How-to Guide | Troubleshooting Fabric            | how-to/troubleshooting-fabric.md           | troubleshooting/overview.md                   |                                                                                              |                                              |                  |
| Explanation  | Architecture Overview            | explanation/architecture.md                | architecture/overview.md                      |                                                                                              |                                              |                  |
| Explanation  | VPC Peering and Isolation        | explanation/vpc-peering.md                 |                                               |                                                                                              |                                              |                  |
| Explanation  | Security Model Overview          | explanation/security-model.md              |                                               |                                                                                              |                                              |                  |

<!-- Add additional rows as new files are mapped or created. -->

## Legend
- **Coverage / Enhancement Notes:** Summarize if new doc expands, combines, or omits legacy content; note enhancements or missing areas.
- **Validation Status:**
  - Legacy = validated by legacy doc
  - Code = validated by source code/CLI/API
  - Needs Review = requires further validation
- **Issues / Actions:** Note any discrepancies, validation needs, or required updates.

## Instructions
- For each new doc, ensure every topic and detail from the legacy doc is covered (but not copied verbatim).
- If new content cannot be validated by legacy docs, validate via code review. If still unvalidated, record details here for further review.
- Update this sheet as the audit progresses.
