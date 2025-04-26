<!-- Diátaxis: Reference -->

# Fabric Configuration

> **Learning Objectives**
> By the end of this reference, you will:
> - Understand the structure and purpose of the `fab.yaml` fabric configuration file
> - Use `hhfab` to initialize, validate, and build fabric configurations
> - Reference and customize users, credentials, logging, telemetry, and other settings
> - Cross-link to wiring diagrams and API documentation for advanced use

---

## Overview

The `fab.yaml` file is the core configuration for Hedgehog Fabric. It defines users, credentials, logging, telemetry, and all non-wiring settings. `fab.yaml` consists of multiple YAML documents separated by `---` (per the YAML spec). For more on `hhfab init`, see `hhfab init --help`.

---

## HHFAB Workflow

After [downloading `hhfab`](../getting-started/download.md):

1. Initialize configuration:
    ```sh
    hhfab init
    # See flags to customize initial configuration
    ```
2. Adjust the `fab.yaml` file as needed
3. Build your [wiring diagram](build-wiring.md)
4. Validate configuration:
    ```sh
    hhfab validate
    ```
5. (Optional) Visualize with:
    ```sh
    hhfab diagram
    ```
6. Build the image:
    ```sh
    hhfab build
    ```

Or import existing configuration and wiring files:

```sh
hhfab init -c fab.yaml -w wiring-file.yaml -w extra-wiring-file.yaml
hhfab validate
hhfab build
```

After this workflow, you will have an `.img` file suitable for installing the control node and bringing up the fabric switches.

---

## Complete Example: `fab.yaml`

Below is a comprehensive `fab.yaml` configuration. For advanced options, see the [Fabricator API Reference](../../reference/include-fab-api/).

```yaml
apiVersion: fabricator.githedgehog.com/v1beta1
kind: Fabricator
metadata:
  name: default
  namespace: fab
spec:
  config:
    control:
      tlsSAN:
        - "customer.site.io"
      ntpServers:
        - time.cloudflare.com
        - time1.google.com
      defaultUser: # username 'core' on all control nodes
        password: "hash..." # generate hash with openssl passwd -5
        authorizedKeys:
          - "ssh-ed25519 key..." # generate ssh key with ssh-keygen

    fabric:
      mode: spine-leaf # "spine-leaf" or "collapsed-core"
      includeONIE: true
      defaultSwitchUsers:
        admin: # at least one user with name 'admin' and role 'admin'
          role: admin
          password: "hash..." # generate hash with openssl passwd -5
          authorizedKeys:
            - "ssh-ed25519 key..."
        op: # optional read-only user
          role: operator
          password: "hash..." # generate hash with openssl passwd -5
          authorizedKeys:
            - "ssh-ed25519 key..." # generate ssh key with ssh-keygen

      defaultAlloyConfig:
        agentScrapeIntervalSeconds: 120
        unixScrapeIntervalSeconds: 120
        unixExporterEnabled: true
        collectSyslogEnabled: true
        lokiTargets:
          lab:
            url: http://url.io:3100/loki/api/v1/push
            labels:
              descriptive: name
        prometheusTargets:
          lab:
            url: http://url.io:9100/api/v1/push
            labels:
              descriptive: name
            sendIntervalSeconds: 120

---
apiVersion: fabricator.githedgehog.com/v1beta1
kind: ControlNode
metadata:
  name: control-1
  namespace: fab
spec:
  bootstrap:
    disk: "/dev/sda" # disk to install OS on, e.g. "sda" or "nvme0n1"
  external:
    interface: eno2 # customer interface to manage control node
    ip: dhcp # IP address for external interface
  management: # interface that manages switches in private management network
    interface: eno1

# Currently only one ControlNode is supported
```

---

## Configure Control Node and Switch Users

#### Control Node Users
Configuring control node and switch users is done either passing 
`--default-password-hash` to `hhfab init` or editing the resulting `fab.yaml` 
file emitted by `hhfab init`.  The default username on the control node is
`core`.

#### Switch Users
There are two users on the switches, `admin` and `operator`. The `operator` user has
read-only access to `sonic-cli` command on the switches. The `admin` user has
broad administrative power on the switch. 
In order to avoid conflicts, do not use the following usernames: `operator`,`hhagent`,`netops`.

---

## NTP and DHCP
The control node uses public NTP servers from Cloudflare and Google by default.
The control node runs a DHCP server on the management network. See the [example
file](#complete-example-file).

---

## Control Node
The control node is the host that manages all the switches, runs k3s, and serves images. 
The **management** interface is for the control node to manage the fabric 
switches, *not* end-user management of the control node. For end-user 
management of the control node specify the **external** interface name.

---

## Telemetry & Logging

Hedgehog Fabric supports remote telemetry and logging via [Prometheus Remote-Write](https://prometheus.io/docs/specs/prw/remote_write_spec/) and Loki API. Metrics include port speeds, counters, errors, operational status, transceivers, fans, power supplies, temperature sensors, BGP neighbors, LLDP neighbors, and more. Logs include Hedgehog agent logs.

To enable telemetry after installation, use:

```sh
kubectl patch -n fab --type merge fabricator/default --patch-file telemetry.yaml
```

For additional options, see the `AlloyConfig` [struct in Fabric repo](https://github.com/githedgehog/fabric/blob/master/api/meta/alloy.go).

```yaml
spec:
  config:
    fabric:
      defaultAlloyConfig:
        agentScrapeIntervalSeconds: 120
        unixScrapeIntervalSeconds: 120
        unixExporterEnabled: true
        lokiTargets:
          grafana_cloud: # target name, multiple targets can be configured
              basicAuth: # optional
                  password: "<password>"
                  username: "<username>"
              labels: # labels to be added to all logs
                  env: env-1
              url: https://logs-prod-021.grafana.net/loki/api/v1/push
        prometheusTargets:
          grafana_cloud: # target name, multiple targets can be configured
              basicAuth: # optional
                  password: "<password>"
                  username: "<username>"
              labels: # labels to be added to all metrics
                  env: env-1
              sendIntervalSeconds: 120
              url: https://prometheus-prod-36-prod-us-west-0.grafana.net/api/prom/push
        unixExporterCollectors: # list of node-exporter collectors to enable, https://grafana.com/docs/alloy/latest/reference/components/prometheus.exporter.unix/#collectors-list
        - cpu
        - filesystem
        - loadavg
        - meminfo
        collectSyslogEnabled: true # collect /var/log/syslog on switches and forward to the lokiTargets
```

---

> **See Also:**
> - [Build Wiring Diagram](./build-wiring.md)
> - [System Requirements](./requirements.md)
> - [Install Hedgehog Fabric](./install.md)
> - [API Reference](../../reference/include-fab-api/)

---

> **Next:** [Supported Devices](./supported-devices.md)
