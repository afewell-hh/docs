---
title: How to Troubleshoot Common Hedgehog Fabric Failures
version: Hedgehog v1.0.0
last-verified: 2025-04-25
hedgehog-release: v1.0.0
type: How-to
---

# How to Troubleshoot Common Hedgehog Fabric Failures

This guide walks you through diagnosing and resolving the most frequent issues encountered with Hedgehog Fabric deployments.

> **Warning:**
> Troubleshooting may involve disruptive actions.
> Always validate the impact before restarting services or applying fixes.
> Review [Release Notes](../reference/release-notes.md) and [Security Model](../explanation/security-model.md) for version-specific and security-impacting changes.

## Prerequisites

- Admin access to the Hedgehog Control Node
- Familiarity with `kubectl fabric` and Kubernetes basics
- Review [Architecture Overview](../explanation/architecture.md) and [Security Model](../explanation/security-model.md)

---

## Step 1: Check System Health and Pod Status

1. Get a quick overview of system health:
   ```bash
   kubectl get pods -n fab
   kubectl fabric inspect all
   ```
   Sample output:
   ```console
   NAME        READY   STATUS             RESTARTS   AGE
   fabricator  1/1     Running            0          1h
   switch-01   1/1     CrashLoopBackOff   5          10m
   ...
   ```
2. Look for pods in `CrashLoopBackOff`, `Error`, or `Pending` state. See troubleshooting tips below.

---

## Step 2: Review Logs for Errors

1. Inspect logs for failing pods:
   ```bash
   kubectl logs -n fab <pod-name>
   ```
   Sample output:
   ```console
   ...
   ERROR: Failed to connect to switch database
   ...
   ```
2. For control plane diagnostics:
   ```bash
   kubectl logs -n fab deployment/fabricator
   ```

---

## Step 3: Validate Fabric Configuration

1. Inspect the configuration of affected objects:
   ```bash
   kubectl fabric inspect vpc --name <vpc-name>
   kubectl fabric inspect switch --name <switch-name>
   kubectl fabric inspect connection --name <connection-name>
   ```
   Sample output:
   ```console
   NAME      STATUS      ...
   vpc-1     Ready       ...
   leaf1     NotReady    ...
   ...
   ```
2. Check for misconfigurations, missing resources, or version mismatches.

---

## Step 4: Test Connectivity

1. From a server pod, check network interfaces and routes:
   ```bash
   kubectl exec -it server-01 -- ip addr
   kubectl exec -it server-01 -- ip route
   ```
   Sample output:
   ```console
   2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> ...
   default via 10.0.0.1 dev eth0
   ...
   ```
2. Test connectivity:
   ```bash
   kubectl exec -it server-01 -- ping 8.8.8.8
   kubectl exec -it server-01 -- curl http://example.com
   ```
   Sample output:
   ```console
   PING 8.8.8.8 (8.8.8.8): 56 data bytes
   64 bytes from 8.8.8.8: icmp_seq=0 ttl=64 time=0.23 ms
   ...
   curl: (6) Could not resolve host: example.com
   ...
   ```

If connectivity fails, check for:
- Incorrect routes or missing interfaces
- Firewall or ACL blocking
- DNS misconfiguration

---

## Step 5: Common Error Patterns & Fixes

- **CrashLoopBackOff:** Pod repeatedly crashes. Check logs for stack traces or configuration errors. Validate image versions and environment variables.
- **Version mismatch:** Ensure all Fabric components are running compatible versions. See [Release Notes](../reference/release-notes.md).
- **Resource not found:** Check for typos in resource names or missing manifests.
- **Persistent failure:** Restart the affected pod or deployment:
  ```bash
  kubectl delete pod <pod-name> -n fab
  ```

---

## Step 6: Escalation & Support

If you cannot resolve the issue:
- Gather logs and diagnostic outputs from above steps
- Review [Architecture Overview](../explanation/architecture.md) and [Security Model](../explanation/security-model.md)
- Contact Hedgehog Support with detailed error messages and steps taken

---

## What’s Next?
- [Release Notes](../reference/release-notes.md)
- [CLI Reference](../reference/fabric-cli.md)
- [Advanced Diagnostics](../explanation/architecture.md)
- [Security Model](../explanation/security-model.md)
- [Contact Support](https://support.githedgehog.com/)

---

## How-to Quality Checklist
- [x] All prerequisites (access, review, familiarity) are met
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
