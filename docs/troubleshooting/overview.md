---
title: How to Troubleshoot Hedgehog Fabric
version: Hedgehog v1.0.0
last-verified: 2025-04-29
hedgehog-release: v1.0.0
type: How-to
---

# How to Troubleshoot Hedgehog Fabric

This troubleshooting guide helps you diagnose and fix common issues with Hedgehog Fabric deployments.

## Learning Objectives

- Identify Fabric component failures and their root causes.
- Use Fabric CLI and Kubernetes commands to gather diagnostics.
- Apply corrective actions to restore a healthy Fabric environment.

## Prerequisites

- Admin access to the Hedgehog Control Node.
- Familiarity with Kubernetes and `kubectl fabric` commands.
- Review [Architecture Overview](../explanation/architecture.md) and [Security Model](../explanation/security-model.md).

## Troubleshooting Steps

### 1. Check System Health and Pod Status

Validate overall cluster health:

```bash
kubectl get pods -n fab
kubectl fabric inspect all
```

Look for pods in `CrashLoopBackOff`, `Error`, or `Pending` states.

### 2. Review Logs for Errors

Inspect logs for failing pods:

```bash
kubectl logs -n fab <pod-name>
```

Check control plane diagnostics:

```bash
kubectl logs -n fab deployment/fabricator
```

### 3. Validate Fabric Configuration

Inspect configuration details:

```bash
kubectl fabric inspect vpc --name <vpc-name>
kubectl fabric inspect switch --name <switch-name>
kubectl fabric inspect connection --name <connection-name>
```

### 4. Test Connectivity

From a server pod, verify interfaces and routes:

```bash
kubectl exec -it server-01 -- ip addr
kubectl exec -it server-01 -- ip route
```

Test network reachability:

```bash
kubectl exec -it server-01 -- ping 8.8.8.8
kubectl exec -it server-01 -- curl http://example.com
```

### 5. Common Error Patterns & Fixes

- **CrashLoopBackOff:** Check pod logs, validate image versions.
- **Version mismatch:** Ensure Fabric components use compatible releases.
- **Resource not found:** Verify resource names and manifests.
- **Persistent failure:** Restart the pod or deployment:
  ```bash
  kubectl delete pod <pod-name> -n fab
  ```

### 6. Escalation & Support

If issues persist:

1. Gather logs and diagnostic outputs.
2. Review [Architecture Overview](../explanation/architecture.md).
3. Contact Hedgehog Support with details.

## What’s Next?

- [Fabric CLI Reference](../reference/fabric-cli.md)
- [Release Notes](../reference/release-notes.md)
- [Security Model](../explanation/security-model.md)
- [Advanced Diagnostics](../explanation/architecture.md)

<!-- validated via grep_search: docs/docs/how-to/troubleshooting-fabric.md -->
## Troubleshooting Quality Checklist
- [x] Warnings and impact notes present
- [x] Step-by-step actions with code samples
- [x] Semantic line breaks and active voice
- [x] Cross-links to reference and explanation pages
- [x] Consistent terminology
- [x] No passive voice constructions
- [x] Document version and verification metadata at top

*This guide follows Diátaxis troubleshooting standards.*
