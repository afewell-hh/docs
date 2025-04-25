---
title: Security Model Overview
version: Hedgehog v1.0.0
type: Explanation
---

# Security Model Overview for Hedgehog Fabric

Hedgehog Fabric is designed with security as a core principle, providing robust controls at every layer of the system. This page explains how authentication, authorization, segmentation, and auditing work together to protect your fabric deployments.

## Control Plane Security

- **Authentication:**
  - All API and CLI access requires authentication.
  - Supported methods: certificates, tokens, or integration with external identity providers (e.g., OIDC).
- **Authorization:**
  - Role-Based Access Control (RBAC) governs who can perform which actions.
  - Fine-grained policies restrict sensitive operations (e.g., destructive commands, peering, external access).
- **Audit Logging:**
  - All configuration changes and sensitive operations are logged.
  - Logs are tamper-resistant and can be exported for compliance review.

## Data Plane Security

- **Network Segmentation:**
  - VPCs are isolated by default at both Layer 2 (VLAN) and Layer 3 (subnet).
  - Peering is explicit and policy-controlled (see [VPC Peering](./vpc-peering.md)).
- **Access Control Lists (ACLs):**
  - Fabric controllers program ACLs on switches to enforce tenant and workload boundaries.
  - Only whitelisted traffic is allowed between segments.
- **No Transitive Trust:**
  - Peered VPCs do not automatically transit to third parties.
  - External connectivity must be explicitly configured and approved.

## Best Practices

- **Principle of Least Privilege:**
  - Grant only the minimum required permissions to users and automation.
- **Regular Policy Reviews:**
  - Periodically audit RBAC and peering relationships.
- **Secure API Endpoints:**
  - Always use encrypted channels (TLS) for API and CLI access.
- **Monitor Audit Logs:**
  - Review logs regularly for suspicious activity.

## Example: Secure API Authentication

```bash
# Authenticate to the Hedgehog Fabric API using a certificate
export FABRIC_API_CERT=~/.hh/certs/client.pem
kubectl fabric login --cert $FABRIC_API_CERT --server https://fabricator.example.com
```

This example demonstrates secure, certificate-based authentication to the Fabric API. Always use current, versioned credentials and verify server endpoints.

## Versioning and Compatibility
- Security features and RBAC policies may evolve between Hedgehog releases. Always consult the [Release Notes](../reference/release-notes.md) for the latest security updates and deprecations.
- Review upgrade guides before changing authentication methods or RBAC policies.

## Cross-References
- [VPC Peering and Isolation](./vpc-peering.md)
- [Fabric API Reference](../reference/fabric-api.md)
- [Fabric CLI Reference](../reference/fabric-cli.md)
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
