<!-- Diátaxis: Reference -->

# System Requirements

> **Learning Objectives**
> By the end of this reference, you will:
> - Identify hardware and network requirements for Hedgehog Fabric
> - Distinguish between minimal and HA control node setups
> - Reference supported and recommended hardware for production

## Out-of-Band Management Network

To provision and manage switches in the fabric, an out-of-band management network switch must be installed. This network is used exclusively by the control node and fabric switches—no other access is permitted. The management switch is not managed by the fabric. It should have at least a 10GbE port connected to the control node.

## Control Node Requirements

- Only UEFI is supported
- Fast SSDs (preferably NVMe) are mandatory for control nodes
    - DRAM-less NAND SSDs (e.g., Crucial BX500) are not supported
- 10GbE port recommended for management network
- Minimal (non-HA) setup: 1 control node
- (Future) HA setup: at least 3 control nodes
- (Future) Extra nodes may be used for logging, monitoring, alerting, etc.

### Reference Control Node (Hedgehog Internal Testing)

- CPU: AMD EPYC 4344P
- Memory: 32 GiB DDR5 ECC 4800MT/s
- Storage: PCIe Gen 4 NVMe M.2 400GB
- Network: Intel X710-BM1 controller
- Motherboard: H13SAE-MF

### Minimal (Non-HA) Setup — 1 Control Node

- Runs non-HA Kubernetes and Hedgehog Fabric control plane
- Not recommended for more than 10 devices or production deployments

|      | Minimal | Recommended |
| ---- | ------- | ----------- |
| CPU  | 6       | 8           |
| RAM  | 16 GB   | 32 GB       |
| Disk | 150 GB  | 250 GB      |

### (Future) HA Setup — 3+ Control Nodes (per node)

- Each node runs part of the HA Kubernetes and Hedgehog Fabric control plane
- Recommended for deployments with more than 10 devices

|      | Minimal | Recommended |
| ---- | ------- | ----------- |
| CPU  | 6       | 8           |
| RAM  | 16 GB   | 32 GB       |
| Disk | 150 GB  | 250 GB      |

## Device Participating in the Hedgehog Fabric (e.g., switch)

- (Future) Each participating device is part of the Kubernetes cluster, so it runs Kubernetes kubelet
- Additionally, it runs the Hedgehog Fabric Agent that controls devices configuration

Following resources should be available on a device to run in the Hedgehog Fabric (after other software such as SONiC usage):

|      | Minimal | Recommended |
| ---- | ------- | ----------- |
| CPU  | 1       | 2           |
| RAM  | 1 GB    | 1.5 GB      |
| Disk | 5 GB    | 10 GB       |

---

> **See Also:**
> - [Install Hedgehog Fabric](install.md)
> - [Upgrade Instructions](upgrade.md)
> - [Release Notes](../release-notes/index.md)

---

> **Next:** [Install Hedgehog Fabric](install.md)
