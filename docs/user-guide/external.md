<!-- Diátaxis: How-to Guide -->

# External Peering

> **Learning Objectives**
> By the end of this guide, you will:
> - Understand how to configure external peering for Hedgehog Fabric
> - Connect Border Leaf switches to Edge devices for L3 connectivity
> - Apply BGP and VLAN configuration for route exchange
> - Enforce filtering and policies for VPC traffic to/from Edge

Hedgehog Fabric uses the Border Leaf concept to exchange VPC routes outside the Fabric and provide L3 connectivity. The `External Peering` feature allows you to set up an external peering endpoint and enforce several policies between internal and external endpoints.

> **Note:** Hedgehog Fabric does not operate Edge side devices.

## 1. Overview: Border Leaf and Edge Integration

Traffic exits from the Fabric on Border Leaves connected to Edge devices. Border Leaves:
- Terminate L2VPN connections
- Distinguish VPC L3 routable traffic toward Edge devices
- Land VPC servers

> **Note:** External Peering is only available on switch devices capable of sub-interfaces.

## 2. Prerequisites for Edge Devices

To connect to a Border Leaf, Edge devices must:
- Set up BGP IPv4 to advertise/receive routes from the Fabric
- Connect to a Fabric Border Leaf over VLAN
- Mark egress routes toward the Fabric with BGP Communities
- Filter ingress routes from the Fabric by BGP Communities

All other filtering and processing of L3 routed Fabric traffic (e.g., NAT, PBR) should be done on Edge devices.

## 3. Control Plane: BGP Peering

The Fabric shares VPC routes with Edge devices via BGP. Peering is done over VLAN in IPv4 Unicast AFI/SAFI.

## 4. Data Plane: VLAN Tagging

VPC L3 routable traffic is tagged with VLAN and sent to the Edge device. Further processing (NAT, PBR, etc.) is performed on the Edge.

## 5. Allowing VPC Access to Edge

Each VPC can be allowed to access Edge devices. Filtering can be applied to routes exported to or imported from Edge devices.

## 6. Configure External Peering (API Example)

Create an `External` object to represent Edge device peering. Example:

```yaml
apiVersion: vpc.githedgehog.com/v1beta1
kind: External
metadata:
  name: default--5835
spec:
  ipv4Namespace: # VPC IP Namespace
  inboundCommunity: # BGP Standard Community of routes from Edge devices
  outboundCommunity: # BGP Standard Community required to be assigned on prefixes advertised from Fabric
```

Create a `Connection` object to identify the switch port on Border leaf that is cabled with an Edge device.

```yaml
apiVersion: wiring.githedgehog.com/v1beta1
kind: Connection
metadata:
  name: # specified or generated
spec:
  external:
    link:
      switch:
        port: ds3000/E1/1
```

Create an `ExternalAttachment` object to define BGP Peering and traffic connectivity between a Border leaf and `External`.

```yaml
apiVersion: vpc.githedgehog.com/v1beta1
kind: ExternalAttachment
metadata:
  name: #
spec:
  connection: # Name of the Connection with type external
  external: # Name of the External to pick config
  neighbor:
    asn: # Edge device ASN
    ip: # IP address of Edge device to peer with
  switch:
    ip: # IP address on the Border Leaf to set up BGP peering
    vlan: # VLAN (optional) ID to tag control and data traffic, use 0 for untagged
```

Create an `ExternalPeering` object to allow a specific VPC to have access to Edge devices.

```yaml
apiVersion: vpc.githedgehog.com/v1beta1
kind: ExternalPeering
metadata:
  name: # Name of ExternalPeering
spec:
  permit:
    external:
      name: # External Name
      prefixes: # List of prefixes (routes) to be allowed to pick up from External
      - # IPv4 prefix
    vpc:
      name: # VPC Name
      subnets: # List of VPC subnets name to be allowed to have access to External (Edge)
      - # Name of the subnet within VPC
```

Apply the objects:
```bash
kubectl apply -f external.yaml
kubectl apply -f connection.yaml
kubectl apply -f external-attachment.yaml
kubectl apply -f external-peering.yaml
```

## 7. Filter and Policy Examples

You can specify prefix filters for import/export with the `permit` field. Example: allow only default route prefixes.

```yaml
spec:
  permit:
    external:
      name: ###
      prefixes:
      - prefix: 0.0.0.0/0 # Any route will be allowed including default route
```

> <details>
> <summary>Troubleshooting and Advanced Tips</summary>
> - Ensure Border Leaf switch supports sub-interfaces.
> - Use `kubectl describe external <name>` to check status and events.
> - For advanced filtering, use BGP community lists and prefix lists.
> </details>

---

> **Next:** [Fabric Shrink/Expand](./shrink-expand.md)
