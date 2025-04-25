---
title: How to Deploy Hedgehog Fabric (Control Plane and Data Plane)
version: Hedgehog v1.0.0
last-verified: 2025-04-25
hedgehog-release: v1.0.0
type: How-to
---

# How to Deploy Hedgehog Fabric (Control Plane and Data Plane)

> **Warning:**
> Deploying Hedgehog Fabric will impact your network and may disrupt existing connectivity.
> Always validate your deployment plan, review all prerequisites, and coordinate with affected teams.
> Review [Release Notes](../reference/release-notes.md) and [Security Model](../explanation/security-model.md) for version-specific and security-impacting changes.

## Prerequisites

- Admin access to the deployment environment (bare metal or virtualized)
- Access to the Hedgehog Control Node with `kubectl fabric` and `hhfab` installed ([Deploying CLI](./deploying-cli.md))
- Sufficient privileges to deploy Kubernetes workloads and manage network devices
- Compatible hardware ([Supported Devices](../reference/supported-devices.md))
- Docker and ORAS installed on the control node
- Backup of any existing configuration or state
- Review [Architecture Overview](../explanation/architecture.md) and [Security Model](../explanation/security-model.md)

---

## Step 1: Prepare the Environment

1. Validate hardware and OS compatibility ([Supported Devices](../reference/supported-devices.md)).
2. Ensure Kubernetes is installed and healthy:
   ```bash
   kubectl get nodes
   kubectl get pods -A
   ```
3. Install the Hedgehog CLI (`hhfab`) if not already present:
   ```bash
   curl -fsSL https://i.hhdev.io/hhfab | bash
   hhfab --version
   ```
4. Authenticate with the Hedgehog image registry ([Deploying CLI](./deploying-cli.md#2-authenticating-with-github-package-registry)).

---

## Step 2: Download Fabricator Images and Manifests

1. Download the Fabricator images and manifests for your target release:
   ```bash
   curl -fsSL https://i.hhdev.io/hhfab | VERSION=<target-version> bash
   oras pull ghcr.io/githedgehog/fabric:<target-version>
   ```
2. Review and extract manifests as needed:
   ```bash
   tar -xzvf fabric-manifests-<target-version>.tar.gz
   ```
3. Review the [Release Notes](../reference/release-notes.md) for any special instructions or caveats for your version.

---

## Step 3: Deploy the Control Plane

1. Apply the control plane manifests:
   ```bash
   kubectl apply -f fabric-manifests/<target-version>/control-plane/
   ```
2. Monitor the rollout:
   ```bash
   kubectl get pods -n fab -w
   ```
   Wait for all control plane pods to reach `Running` status.

---

## Step 4: Deploy the Data Plane (Switches/Devices)

1. Register each device (switch) in Fabric:
   ```bash
   kubectl fabric switch create --name <switch-name> --model <model> --mgmt-ip <ip-address> [other-params]
   ```
   - See [Supported Devices](../reference/supported-devices.md) for valid models and requirements.
2. Validate device registration:
   ```bash
   kubectl fabric inspect switch --name <switch-name>
   ```
   Sample output:
   ```console
   NAME            STATUS      UPTIME      ...
   <switch-name>   Ready       00:01:12    ...
   ```

---

## Step 5: Initial Network Validation

1. Create a test VPC and attach it to a switch:
   ```bash
   kubectl fabric vpc create --name test-vpc --subnet 10.10.0.0/24
   kubectl fabric vpc attach --vpc-subnet test-vpc/default --connection <switch-connection>
   ```
2. Deploy a test workload (e.g., server pod) and verify connectivity:
   ```bash
   kubectl run server-01 --image=nginx --restart=Never -n fab
   kubectl exec -it server-01 -n fab -- ping <gateway-ip>
   ```
3. Inspect VPC and connection status:
   ```bash
   kubectl fabric inspect vpc --name test-vpc
   kubectl fabric inspect connection --name <switch-connection>
   ```

---

## Rollback (if needed)

If deployment fails or must be reverted:

1. Delete the deployed resources:
   ```bash
   kubectl delete -f fabric-manifests/<target-version>/control-plane/
   # Manually delete any created switches, VPCs, or workloads
   ```
2. Restore from backup as needed.
3. See [Troubleshooting Fabric Deployments](./troubleshooting-fabric.md) for common issues.

---

## Troubleshooting

- See [Troubleshooting Fabric Deployments](./troubleshooting-fabric.md) for common issues.
- Consult [CLI Reference](../reference/fabric-cli.md) for command details.
- Review [Release Notes](../reference/release-notes.md) for known issues and workarounds.
- Reference [Security Model](../explanation/security-model.md) for best practices.

---

## What’s Next?
- [Upgrading Fabric](./upgrading-fabric.md)
- [Adding External Connectivity](./add-external-connectivity.md)
- [Device Replacement](./device-replacement.md)
- [Reference: Fabric CLI](../reference/fabric-cli.md)
- [Release Notes](../reference/release-notes.md)
- [Security Model](../explanation/security-model.md)

---

## How-to Quality Checklist
- [x] All prerequisites (access, hardware, backup, compatibility, security review) are met
- [x] Step-by-step, active voice used
- [x] Semantic line breaks throughout
- [x] Code samples, versioned and current
- [x] Explicit warnings and validation steps present
- [x] Cross-links to reference, troubleshooting, explanation docs
- [x] Consistent terminology and Diátaxis-compliant structure
- [x] No passive voice constructions
- [x] Instructions are actionable and strictly procedural

If you find any issues or gaps, please update this doc and the [tracking sheet](../_comparison-tracking.md).

---

*This document is maintained according to Diátaxis and Hedgehog quality standards. Please flag any inaccuracies or gaps for audit and improvement.*
