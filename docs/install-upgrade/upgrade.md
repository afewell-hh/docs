<!-- Diátaxis: How-to Guide -->

# Upgrade Hedgehog Fabric

> **Learning Objectives**
> By the end of this how-to, you will:
> - Prepare for and execute an in-place upgrade of Hedgehog Fabric (control node and switches)
> - Generate and apply a self-contained upgrade package
> - Validate a successful upgrade and know how to troubleshoot

---

## Upgrades from Beta-1 Onwards

Starting with Beta-1, the upgrade process is streamlined and fully automated. The control node is upgraded in place, and agents/switches are upgraded using the control node.

### Step-by-Step Upgrade Procedure

1. **Export your current fabric configuration:**

    ```sh
    kubectl hhfab config export > fab.yaml
    ```

2. **On the node with the new version of `hhfab`:**

    ```sh
    hhfab init -c fab.yaml -f
    hhfab build --mode=manual
    # This generates result/control--control-1--install.tgz
    ```

3. **Upload the upgrade package to the control node:**

    ```sh
    scp result/control--control-1--install.tgz <user>@<control-node>:/tmp/
    ```

4. **Unpack and run the upgrade:**

    ```sh
    tar xzf control--control-1--install.tgz
    cd control--control-1--install
    sudo ./hhfab-recipe upgrade
    ```

    - The upgrade will prompt for a reboot as part of upgrading Flatcar on the control node.

5. **Validate the upgrade:**

    ```sh
    kubectl -n fab get fab/default -o=jsonpath='{.status.versions.fabricator.controller}'
    # Compare the version to the release notes
    ```

- The upgrade process is idempotent and can be run multiple times safely.
- See [Release Notes](../release-notes/index.md) for details on your version and [SONiC Upgrade](#upgrade-sonic) if applicable.

---

## Upgrade from Alpha-7 to Beta-1

### Prerequisites
- Ensure hardware meets [system requirements](requirements.md#control-node).
- The upgrade is destructive—back up all needed data from the server.

### Management Network
- Beta-1 uses RJ-45 management ports of switches (not front panel ports).
- A dedicated management network must be in place and cabled before Beta-1 installation.
- The control node runs a DHCP server on this network and must be the sole DHCP server.
- Do not co-mingle other equipment/services on this network.

### Switch ONIE Installation
- Beta-1 uses the switch vendor ONIE for NOS installation.
- Install the latest vendor-provided ONIE (do **not** use Hedgehog ONIE).

### Changes to the Wiring Diagram

* All API versions changed from `v1alpha2` to `v1beta1`
* `Server[control=true]` object type was removed and replaced with `ControlNode` object in the `fabricator.githedgehog.com/v1beta1` API (.spec.control field removed), `Server` object only describes workload server now
* All initial configuration is mainly still available using the `hhfab init` flags but now configurable in the `fab.yaml` file it creates and available in the runtime in the `Fabricator` object in the `fabricator.githedgehog.com/v1beta1` API
* `Connection[type=management]` object removed, relevant information is now present on the `ControlNode` object in the form of the management interface and its config, switches are always connected using management port
* `.spec.location` remove from `Switch` object
* `.spec.boot` added to `Switch` object with `mac` and `serial` fields, at least **one** of them is required to identify switch for installation

### Install The Control Node
Follow the [instructions](install.md#build-control-node-configuration-and-installer) for installing the Beta-1 Fabric on a control node.

## Install SONiC using ONIE 

As the switches boot up, select the `ONIE` option from the grub screen. From
there select the `ONIE: Install OS` option. In the grub boot menu the asterisk
(`*`) character functions as an indicator of the option that would be executed
if the `enter` key was pressed. For example to enter the `ONIE` menu it would
appear as `*ONIE` on the screen. The install option will cause the switch to 
begin searching for installation media, this media is supplied by the control node.

## Upgrade SONiC

Occasionally some fabric upgrades will include upgrades to the SONiC Network
Operating System. Upgrading SONiC will cause the switch to not pass traffic
during the upgrade process. For that reason, SONiC is not upgraded
automatically and the user is encouraged to schedule a maintenance window for
the upgrade. 

To upgrade a switch on an existing deployment use the command `kubectl fabric
switch reinstall --name switch-name`. The switch will be gracefully shutdown,
and reboot into the `ONIE` boot environment for reinstallation. After the
switch boots the hedgehog agent will automatically restore the configuration
and traffic will resume without user intervention. 

> **See Also:**
> - [System Requirements](./requirements.md)
> - [Install Hedgehog Fabric](./install.md)
> - [Release Notes](../release-notes/index.md)

---

> **Next:** [Build Wiring](./build-wiring.md)
