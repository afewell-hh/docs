<!-- Diátaxis: How-to Guide -->

# VPCs and Namespaces

> **Learning Objectives**
> By the end of this guide, you will:
> - Understand how to define and configure VPCs in Hedgehog
> - Create subnets, assign VLANs, and configure DHCP options
> - Attach VPCs to devices and manage isolation/restriction settings

A Virtual Private Cloud (VPC) in Hedgehog provides an isolated private network with support for multiple subnets, user-defined VLANs, and optional DHCP services. This guide shows how to define, configure, and attach VPCs using YAML manifests.

## 1. Define a VPC

Create a VPC manifest file (e.g., `vpc-1.yaml`):

```yaml
apiVersion: vpc.githedgehog.com/v1beta1
kind: VPC
metadata:
  name: vpc-1
  namespace: default
spec:
  ipv4Namespace: default # Limits which subnets can the VPC use to guarantee non-overlapping IPv4 ranges
  vlanNamespace: default # Limits which Vlan Ids can the VPC use to guarantee non-overlapping VLANs
  defaultIsolated: true # Sets default behavior for the current VPC subnets to be isolated
  defaultRestricted: true # Sets default behavior for the current VPC subnets to be restricted
  subnets:
    default:
      dhcp:
        enable: true
        range:
          start: 10.10.1.10
          end: 10.10.1.99
        options:
          pxeURL: tftp://10.10.10.99/bootfilename
          dnsServers:
            - 1.1.1.1
          timeServers:
            - 1.1.1.1
          interfaceMTU: 1500
      subnet: 10.10.1.0/24
      gateway: 10.10.1.1
      vlan: 1001
      isolated: true
      restricted: true
    thrird-party-dhcp:
      dhcp:
        relay: 10.99.0.100/24
      subnet: "10.10.2.0/24"
      vlan: 1002
    another-subnet:
      subnet: 10.10.100.0/24
      vlan: 1100
```

Apply the VPC manifest:
```bash
kubectl apply -f vpc-1.yaml
```

> <details>
> <summary>Advanced: Customizing DHCP and VLANs</summary>
> - Use `dhcp.options` to specify PXE, DNS, NTP, and MTU settings.
> - Set `relay` under `dhcp` for third-party DHCP servers.
> - Assign unique VLANs per subnet to avoid conflicts.
> </details>

## 2. Attach a VPC Subnet to a Device

Create an attachment manifest (e.g., `attach-server-1.yaml`):

```yaml
apiVersion: fabric.githedgehog.com/v1
kind: VpcAttachment
metadata:
  name: attach-server-1
spec:
  connection: server-1--mclag--s5248-01--s5248-02 # Connection name representing the server port(s)
  subnet: vpc-1/default # VPC subnet name
  nativeVLAN: true # (Optional) if true, the port will be configured as a native VLAN port (untagged)
```

Apply the attachment:
```bash
kubectl apply -f attach-server-1.yaml
```

## 3. Verify VPC and Attachment Status

List VPCs:
```bash
kubectl get vpc
```

Describe a VPC for details:
```bash
kubectl describe vpc vpc-1
```

List attachments:
```bash
kubectl get vpcattachment
```

> **Tip:** Use `kubectl get conn` to see connection status between devices and subnets.

## 4. Isolation and Restriction Settings

- `isolated: true` (at subnet level): Subnet is isolated from other subnets within the same VPC.
- `restricted: true`: Hosts in the subnet are isolated from each other.
- `defaultIsolated`/`defaultRestricted`: Apply these defaults to all subnets unless overridden.

> <details>
> <summary>Troubleshooting</summary>
> - Ensure VLANs and subnets do not overlap between VPCs.
> - Check DHCP server settings if hosts do not receive IPs.
> - Use `kubectl describe` for error details.
> </details>

## VPC Peering

VPC peering enables VPC-to-VPC connectivity. There are two types of VPC peering:

* Local: peering is implemented on the same switches where VPCs are attached
* Remote: peering is implemented on the border/mixed leaves defined by the `SwitchGroup` object

### Local VPC Peering

```yaml
apiVersion: vpc.githedgehog.com/v1beta1
kind: VPCPeering
metadata:
  name: vpc-1--vpc-2
  namespace: default
spec:
  permit: # Defines a pair of VPCs to peer
  - vpc-1: {} # Meaning all subnets of two VPCs will be able to communicate with each other
    vpc-2: {} # See "Subnet filtering" for more advanced configuration
```

### Remote VPC Peering

```yaml
apiVersion: vpc.githedgehog.com/v1beta1
kind: VPCPeering
metadata:
  name: vpc-1--vpc-2
  namespace: default
spec:
  permit:
  - vpc-1: {}
    vpc-2: {}
  remote: border # Indicates a switch group to implement the peering on
```

### Subnet Filtering

It's possible to specify which specific subnets of the peering VPCs could communicate to each other using the `permit` field.

```yaml
apiVersion: vpc.githedgehog.com/v1beta1
kind: VPCPeering
metadata:
  name: vpc-1--vpc-2
  namespace: default
spec:
  permit: # subnet-1 and subnet-2 of vpc-1 could communicate to subnet-3 of vpc-2 as well as subnet-4 of vpc-2 could communicate to subnet-5 and subnet-6 of vpc-2
  - vpc-1:
      subnets: [subnet-1, subnet-2]
    vpc-2:
      subnets: [subnet-3]
  - vpc-1:
      subnets: [subnet-4]
    vpc-2:
      subnets: [subnet-5, subnet-6]
```

## IPv4Namespace

An `IPv4Namespace` defines a set of (non-overlapping) IPv4 address ranges available for use by VPC subnets.
Each VPC belongs to a specific IPv4 namespace. Therefore, its subnet prefixes must be from that IPv4 namespace.

```yaml
apiVersion: vpc.githedgehog.com/v1beta1
kind: IPv4Namespace
metadata:
  name: default
  namespace: default
spec:
  subnets: # List of prefixes that VPCs can pick their subnets from
  - 10.10.0.0/16
```

## VLANNamespace

A `VLANNamespace` defines a set of VLAN ranges available for attaching servers to switches. Each switch can belong to one or more
disjoint VLANNamespaces.

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: VLANNamespace
metadata:
  name: default
  namespace: default
spec:
  ranges: # List of VLAN ranges that VPCs can pick their subnet VLANs from
  - from: 1000
    to: 2999
```

---

> **Next:** [User Guide Overview](./overview.md)
