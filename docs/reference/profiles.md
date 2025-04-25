---
last-verified: 2025-04-25
hedgehog-release: <REPLACE_WITH_VERSION>
audit-checklist:
  - [ ] All profiles match authoritative Go source (pkg/ctrl/switchprofile/)
  - [ ] Table and per-profile sections are complete and accurate
  - [ ] Features and port details are up-to-date
  - [ ] Cross-links to how-to and explanation docs are present
  - [ ] Consistent terminology and active voice
  - [ ] Semantic line breaks
  - [ ] At least one config/code sample per profile
  - [ ] Versioned examples
---

# Switch Catalog

The following is a list of all supported switches with their supported capabilities and configuration. Please, make sure
to use the version of documentation that matches your environment to get an up-to-date list of supported switches, their
features and port naming scheme.


| Switch | Supported Roles | Silicon | Ports |
|--------|-----------------|---------|-------|
| [Celestica DS3000 (Seastone2)](#celestica-ds3000) | **spine**, **leaf** | Broadcom TD3-X7 3.2T | 32xQSFP28-100G, 1xSFP28-10G |
| [Celestica DS4000 (Silverstone2)](#celestica-ds4000) | **spine** | Broadcom TH3 | 32xQSFPDD-400G, 1xSFP28-10G |
| [Celestica DS4101 (Greystone)](#celestica-ds4101) | **spine** | Broadcom TH4G | 32xOSFP-2x400G, 2xSFP28-10G |
| [Celestica DS5000 (Moonstone)](#celestica-ds5000) | **spine**, **limited-leaf** | Broadcom TH5 | 64xOSFP-800G, 2xSFP28-25G |
| [Dell S5232F-ON](#dell-s5232f-on) | **spine**, **leaf** | Broadcom TD3-X7 3.2T | 32xQSFP28-100G, 2xSFP28-10G |
| [Dell S5248F-ON](#dell-s5248f-on) | **spine**, **leaf** | Broadcom TD3-X7 3.2T | 48xSFP28-25G, 8xQSFP28-100G |
| [Dell Z9332F-ON](#dell-z9332f-on) | **spine** | Broadcom TH3 | 32xQSFPDD-400G, 2xSFP28-10G |
| [Edgecore DCS203 (AS7326-56X)](#edgecore-dcs203) | **spine**, **leaf** | Broadcom TD3-X7 2.0T | 48xSFP28-25G, 8xQSFP28-100G, 2xSFP28-10G |
| [Edgecore DCS204 (AS7726-32X)](#edgecore-dcs204) | **spine**, **leaf** | Broadcom TD3-X7 3.2T | 32xQSFP28-100G, 2xSFP28-10G |
| [Edgecore DCS501 (AS7712-32X)](#edgecore-dcs501) | **spine** | Broadcom TH | 32xQSFP28-100G |
| [Edgecore EPS203 (AS4630-54NPE)](#edgecore-eps203) | **limited-leaf** | Broadcom TD3-X3 | 36xRJ45-2.5G, 12xRJ45-10G, 4xSFP28-25G, 2xQSFP28-100G |
| [Supermicro SSE-C4632SB](#supermicro-sse-c4632sb) | **spine**, **leaf** | Broadcom TD3-X7 3.2T | 32xQSFP28-100G, 1xSFP28-10G |

!!! note
    - Switches that support **leaf** role could be used for the collapsed-core topology as well
    - Switches with **limited-leaf** role does not support some leaf features and are not supported in the
      collapsed-core topology


## Celestica DS3000

Profile Name (to use in switch object `.spec.profile`): **celestica-ds3000**

Other names: Celestica Seastone2

**Supported roles:** **spine**, **leaf**, **leaf**

Switch Silicon: **Broadcom TD3-X7 3.2T**

Platform: `x86_64-cel_seastone_2-r0`

Ports Summary: **32xQSFP28-100G, 1xSFP28-10G**

**Supported features:**

- Subinterfaces: true
- VXLAN: true
- ACLs: true

**Available Ports:**

_Label column is a port label on a physical switch._

| Port   | Label | Type         | NOS Name      | Group | Default | Supported                     |
|--------|-------|--------------|---------------|-------|---------|-------------------------------|
| M1     | Mgmt  | Management   | Management0   | -     | -       | -                             |
| E1/1   | 1     | QSFP28-100G  | 1/1 (Ethernet0)    | 1     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/2   | 2     | QSFP28-100G  | 1/2 (Ethernet4)    | 1     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/3   | 3     | QSFP28-100G  | 1/3 (Ethernet8)    | 1     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/4   | 4     | QSFP28-100G  | 1/4 (Ethernet12)   | 1     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/5   | 5     | QSFP28-100G  | 1/5 (Ethernet16)   | 2     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/6   | 6     | QSFP28-100G  | 1/6 (Ethernet20)   | 2     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/7   | 7     | QSFP28-100G  | 1/7 (Ethernet24)   | 2     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/8   | 8     | QSFP28-100G  | 1/8 (Ethernet28)   | 2     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/9   | 9     | QSFP28-100G  | 1/9 (Ethernet32)   | 3     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/10  | 10    | QSFP28-100G  | 1/10 (Ethernet36)  | 3     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/11  | 11    | QSFP28-100G  | 1/11 (Ethernet40)  | 3     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/12  | 12    | QSFP28-100G  | 1/12 (Ethernet44)  | 3     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/13  | 13    | QSFP28-100G  | 1/13 (Ethernet48)  | 4     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/14  | 14    | QSFP28-100G  | 1/14 (Ethernet52)  | 4     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/15  | 15    | QSFP28-100G  | 1/15 (Ethernet56)  | 4     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/16  | 16    | QSFP28-100G  | 1/16 (Ethernet60)  | 4     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/17  | 17    | QSFP28-100G  | 1/17 (Ethernet64)  | 5     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/18  | 18    | QSFP28-100G  | 1/18 (Ethernet68)  | 5     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/19  | 19    | QSFP28-100G  | 1/19 (Ethernet72)  | 5     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/20  | 20    | QSFP28-100G  | 1/20 (Ethernet76)  | 5     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/21  | 21    | QSFP28-100G  | 1/21 (Ethernet80)  | 6     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/22  | 22    | QSFP28-100G  | 1/22 (Ethernet84)  | 6     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/23  | 23    | QSFP28-100G  | 1/23 (Ethernet88)  | 6     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/24  | 24    | QSFP28-100G  | 1/24 (Ethernet92)  | 6     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/25  | 25    | QSFP28-100G  | 1/25 (Ethernet96)  | 7     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/26  | 26    | QSFP28-100G  | 1/26 (Ethernet100) | 7     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/27  | 27    | QSFP28-100G  | 1/27 (Ethernet104) | 7     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/28  | 28    | QSFP28-100G  | 1/28 (Ethernet108) | 7     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/29  | 29    | QSFP28-100G  | 1/29 (Ethernet112) | 8     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/30  | 30    | QSFP28-100G  | 1/30 (Ethernet116) | 8     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/31  | 31    | QSFP28-100G  | 1/31 (Ethernet120) | 8     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/32  | 32    | QSFP28-100G  | 1/32 (Ethernet124) | 8     | 100G    | 100G, 40G, 4x10G, 4x25G       |
| E1/33  | 33    | SFP28-10G    | Ethernet128   | -     | 10G     | 1G, 10G                      |

**Port profile details:**

- **QSFP28-100G**: Default 100G, Supported: 100G, 40G, 4x10G, 4x25G
- **SFP28-10G**: Default 10G, Supported: 1G, 10G

**Example configuration (Hedgehog v2025.04):**

```yaml
apiVersion: fabric.hedgehog.com/v1
kind: Switch
metadata:
  name: ds3000-demo
spec:
  profile: celestica-ds3000
  hostname: ds3000-demo
  mgmt:
    ipv4: 192.0.2.30/24
    gateway: 192.0.2.1
```

---

## Celestica DS4000

Profile Name (to use in switch object `.spec.profile`): **celestica-ds4000**

Other names: Celestica Silverstone2

**Supported roles**: **spine**

Switch Silicon: **Broadcom TH3**

Platform: `x86_64-cel_silverstone-r0`

Ports Summary: **32xQSFPDD-400G, 1xSFP28-10G**

**Supported features:**

- Subinterfaces: false
- VXLAN: false
- ACLs: true
- ACLs: true

**Available Ports:**

Label column is a port label on a physical switch.
| Port   | Label | Type           | NOS Name           | Group | Default | Supported |
|--------|-------|----------------|--------------------|-------|---------|-----------|
| M1     | Mgmt  | Management     | Management0        | -     | -       | -         |
| E1/1  | 1   | Breakout | Ethernet1/1  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/2  | 2   | Breakout | Ethernet1/2  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/3  | 3   | Breakout | Ethernet1/3  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/4  | 4   | Breakout | Ethernet1/4  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/5  | 5   | Breakout | Ethernet1/5  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/6  | 6   | Breakout | Ethernet1/6  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/7  | 7   | Breakout | Ethernet1/7  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/8  | 8   | Breakout | Ethernet1/8  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/9   | 9   | Breakout | Ethernet1/9   | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/10  | 10  | Breakout | Ethernet1/10  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/11  | 11  | Breakout | Ethernet1/11  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/12 | 12  | Breakout | Ethernet1/12  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/13 | 13  | Breakout | Ethernet1/13  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/14 | 14  | Breakout | Ethernet1/14  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/15 | 15  | Breakout | Ethernet1/15  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/16 | 16  | Breakout | Ethernet1/16  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/17 | 17  | Breakout | Ethernet1/17  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/18 | 18  | Breakout | Ethernet1/18  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/19 | 19  | Breakout | Ethernet1/19  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/20 | 20  | Breakout | Ethernet1/20  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/21 | 21  | Breakout | Ethernet1/21  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/22 | 22  | Breakout | Ethernet1/22  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/23 | 23  | Breakout | Ethernet1/23  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/24 | 24  | Breakout | Ethernet1/24  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/25 | 25  | Breakout | Ethernet1/25  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/26 | 26  | Breakout | Ethernet1/26  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/27 | 27  | Breakout | Ethernet1/27  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/28 | 28  | Breakout | Ethernet1/28  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/29 | 29  | Breakout | Ethernet1/29  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/30 | 30  | Breakout | Ethernet1/30  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/31 | 31  | Breakout | Ethernet1/31  | 1x400G | 1x400G, 2x200G, 4x100G |
| E1/32 | 32  | Breakout | Ethernet1/32  | 1x400G | 1x400G, 2x200G, 4x100G |
| S1    | 33  | Direct    | Ethernet1/33 | 10G   | 1G, 10G |
| E1/33 | 33 | Direct |  | 10G | 1G, 10G |

**Port profile details:**
- **QSFPDD-400G**: Default 400G, Supported 100G, 200G, 400G
- **SFP28-10G**: Default 10G, Supported 1G, 10G
- **SFP28-10G**: Default 10G, Supported 1G, 10G

**Example configuration:**
apiVersion: fabric.hedgehog.com/v1
kind: Switch
metadata:
  name: example-ds4000
spec:
  profile: celestica-ds4000
```yaml
apiVersion: fabric.hedgehog.com/v1
kind: Switch
metadata:
  name: example-ds4000
spec:
  profile: celestica-ds4000
  ports:
    - name: E1/1
      speed: 400G
    - name: E1/33
      speed: 10G
```

---

## Celestica DS4101

Profile Name (to use in switch object `.spec.profile`): **celestica-ds4101**

Other names: Celestica Greystone

**Supported roles**: **spine**

Switch Silicon: **Broadcom TH4G**

Ports Summary: **32xOSFP-2x400G, 2xSFP28-10G**

**Supported features:**

- Subinterfaces: false
- VXLAN: false
- ACLs: true
- ACLs: true

**Available Ports:**

Label column is a port label on a physical switch.
| Port   | Label | Type      | NOS Name        | Group | Default | Supported |
|--------|-------|-----------|-----------------|-------|---------|-----------|
| M1     | M1    | Direct    | Management0     | -     | 10G     | 1G, 10G   |
| M2     | M2    | Direct    | Management1     | -     | 10G     | 1G, 10G   |
| E1/1   | 1     | Breakout  | Ethernet1/1     | -     | 2x400G  | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/2   | 2     | Breakout  | Ethernet1/2     | -     | 2x400G  | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/2 | 2 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/3 | 3 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/4 | 4 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/5 | 5 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/6 | 6 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/7 | 7 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/8 | 8 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/9 | 9 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/10 | 10 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/11 | 11 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/12 | 12 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/13 | 13 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/14 | 14 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/15 | 15 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/16 | 16 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/17 | 17 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/18 | 18 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/19 | 19 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/20 | 20 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/21 | 21 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/22 | 22 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/23 | 23 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/24 | 24 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/25 | 25 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/26 | 26 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/27 | 27 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/28 | 28 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/29 | 29 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/30 | 30 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/31 | 31 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/32 | 32 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/33 | 33 | Direct |  | 10G | 1G, 10G |
| E1/34 | 34 | Direct |  | 10G | 1G, 10G |

**Port profile details:**

- **OSFP-2x400G**: Default 2x400G, Supported 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G
- **SFP28-10G**: Default 10G, Supported 1G, 10G

**Available Ports:**

Label column is a port label on a physical switch.

| Port | Label | Type | Group | Default | Supported |
|------|-------|------|-------|---------|-----------|
| M1 | M1 | Direct |  | 10G | 1G, 10G |
| M2 | M2 | Direct |  | 10G | 1G, 10G |
| E1/1 | 1 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/2 | 2 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/3 | 3 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/4 | 4 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/5 | 5 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/6 | 6 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/7 | 7 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/8 | 8 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/9 | 9 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/10 | 10 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/11 | 11 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/12 | 12 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/13 | 13 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/14 | 14 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/15 | 15 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/16 | 16 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/17 | 17 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/18 | 18 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/19 | 19 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/20 | 20 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/21 | 21 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/22 | 22 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/23 | 23 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/24 | 24 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/25 | 25 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/26 | 26 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/27 | 27 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/28 | 28 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/29 | 29 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/30 | 30 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/31 | 31 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/32 | 32 | Breakout |  | 2x400G | 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G |
| E1/33 | 33 | Direct |  | 10G | 1G, 10G |
| E1/34 | 34 | Direct |  | 10G | 1G, 10G |

**Port profile details:**

- **OSFP-2x400G**: Default 2x400G, Supported 1x100G, 1x200G, 1x400G, 2x100G, 2x200G, 2x400G, 2x40G, 4x100G, 4x200G, 4x50G, 8x100G, 8x10G, 8x25G, 8x50G
- **SFP28-10G**: Default 10G, Supported 1G, 10G

**Example configuration:**

```yaml
apiVersion: fabric.hedgehog.com/v1
kind: Switch
metadata:
  name: example-ds4101
spec:
  profile: celestica-ds4101
  ports:
    - name: E1/1
      speed: 2x400G
    - name: E1/33
      speed: 10G
```

---

## Celestica DS5000

Profile Name (to use in switch object `.spec.profile`): **celestica-ds5000**

Other names: Celestica Moonstone

**Supported roles**: **spine**, **limited-leaf**

Switch Silicon: **Broadcom TH5**

Ports Summary: **64xOSFP-800G, 2xSFP28-25G**

**Supported features:**

- Subinterfaces: false
- VXLAN: true
- ACLs: true

**Available Ports:**

Label column is a port label on a physical switch.

| Port | Label | Type | Group | Default | Supported |
|------|-------|------|-------|---------|-----------|
| M1 | M1 | Direct |  | 25G | 1G, 10G, 25G |
| M2 | M2 | Direct |  | 25G | 1G, 10G, 25G |
| E1/1 | 1 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/2 | 2 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/3 | 3 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/4 | 4 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/5 | 5 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/6 | 6 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/7 | 7 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/8 | 8 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/9 | 9 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/10 | 10 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/11 | 11 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/12 | 12 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/13 | 13 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/14 | 14 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/15 | 15 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/16 | 16 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/17 | 17 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/18 | 18 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/19 | 19 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/20 | 20 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/21 | 21 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/22 | 22 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/23 | 23 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/24 | 24 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/25 | 25 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/26 | 26 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/27 | 27 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/28 | 28 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/29 | 29 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/30 | 30 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/31 | 31 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/32 | 32 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/33 | 33 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/34 | 34 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/35 | 35 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/36 | 36 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/37 | 37 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/38 | 38 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/39 | 39 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/40 | 40 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/41 | 41 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/42 | 42 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/43 | 43 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/44 | 44 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/45 | 45 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/46 | 46 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/47 | 47 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/48 | 48 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/49 | 49 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/50 | 50 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/51 | 51 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/52 | 52 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/53 | 53 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/54 | 54 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/55 | 55 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/56 | 56 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/57 | 57 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/58 | 58 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/59 | 59 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/60 | 60 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/61 | 61 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/62 | 62 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/63 | 63 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/64 | 64 | Breakout |  | 1x800G | 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G |
| E1/65 | 65 | Direct |  | 25G | 1G, 10G, 25G |
| E1/66 | 66 | Direct |  | 25G | 1G, 10G, 25G |

**Port profile details:**

- **OSFP-800G**: Default 1x800G, Supported 1x100G, 1x200G, 1x400G, 1x50G, 1x800G, 2x100G, 2x200G, 2x400G, 2x50G, 4x100G, 4x200G, 8x100G
- **SFP28-25G**: Default 25G, Supported 1G, 10G, 25G

**Example configuration:**

```yaml
apiVersion: fabric.hedgehog.com/v1
kind: Switch
metadata:
  name: example-ds5000
spec:
  profile: celestica-ds5000
  ports:
    - name: E1/1
      speed: 1x800G
    - name: E1/65
      speed: 25G
```

---

## Dell S5232F-ON

Profile Name (to use in switch object `.spec.profile`): **dell-s5232f-on**

Other names: Dell S5232F-ON

**Supported roles**: **spine**, **leaf**

Switch Silicon: **Broadcom TD3-X7 3.2T**

Platform: **x86_64-dellemc_s5232f_c3538-r0**

Ports Summary: **32xQSFP28-100G, 2xSFP28-10G**

**Supported features:**

- Subinterfaces: true
- VXLAN: true
- ACLs: true

**Available Ports:**

Label column is a port label on a physical switch.

| Port   | Label | Type        | NOS Name        | ONIE Name | Default  | Supported   |
|--------|-------|-------------|-----------------|-----------|----------|-------------|
| M1     | Mgmt  | Management  | Management0     | eth0      | -        | -           |
| E1/1   | 1     | Breakout    | 1/1 (Ethernet0) |           | 100G     | 100G        |
| E1/2   | 2     | Breakout    | 1/2 (Ethernet4) |           | 100G     | 100G        |
| E1/3   | 3     | Breakout    | 1/3 (Ethernet8) |           | 100G     | 100G        |
| E1/4   | 4     | Breakout    | 1/4 (Ethernet12)|           | 100G     | 100G        |
| E1/5   | 5     | Breakout    | 1/5 (Ethernet16)|           | 100G     | 100G        |
| E1/6   | 6     | Breakout    | 1/6 (Ethernet20)|           | 100G     | 100G        |
| E1/7   | 7     | Breakout    | 1/7 (Ethernet24)|           | 100G     | 100G        |
| E1/8   | 8     | Breakout    | 1/8 (Ethernet28)|           | 100G     | 100G        |
| E1/9   | 9     | Breakout    | 1/9 (Ethernet32)|           | 100G     | 100G        |
| E1/10  | 10    | Breakout    | 1/10 (Ethernet36)|           | 100G     | 100G        |
| E1/11  | 11    | Breakout    | 1/11 (Ethernet40)|           | 100G     | 100G        |
| E1/12  | 12    | Breakout    | 1/12 (Ethernet44)|           | 100G     | 100G        |
| E1/13  | 13    | Breakout    | 1/13 (Ethernet48)|           | 100G     | 100G        |
| E1/14  | 14    | Breakout    | 1/14 (Ethernet52)|           | 100G     | 100G        |
| E1/15  | 15    | Breakout    | 1/15 (Ethernet56)|           | 100G     | 100G        |
| E1/16  | 16    | Breakout    | 1/16 (Ethernet60)|           | 100G     | 100G        |
| E1/17  | 17    | Breakout    | 1/17 (Ethernet64)|           | 100G     | 100G        |
| E1/18  | 18    | Breakout    | 1/18 (Ethernet68)|           | 100G     | 100G        |
| E1/19  | 19    | Breakout    | 1/19 (Ethernet72)|           | 100G     | 100G        |
| E1/20  | 20    | Breakout    | 1/20 (Ethernet76)|           | 100G     | 100G        |
| E1/21  | 21    | Breakout    | 1/21 (Ethernet80)|           | 100G     | 100G        |
| E1/22  | 22    | Breakout    | 1/22 (Ethernet84)|           | 100G     | 100G        |
| E1/23  | 23    | Breakout    | 1/23 (Ethernet88)|           | 100G     | 100G        |
| E1/24  | 24    | Breakout    | 1/24 (Ethernet92)|           | 100G     | 100G        |
| E1/25  | 25    | Breakout    | 1/25 (Ethernet96)|           | 100G     | 100G        |
| E1/26  | 26    | Breakout    | 1/26 (Ethernet100)|           | 100G     | 100G        |
| E1/27  | 27    | Breakout    | 1/27 (Ethernet104)|           | 100G     | 100G        |
| E1/28  | 28    | Breakout    | 1/28 (Ethernet108)|           | 100G     | 100G        |
| E1/29  | 29    | Breakout    | 1/29 (Ethernet112)|           | 100G     | 100G        |
| E1/30  | 30    | Breakout    | 1/30 (Ethernet116)|           | 100G     | 100G        |
| E1/31  | 31    | Breakout    | 1/31 (Ethernet120)|           | 100G     | 100G        |
| E1/32  | 32    | Direct (non-breakout) | Ethernet124 |           | 100G     | 100G        |
| E1/33  | 33    | SFP28-10G   | Ethernet128      |           | 10G      | 1G, 10G     |
| E1/34  | 34    | SFP28-10G   | Ethernet129      |           | 10G      | 1G, 10G     |

**Port profile details:**

- **QSFP28-100G**: Default 100G, Supported 100G
- **SFP28-10G**: Default 10G, Supported 1G, 10G

**Example configuration:**

```yaml
apiVersion: fabric.hedgehog.com/v1
kind: Switch
metadata:
  name: example-s5232f
spec:
  profile: dell-s5232f-on
  ports:
    - name: E1/1
      speed: 100G
    - name: E1/33
      speed: 10G
```

---

## Dell S5248F-ON

Profile Name (to use in switch object `.spec.profile`): **dell-s5248f-on**

Other names: Dell S5248F-ON

**Supported roles**: **spine**, **leaf**

Switch Silicon: **Broadcom TD3-X7 3.2T**

Platform: **x86_64-dellemc_s5248f_c3538-r0**

Ports Summary: **48xSFP28-25G, 8xQSFP28-100G**

**Supported features:**

- Subinterfaces: true
- VXLAN: true
- ACLs: true

**Available Ports:**

Label column is a port label on a physical switch.

| Port   | Label | Type        | NOS Name    | Group | Default | Supported |
|--------|-------|-------------|-------------|-------|---------|-----------|
| M1     | Mgmt  | Management  | Management0 | -     | -       | -         |
| E1/1   | 1     | SFP28-25G   | Ethernet0   | 1     | 25G     | 10G, 25G  |
| E1/2   | 2     | SFP28-25G   | Ethernet1   | 1     | 25G     | 10G, 25G  |
| E1/3   | 3     | SFP28-25G   | Ethernet2   | 1     | 25G     | 10G, 25G  |
| E1/4   | 4     | SFP28-25G   | Ethernet3   | 1     | 25G     | 10G, 25G  |
| E1/5   | 5     | SFP28-25G   | Ethernet4   | 2     | 25G     | 10G, 25G  |
| E1/6   | 6     | SFP28-25G   | Ethernet5   | 2     | 25G     | 10G, 25G  |
| E1/7   | 7     | SFP28-25G   | Ethernet6   | 2     | 25G     | 10G, 25G  |
| E1/8   | 8     | SFP28-25G   | Ethernet7   | 2     | 25G     | 10G, 25G  |
| E1/9   | 9     | SFP28-25G   | Ethernet8   | 3     | 25G     | 10G, 25G  |
| E1/10  | 10    | SFP28-25G   | Ethernet9   | 3     | 25G     | 10G, 25G  |
| E1/11  | 11    | SFP28-25G   | Ethernet10  | 3     | 25G     | 10G, 25G  |
| E1/12  | 12    | SFP28-25G   | Ethernet11  | 3     | 25G     | 10G, 25G  |
| E1/13  | 13    | SFP28-25G   | Ethernet12  | 4     | 25G     | 10G, 25G  |
| E1/14  | 14    | SFP28-25G   | Ethernet13  | 4     | 25G     | 10G, 25G  |
| E1/15  | 15    | SFP28-25G   | Ethernet14  | 4     | 25G     | 10G, 25G  |
| E1/16  | 16    | SFP28-25G   | Ethernet15  | 4     | 25G     | 10G, 25G  |
| E1/17  | 17    | SFP28-25G   | Ethernet16  | 5     | 25G     | 10G, 25G  |
| E1/18  | 18    | SFP28-25G   | Ethernet17  | 5     | 25G     | 10G, 25G  |
| E1/19  | 19    | SFP28-25G   | Ethernet18  | 5     | 25G     | 10G, 25G  |
| E1/20  | 20    | SFP28-25G   | Ethernet19  | 5     | 25G     | 10G, 25G  |
| E1/21  | 21    | SFP28-25G   | Ethernet20  | 6     | 25G     | 10G, 25G  |
| E1/22  | 22    | SFP28-25G   | Ethernet21  | 6     | 25G     | 10G, 25G  |
| E1/23  | 23    | SFP28-25G   | Ethernet22  | 6     | 25G     | 10G, 25G  |
| E1/24  | 24    | SFP28-25G   | Ethernet23  | 6     | 25G     | 10G, 25G  |
| E1/25  | 25    | SFP28-25G   | Ethernet24  | 7     | 25G     | 10G, 25G  |
| E1/26  | 26    | SFP28-25G   | Ethernet25  | 7     | 25G     | 10G, 25G  |
| E1/27  | 27    | SFP28-25G   | Ethernet26  | 7     | 25G     | 10G, 25G  |
| E1/28  | 28    | SFP28-25G   | Ethernet27  | 7     | 25G     | 10G, 25G  |
| E1/29  | 29    | SFP28-25G   | Ethernet28  | 8     | 25G     | 10G, 25G  |
| E1/30  | 30    | SFP28-25G   | Ethernet29  | 8     | 25G     | 10G, 25G  |
| E1/31  | 31    | SFP28-25G   | Ethernet30  | 8     | 25G     | 10G, 25G  |
| E1/32  | 32    | SFP28-25G   | Ethernet31  | 8     | 25G     | 10G, 25G  |
| E1/33  | 33    | SFP28-25G   | Ethernet32  | 9     | 25G     | 10G, 25G  |
| E1/34  | 34    | SFP28-25G   | Ethernet33  | 9     | 25G     | 10G, 25G  |
| E1/35  | 35    | SFP28-25G   | Ethernet34  | 9     | 25G     | 10G, 25G  |
| E1/36  | 36    | SFP28-25G   | Ethernet35  | 9     | 25G     | 10G, 25G  |
| E1/37  | 37    | SFP28-25G   | Ethernet36  | 10    | 25G     | 10G, 25G  |
| E1/38  | 38    | SFP28-25G   | Ethernet37  | 10    | 25G     | 10G, 25G  |
| E1/39  | 39    | SFP28-25G   | Ethernet38  | 10    | 25G     | 10G, 25G  |
| E1/40  | 40    | SFP28-25G   | Ethernet39  | 10    | 25G     | 10G, 25G  |
| E1/41  | 41    | SFP28-25G   | Ethernet40  | 11    | 25G     | 10G, 25G  |
| E1/42  | 42    | SFP28-25G   | Ethernet41  | 11    | 25G     | 10G, 25G  |
| E1/43  | 43    | SFP28-25G   | Ethernet42  | 11    | 25G     | 10G, 25G  |
| E1/44  | 44    | SFP28-25G   | Ethernet43  | 11    | 25G     | 10G, 25G  |
| E1/45  | 45    | SFP28-25G   | Ethernet44  | 12    | 25G     | 10G, 25G  |
| E1/46  | 46    | SFP28-25G   | Ethernet45  | 12    | 25G     | 10G, 25G  |
| E1/47  | 47    | SFP28-25G   | Ethernet46  | 12    | 25G     | 10G, 25G  |
| E1/48  | 48    | SFP28-25G   | Ethernet47  | 12    | 25G     | 10G, 25G  |
| E1/49  | 49    | QSFP28-100G | Ethernet48  | 13    | 100G    | 100G      |
| E1/50  | 50    | QSFP28-100G | Ethernet49  | 13    | 100G    | 100G      |
| E1/51  | 51    | QSFP28-100G | Ethernet50  | 13    | 100G    | 100G      |
| E1/52  | 52    | QSFP28-100G | Ethernet51  | 13    | 100G    | 100G      |
| E1/53  | 53    | QSFP28-100G | Ethernet52  | 14    | 100G    | 100G      |
| E1/54  | 54    | QSFP28-100G | Ethernet53  | 14    | 100G    | 100G      |
| E1/55  | 55    | QSFP28-100G | Ethernet54  | 14    | 100G    | 100G      |
| E1/56  | 56    | QSFP28-100G | Ethernet55  | 14    | 100G    | 100G      |

**Port profile details:**

- **SFP28-25G**: Default 25G, Supported 10G, 25G
- **QSFP28-100G**: Default 100G, Supported 100G

**Example configuration:**

```yaml
apiVersion: fabric.hedgehog.com/v1
kind: Switch
metadata:
  name: example-s5248f
spec:
  profile: dell-s5248f-on
  ports:
    - name: E1/1
      speed: 25G
    - name: E1/49
      speed: 100G
```

---

## Dell Z9332F-ON

Profile Name (to use in switch object `.spec.profile`): **dell-z9332f-on**

**Supported roles**: **spine**

Switch Silicon: **Broadcom TH3**

Platform: `x86_64-cel_silverstone-r0`

Platform: **x86_64-dellemc_z9332f_d1508-r0**

Ports Summary: **32xQSFPDD-400G, 2xSFP28-10G**

**Supported features:**

- Subinterfaces: false
- VXLAN: false
- ACLs: true
- ACLs: true

**Available Ports:**

Label column is a port label on a physical switch.

| Port   | Label | Type         | NOS Name     | Group | Default | Supported         |
|--------|-------|--------------|--------------|-------|---------|-------------------|
| M1     | Mgmt  | Management   | Management0  | -     | -       | -                 |
| E1/1   | 1     | QSFPDD-400G  | Ethernet0    | 1     | 400G    | 100G, 200G, 400G  |
| E1/2   | 2     | QSFPDD-400G  | Ethernet8    | 1     | 400G    | 100G, 200G, 400G  |
| E1/3   | 3     | QSFPDD-400G  | Ethernet16   | 2     | 400G    | 100G, 200G, 400G  |
| E1/4   | 4     | QSFPDD-400G  | Ethernet24   | 2     | 400G    | 100G, 200G, 400G  |
| E1/5   | 5     | QSFPDD-400G  | Ethernet32   | 3     | 400G    | 100G, 200G, 400G  |
| E1/6   | 6     | QSFPDD-400G  | Ethernet40   | 3     | 400G    | 100G, 200G, 400G  |
| E1/7   | 7     | QSFPDD-400G  | Ethernet48   | 4     | 400G    | 100G, 200G, 400G  |
| E1/8   | 8     | QSFPDD-400G  | Ethernet56   | 4     | 400G    | 100G, 200G, 400G  |
| E1/9   | 9     | QSFPDD-400G  | Ethernet64   | 5     | 400G    | 100G, 200G, 400G  |
| E1/10  | 10    | QSFPDD-400G  | Ethernet72   | 5     | 400G    | 100G, 200G, 400G  |
| E1/11  | 11    | QSFPDD-400G  | Ethernet80   | 6     | 400G    | 100G, 200G, 400G  |
| E1/12  | 12    | QSFPDD-400G  | Ethernet88   | 6     | 400G    | 100G, 200G, 400G  |
| E1/13  | 13    | QSFPDD-400G  | Ethernet96   | 7     | 400G    | 100G, 200G, 400G  |
| E1/14  | 14    | QSFPDD-400G  | Ethernet104  | 7     | 400G    | 100G, 200G, 400G  |
| E1/15  | 15    | QSFPDD-400G  | Ethernet112  | 8     | 400G    | 100G, 200G, 400G  |
| E1/16  | 16    | QSFPDD-400G  | Ethernet120  | 8     | 400G    | 100G, 200G, 400G  |
| E1/17  | 17    | QSFPDD-400G  | Ethernet128  | 9     | 400G    | 100G, 200G, 400G  |
| E1/18  | 18    | QSFPDD-400G  | Ethernet136  | 9     | 400G    | 100G, 200G, 400G  |
| E1/19  | 19    | QSFPDD-400G  | Ethernet144  | 10    | 400G    | 100G, 200G, 400G  |
| E1/20  | 20    | QSFPDD-400G  | Ethernet152  | 10    | 400G    | 100G, 200G, 400G  |
| E1/21  | 21    | QSFPDD-400G  | Ethernet160  | 11    | 400G    | 100G, 200G, 400G  |
| E1/22  | 22    | QSFPDD-400G  | Ethernet168  | 11    | 400G    | 100G, 200G, 400G  |
| E1/23  | 23    | QSFPDD-400G  | Ethernet176  | 12    | 400G    | 100G, 200G, 400G  |
| E1/24  | 24    | QSFPDD-400G  | Ethernet184  | 12    | 400G    | 100G, 200G, 400G  |
| E1/25  | 25    | QSFPDD-400G  | Ethernet192  | 13    | 400G    | 100G, 200G, 400G  |
| E1/26  | 26    | QSFPDD-400G  | Ethernet200  | 13    | 400G    | 100G, 200G, 400G  |
| E1/27  | 27    | QSFPDD-400G  | Ethernet208  | 14    | 400G    | 100G, 200G, 400G  |
| E1/28  | 28    | QSFPDD-400G  | Ethernet216  | 14    | 400G    | 100G, 200G, 400G  |
| E1/29  | 29    | QSFPDD-400G  | Ethernet224  | 15    | 400G    | 100G, 200G, 400G  |
| E1/30  | 30    | QSFPDD-400G  | Ethernet232  | 15    | 400G    | 100G, 200G, 400G  |
| E1/31  | 31    | QSFPDD-400G  | Ethernet240  | 16    | 400G    | 100G, 200G, 400G  |
| E1/32  | 32    | QSFPDD-400G  | Ethernet248  | 16    | 400G    | 100G, 200G, 400G  |
| E1/33  | M1    | SFP28-10G    | Ethernet256  | -     | 10G     | 1G, 10G           |
| E1/34  | M2    | SFP28-10G    | Ethernet257  | -     | 10G     | 1G, 10G           |

**Port profile details:**

- **QSFPDD-400G**: Default 400G, Supported 100G, 200G, 400G
- **SFP28-10G**: Default 10G, Supported 1G, 10G

**Example configuration:**

```yaml
apiVersion: fabric.hedgehog.com/v1
kind: Switch
metadata:
  name: example-z9332f
spec:
  profile: dell-z9332f-on
  ports:
    - name: E1/1
      speed: 400G
    - name: E1/33
      speed: 10G
```

---

## Edgecore DCS203

Profile Name (to use in switch object `.spec.profile`): **edgecore-dcs203**

Other names: Edgecore AS7326-56X

**Supported roles**: **spine**, **leaf**

Switch Silicon: **Broadcom TD3-X7 2.0T**

Platform: **x86_64-accton_as7326_56x-r0**

Ports Summary: **48xSFP28-25G, 8xQSFP28-100G, 2xSFP28-10G**

**Supported features:**

- Subinterfaces: true
- VXLAN: true
- ACLs: true

**Available Ports:**

Label column is a port label on a physical switch.

| Port   | Label | Type         | NOS Name     | Group | Default | Supported      |
|--------|-------|--------------|--------------|-------|---------|----------------|
| M1     | Mgmt  | Management   | Management0  | -     | -       | -              |
| E1/1   | 1     | SFP28-25G    | Ethernet0    | 1     | 25G     | 10G, 25G       |
| E1/2   | 2     | SFP28-25G    | Ethernet1    | 1     | 25G     | 10G, 25G       |
| E1/3   | 3     | SFP28-25G    | Ethernet2    | 1     | 25G     | 10G, 25G       |
| E1/4   | 4     | SFP28-25G    | Ethernet3    | 1     | 25G     | 10G, 25G       |
| E1/5   | 5     | SFP28-25G    | Ethernet4    | 1     | 25G     | 10G, 25G       |
| E1/6   | 6     | SFP28-25G    | Ethernet5    | 1     | 25G     | 10G, 25G       |
| E1/7   | 7     | SFP28-25G    | Ethernet6    | 1     | 25G     | 10G, 25G       |
| E1/8   | 8     | SFP28-25G    | Ethernet7    | 1     | 25G     | 10G, 25G       |
| E1/9   | 9     | SFP28-25G    | Ethernet8    | 1     | 25G     | 10G, 25G       |
| E1/10  | 10    | SFP28-25G    | Ethernet9    | 1     | 25G     | 10G, 25G       |
| E1/11  | 11    | SFP28-25G    | Ethernet10   | 1     | 25G     | 10G, 25G       |
| E1/12  | 12    | SFP28-25G    | Ethernet11   | 1     | 25G     | 10G, 25G       |
| E1/13  | 13    | SFP28-25G    | Ethernet12   | 2     | 25G     | 10G, 25G       |
| E1/14  | 14    | SFP28-25G    | Ethernet13   | 2     | 25G     | 10G, 25G       |
| E1/15  | 15    | SFP28-25G    | Ethernet14   | 2     | 25G     | 10G, 25G       |
| E1/16  | 16    | SFP28-25G    | Ethernet15   | 2     | 25G     | 10G, 25G       |
| E1/17  | 17    | SFP28-25G    | Ethernet16   | 2     | 25G     | 10G, 25G       |
| E1/18  | 18    | SFP28-25G    | Ethernet17   | 2     | 25G     | 10G, 25G       |
| E1/19  | 19    | SFP28-25G    | Ethernet18   | 2     | 25G     | 10G, 25G       |
| E1/20  | 20    | SFP28-25G    | Ethernet19   | 2     | 25G     | 10G, 25G       |
| E1/21  | 21    | SFP28-25G    | Ethernet20   | 2     | 25G     | 10G, 25G       |
| E1/22  | 22    | SFP28-25G    | Ethernet21   | 2     | 25G     | 10G, 25G       |
| E1/23  | 23    | SFP28-25G    | Ethernet22   | 2     | 25G     | 10G, 25G       |
| E1/24  | 24    | SFP28-25G    | Ethernet23   | 2     | 25G     | 10G, 25G       |
| E1/25  | 25    | SFP28-25G    | Ethernet24   | 3     | 25G     | 10G, 25G       |
| E1/26  | 26    | SFP28-25G    | Ethernet25   | 3     | 25G     | 10G, 25G       |
| E1/27  | 27    | SFP28-25G    | Ethernet26   | 3     | 25G     | 10G, 25G       |
| E1/28  | 28    | SFP28-25G    | Ethernet27   | 3     | 25G     | 10G, 25G       |
| E1/29  | 29    | SFP28-25G    | Ethernet28   | 3     | 25G     | 10G, 25G       |
| E1/30  | 30    | SFP28-25G    | Ethernet29   | 3     | 25G     | 10G, 25G       |
| E1/31  | 31    | SFP28-25G    | Ethernet30   | 3     | 25G     | 10G, 25G       |
| E1/32  | 32    | SFP28-25G    | Ethernet31   | 3     | 25G     | 10G, 25G       |
| E1/33  | 33    | SFP28-25G    | Ethernet32   | 3     | 25G     | 10G, 25G       |
| E1/34  | 34    | SFP28-25G    | Ethernet33   | 3     | 25G     | 10G, 25G       |
| E1/35  | 35    | SFP28-25G    | Ethernet34   | 3     | 25G     | 10G, 25G       |
| E1/36  | 36    | SFP28-25G    | Ethernet35   | 3     | 25G     | 10G, 25G       |
| E1/37  | 37    | SFP28-25G    | Ethernet36   | 4     | 25G     | 10G, 25G       |
| E1/38  | 38    | SFP28-25G    | Ethernet37   | 4     | 25G     | 10G, 25G       |
| E1/39  | 39    | SFP28-25G    | Ethernet38   | 4     | 25G     | 10G, 25G       |
| E1/40  | 40    | SFP28-25G    | Ethernet39   | 4     | 25G     | 10G, 25G       |
| E1/41  | 41    | SFP28-25G    | Ethernet40   | 4     | 25G     | 10G, 25G       |
| E1/42  | 42    | SFP28-25G    | Ethernet41   | 4     | 25G     | 10G, 25G       |
| E1/43  | 43    | SFP28-25G    | Ethernet42   | 4     | 25G     | 10G, 25G       |
| E1/44  | 44    | SFP28-25G    | Ethernet43   | 4     | 25G     | 10G, 25G       |
| E1/45  | 45    | SFP28-25G    | Ethernet44   | 4     | 25G     | 10G, 25G       |
| E1/46  | 46    | SFP28-25G    | Ethernet45   | 4     | 25G     | 10G, 25G       |
| E1/47  | 47    | SFP28-25G    | Ethernet46   | 4     | 25G     | 10G, 25G       |
| E1/48  | 48    | SFP28-25G    | Ethernet47   | 4     | 25G     | 10G, 25G       |
| E1/49  | 49    | QSFP28-100G  | Ethernet48  | 13    | 100G    | 100G           |
| E1/50  | 50    | QSFP28-100G  | Ethernet49  | 13    | 100G    | 100G           |
| E1/51  | 51    | QSFP28-100G  | Ethernet50  | 13    | 100G    | 100G           |
| E1/52  | 52    | QSFP28-100G  | Ethernet51  | 13    | 100G    | 100G           |
| E1/53  | 53    | QSFP28-100G  | Ethernet52  | 14    | 100G    | 100G           |
| E1/54  | 54    | QSFP28-100G  | Ethernet53  | 14    | 100G    | 100G           |
| E1/55  | 55    | QSFP28-100G  | Ethernet54  | 14    | 100G    | 100G           |
| E1/56  | 56    | QSFP28-100G  | Ethernet55  | 14    | 100G    | 100G           |
| E1/57  | 57    | SFP28-10G    | Ethernet56   | -     | 10G     | 1G, 10G         |
| E1/58  | 58    | SFP28-10G    | Ethernet57   | -     | 10G     | 1G, 10G         |

**Port profile details:**

- **SFP28-25G**: Default 25G, Supported 10G, 25G
- **QSFP28-100G**: Default 100G, Supported 100G
- **SFP28-10G**: Default 10G, Supported 1G, 10G

**Example configuration:**

```yaml
apiVersion: fabric.hedgehog.com/v1
kind: Switch
metadata:
  name: example-dcs203
spec:
  profile: edgecore-dcs203
  ports:
    - name: E1/1
      speed: 25G
    - name: E1/49
      speed: 100G
    - name: E1/57
      speed: 10G
```

---

## Edgecore DCS204

Profile Name (to use in switch object `.spec.profile`): **edgecore-dcs204**

Other names: Edgecore AS7726-32X

**Supported roles**: **spine**, **leaf**

Switch Silicon: **Broadcom TD3-X7 3.2T**

Ports Summary: **32xQSFP28-100G, 2xSFP28-10G**

**Supported features:**

- Subinterfaces: true
- VXLAN: true
- ACLs: true

**Available Ports:**

Label column is a port label on a physical switch.

| Port   | Label | Type         | NOS Name      | Group | Default | Supported      |
|--------|-------|--------------|---------------|-------|---------|----------------|
| M1     | Mgmt  | Management   | Management0   | -     | -       | -              |
| E1/1   | 1     | QSFP28-100G  | 1/1 (Eth0)    | 1     | 100G    | 100G           |
| E1/2   | 2     | QSFP28-100G  | 1/2 (Eth4)    | 1     | 100G    | 100G           |
| E1/3   | 3     | QSFP28-100G  | 1/3 (Eth8)    | 1     | 100G    | 100G           |
| E1/4   | 4     | QSFP28-100G  | 1/4 (Eth12)   | 1     | 100G    | 100G           |
| E1/5   | 5     | QSFP28-100G  | 1/5 (Eth16)   | 2     | 100G    | 100G           |
| E1/6   | 6     | QSFP28-100G  | 1/6 (Eth20)   | 2     | 100G    | 100G           |
| E1/7   | 7     | QSFP28-100G  | 1/7 (Eth24)   | 2     | 100G    | 100G           |
| E1/8   | 8     | QSFP28-100G  | 1/8 (Eth28)   | 2     | 100G    | 100G           |
| E1/9   | 9     | QSFP28-100G  | 1/9 (Eth32)   | 3     | 100G    | 100G           |
| E1/10  | 10    | QSFP28-100G  | 1/10 (Eth36)  | 3     | 100G    | 100G           |
| E1/11  | 11    | QSFP28-100G  | 1/11 (Eth40)  | 3     | 100G    | 100G           |
| E1/12  | 12    | QSFP28-100G  | 1/12 (Eth44)  | 3     | 100G    | 100G           |
| E1/13  | 13    | QSFP28-100G  | 1/13 (Eth48)  | 4     | 100G    | 100G           |
| E1/14  | 14    | QSFP28-100G  | 1/14 (Eth52)  | 4     | 100G    | 100G           |
| E1/15  | 15    | QSFP28-100G  | 1/15 (Eth56)  | 4     | 100G    | 100G           |
| E1/16  | 16    | QSFP28-100G  | 1/16 (Eth60)  | 4     | 100G    | 100G           |
| E1/17  | 17    | QSFP28-100G  | 1/17 (Eth64)  | 5     | 100G    | 100G           |
| E1/18  | 18    | QSFP28-100G  | 1/18 (Eth68)  | 5     | 100G    | 100G           |
| E1/19  | 19    | QSFP28-100G  | 1/19 (Eth72)  | 5     | 100G    | 100G           |
| E1/20  | 20    | QSFP28-100G  | 1/20 (Eth76)  | 5     | 100G    | 100G           |
| E1/21  | 21    | QSFP28-100G  | 1/21 (Eth80)  | 6     | 100G    | 100G           |
| E1/22  | 22    | QSFP28-100G  | 1/22 (Eth84)  | 6     | 100G    | 100G           |
| E1/23  | 23    | QSFP28-100G  | 1/23 (Eth88)  | 6     | 100G    | 100G           |
| E1/24  | 24    | QSFP28-100G  | 1/24 (Eth92)  | 6     | 100G    | 100G           |
| E1/25  | 25    | QSFP28-100G  | 1/25 (Eth96)  | 7     | 100G    | 100G           |
| E1/26  | 26    | QSFP28-100G  | 1/26 (Eth100) | 7     | 100G    | 100G           |
| E1/27  | 27    | QSFP28-100G  | 1/27 (Eth104) | 7     | 100G    | 100G           |
| E1/28  | 28    | QSFP28-100G  | 1/28 (Eth108) | 7     | 100G    | 100G           |
| E1/29  | 29    | QSFP28-100G  | 1/29 (Eth112) | 8     | 100G    | 100G           |
| E1/30  | 30    | QSFP28-100G  | 1/30 (Eth116) | 8     | 100G    | 100G           |
| E1/31  | 31    | QSFP28-100G  | 1/31 (Eth120) | 8     | 100G    | 100G           |
| E1/32  | 32    | QSFP28-100G  | Ethernet124*  | 8     | 100G    | 100G           |
| E1/33  | 33    | SFP28-10G    | Ethernet128   | -     | 10G     | 1G, 10G        |
| E1/34  | 34    | SFP28-10G    | Ethernet129   | -     | 10G     | 1G, 10G        |

*Ethernet124 is a single port with no breakout.

**Port profile details:**

- **QSFP28-100G**: Default 100G, Supported 100G
- **SFP28-10G**: Default 10G, Supported 1G, 10G

**Example configuration:**

```yaml
apiVersion: fabric.hedgehog.com/v1
kind: Switch
metadata:
  name: example-dcs204
spec:
  profile: edgecore-dcs204
  ports:
    - name: E1/1
      speed: 100G
    - name: E1/33
      speed: 10G
```

---

## Edgecore DCS501

Profile Name (to use in switch object `.spec.profile`): **edgecore-dcs501**

Other names: Edgecore AS7712-32X

**Supported roles**: **spine**

Switch Silicon: **Broadcom TH**

Platform: **x86_64-accton_as7712_32x-r0**

Ports Summary: **32xQSFP28-100G**

**Supported features:**

- Subinterfaces: false
- VXLAN: false
- ACLs: true
- ACLs: true

**Available Ports:**

Label column is a port label on a physical switch.

| Port | Label | Type | Group | Default | Supported |
|------|-------|------|-------|---------|-----------|
| M1 |  | Management |  |  |  |
| E1/1 | 1 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/2 | 2 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/3 | 3 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/4 | 4 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/5 | 5 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/6 | 6 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/7 | 7 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/8 | 8 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/9 | 9 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/10 | 10 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/11 | 11 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/12 | 12 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/13 | 13 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/14 | 14 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/15 | 15 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/16 | 16 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/17 | 17 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/18 | 18 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/19 | 19 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/20 | 20 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/21 | 21 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/22 | 22 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/23 | 23 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/24 | 24 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/25 | 25 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/26 | 26 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/27 | 27 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/28 | 28 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/29 | 29 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/30 | 30 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/31 | 31 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/32 | 32 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |

**Port profile details:**

- **QSFP28-100G**: Default 100G, Supported 100G, 40G, 4x10G, 4x25G

**Example configuration:**

```yaml
apiVersion: fabric.hedgehog.com/v1
kind: Switch
metadata:
  name: example-dcs501
spec:
  profile: edgecore-dcs501
  ports:
    - name: E1/1
      speed: 100G
```

---

## Edgecore EPS203

Profile Name (to use in switch object `.spec.profile`): **edgecore-eps203**

Other names: Edgecore AS4630-54NPE

**Supported roles**: **limited-leaf**

Switch Silicon: **Broadcom TD3-X3**

Platform: **x86_64-accton_as4630_54npe-r0**

Ports Summary: **36xRJ45-2.5G, 12xRJ45-10G, 4xSFP28-25G, 2xQSFP28-100G**

**Supported features:**

- Subinterfaces: false
- VXLAN: true
- ACLs: true

**Available Ports:**

Label column is a port label on a physical switch.

| Port | Label | Type | Group | Default | Supported |
|------|-------|------|-------|---------|-----------|
| M1 |  | Management |  |  |  |
| E1/1 | 1 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/2 | 2 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/3 | 3 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/4 | 4 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/5 | 5 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/6 | 6 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/7 | 7 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/8 | 8 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/9 | 9 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/10 | 10 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/11 | 11 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/12 | 12 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/13 | 13 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/14 | 14 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/15 | 15 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/16 | 16 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/17 | 17 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/18 | 18 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/19 | 19 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/20 | 20 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/21 | 21 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/22 | 22 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/23 | 23 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/24 | 24 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/25 | 25 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/26 | 26 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/27 | 27 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/28 | 28 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/29 | 29 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/30 | 30 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/31 | 31 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/32 | 32 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/33 | 33 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/34 | 34 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/35 | 35 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/36 | 36 | Direct |  | 2.5G | 1G, 2.5G, AutoNeg supported (default: true) |
| E1/37 | 37 | Direct |  | 10G | 1G, 10G, AutoNeg supported (default: true) |
| E1/38 | 38 | Direct |  | 10G | 1G, 10G, AutoNeg supported (default: true) |
| E1/39 | 39 | Direct |  | 10G | 1G, 10G, AutoNeg supported (default: true) |
| E1/40 | 40 | Direct |  | 10G | 1G, 10G, AutoNeg supported (default: true) |
| E1/41 | 41 | Direct |  | 10G | 1G, 10G, AutoNeg supported (default: true) |
| E1/42 | 42 | Direct |  | 10G | 1G, 10G, AutoNeg supported (default: true) |
| E1/43 | 43 | Direct |  | 10G | 1G, 10G, AutoNeg supported (default: true) |
| E1/44 | 44 | Direct |  | 10G | 1G, 10G, AutoNeg supported (default: true) |
| E1/45 | 45 | Direct |  | 10G | 1G, 10G, AutoNeg supported (default: true) |
| E1/46 | 46 | Direct |  | 10G | 1G, 10G, AutoNeg supported (default: true) |
| E1/47 | 47 | Direct |  | 10G | 1G, 10G, AutoNeg supported (default: true) |
| E1/48 | 48 | Direct |  | 10G | 1G, 10G, AutoNeg supported (default: true) |
| E1/49 | 49 | Direct |  | 25G | 1G, 10G, 25G |
| E1/50 | 50 | Direct |  | 25G | 1G, 10G, 25G |
| E1/51 | 51 | Direct |  | 25G | 1G, 10G, 25G |
| E1/52 | 52 | Direct |  | 25G | 1G, 10G, 25G |
| E1/53 | 53 | Direct |  | 100G | 40G, 100G |
| E1/54 | 54 | Direct |  | 100G | 40G, 100G |

**Example configuration (Hedgehog v2025.04):**

```yaml
apiVersion: fabric.hedgehog.com/v1
kind: Switch
metadata:
  name: eps203-demo
spec:
  profile: edgecore-eps203
  hostname: eps203-demo
  mgmt:
    ipv4: 192.0.2.10/24
    gateway: 192.0.2.1
```

---

## Supermicro SSE-C4632SB

Profile Name (to use in switch object `.spec.profile`): **supermicro-sse-c4632sb**

Other names: Supermicro SSE-C4632SB

**Supported roles**: **spine**, **leaf**

Switch Silicon: **Broadcom TD3-X7 3.2T**

Platform: **x86_64-cel_seastone_2-r0**

Ports Summary: **32xQSFP28-100G, 1xSFP28-10G**

**Supported features:**

- Subinterfaces: true
- VXLAN: true
- ACLs: true

**Available Ports:**

Label column is a port label on a physical switch.

| Port | Label | Type | Group | Default | Supported |
|------|-------|------|-------|---------|-----------|
| M1 |  | Management |  |  |  |
| E1/1 | 1 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/2 | 2 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/3 | 3 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/4 | 4 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/5 | 5 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/6 | 6 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/7 | 7 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/8 | 8 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/9 | 9 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/10 | 10 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/11 | 11 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/12 | 12 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/13 | 13 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/14 | 14 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/15 | 15 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/16 | 16 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/17 | 17 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/18 | 18 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/19 | 19 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/20 | 20 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/21 | 21 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/22 | 22 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/23 | 23 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/24 | 24 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/25 | 25 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/26 | 26 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/27 | 27 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/28 | 28 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/29 | 29 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/30 | 30 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/31 | 31 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/32 | 32 | Breakout |  | 1x100G | 1x100G, 1x40G, 4x10G, 4x25G |
| E1/33 | 33 | Direct |  | 10G | 1G, 10G |

## Virtual Switch

Profile Name (to use in switch object `.spec.profile`): **vs**

This is a virtual switch profile. It's for testing/demo purpose only with limited features and performance.

**Supported roles**: **spine**, **leaf**

Switch Silicon: **vs**

Ports Summary: **48xSFP28-25G**

**Supported features:**

- Subinterfaces: true
- VXLAN: true
- ACLs: false

**Available Ports:**

Label column is a port label on a physical switch.

| Port | Label | Type | Group | Default | Supported |
|------|-------|------|-------|---------|-----------|
| M1 |  | Management |  |  |  |
| E1/1 | 1 | Port Group | 1 | 25G | 10G, 25G |
| E1/2 | 2 | Port Group | 1 | 25G | 10G, 25G |
| E1/3 | 3 | Port Group | 1 | 25G | 10G, 25G |
| E1/4 | 4 | Port Group | 1 | 25G | 10G, 25G |
| E1/5 | 5 | Port Group | 2 | 25G | 10G, 25G |
| E1/6 | 6 | Port Group | 2 | 25G | 10G, 25G |
| E1/7 | 7 | Port Group | 2 | 25G | 10G, 25G |
| E1/8 | 8 | Port Group | 2 | 25G | 10G, 25G |
| E1/9 | 9 | Port Group | 3 | 25G | 10G, 25G |
| E1/10 | 10 | Port Group | 3 | 25G | 10G, 25G |
| E1/11 | 11 | Port Group | 3 | 25G | 10G, 25G |
| E1/12 | 12 | Port Group | 3 | 25G | 10G, 25G |
| E1/13 | 13 | Port Group | 4 | 25G | 10G, 25G |
| E1/14 | 14 | Port Group | 4 | 25G | 10G, 25G |
| E1/15 | 15 | Port Group | 4 | 25G | 10G, 25G |
| E1/16 | 16 | Port Group | 4 | 25G | 10G, 25G |
| E1/17 | 17 | Port Group | 5 | 25G | 10G, 25G |
| E1/18 | 18 | Port Group | 5 | 25G | 10G, 25G |
| E1/19 | 19 | Port Group | 5 | 25G | 10G, 25G |
| E1/20 | 20 | Port Group | 5 | 25G | 10G, 25G |
| E1/21 | 21 | Port Group | 6 | 25G | 10G, 25G |
| E1/22 | 22 | Port Group | 6 | 25G | 10G, 25G |
| E1/23 | 23 | Port Group | 6 | 25G | 10G, 25G |
| E1/24 | 24 | Port Group | 6 | 25G | 10G, 25G |
| E1/25 | 25 | Port Group | 7 | 25G | 10G, 25G |
| E1/26 | 26 | Port Group | 7 | 25G | 10G, 25G |
| E1/27 | 27 | Port Group | 7 | 25G | 10G, 25G |
| E1/28 | 28 | Port Group | 7 | 25G | 10G, 25G |
| E1/29 | 29 | Port Group | 8 | 25G | 10G, 25G |
| E1/30 | 30 | Port Group | 8 | 25G | 10G, 25G |
| E1/31 | 31 | Port Group | 8 | 25G | 10G, 25G |
| E1/32 | 32 | Port Group | 8 | 25G | 10G, 25G |
| E1/33 | 33 | Port Group | 9 | 25G | 10G, 25G |
| E1/34 | 34 | Port Group | 9 | 25G | 10G, 25G |
| E1/35 | 35 | Port Group | 9 | 25G | 10G, 25G |
| E1/36 | 36 | Port Group | 9 | 25G | 10G, 25G |
| E1/37 | 37 | Port Group | 10 | 25G | 10G, 25G |
| E1/38 | 38 | Port Group | 10 | 25G | 10G, 25G |
| E1/39 | 39 | Port Group | 10 | 25G | 10G, 25G |
| E1/40 | 40 | Port Group | 10 | 25G | 10G, 25G |
| E1/41 | 41 | Port Group | 11 | 25G | 10G, 25G |
| E1/42 | 42 | Port Group | 11 | 25G | 10G, 25G |
| E1/43 | 43 | Port Group | 11 | 25G | 10G, 25G |
| E1/44 | 44 | Port Group | 11 | 25G | 10G, 25G |
| E1/45 | 45 | Port Group | 12 | 25G | 10G, 25G |
| E1/46 | 46 | Port Group | 12 | 25G | 10G, 25G |
| E1/47 | 47 | Port Group | 12 | 25G | 10G, 25G |
| E1/48 | 48 | Port Group | 12 | 25G | 10G, 25G |

```
