# Action Name: isolate_device

## Description
This remediation action will isolate from the network the device targeted by the current workflow. The workflow engine (i.e. Greenmaker) is responsible for implementing the abstractions necessary to isolate the target device based upon its operating system and role in the network. This may involve routing protocol changes, interface state changes, and other configuration changes necessary to seamlessly remove the device from the path of production network traffic.

## Action Definition

### Action Type
Remediation Action

### Supported Input Arguments

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| N/A |  |  |  |

### Supported Output Parameters

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| N/A |  |  |  |

### Supported Simulation Input Parameters

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| N/A |  |  |  |

### Return Criteria ###

N/A

### Supported ansible_network_os

**Currently unsupported / in development**

### Sample Usage

``` yaml

workflow:
  - step:
      metadata:
        name: "isolate_device"
        description: |
          Isolate device before taking actions to troubleshooting and/or remediate issue
      validation: {}
      on_true:
        - isolate_device: {}

```