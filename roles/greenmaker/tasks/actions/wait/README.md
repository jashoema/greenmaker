# Action Name: wait

## Description
This remediation action will pause execution of the workflow and wait for a specified period of time in seconds before continuing execution.  This is useful for scenarios where waiting on a device or module to boot up is necessary before continuing the workflow execution.

## Action Definition

### Action Type
Remediation Action

### Supported Input Arguments

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| duration | String | Time in seconds for which to pause execution. | Yes |

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

- all

### Sample Usage

``` yaml

workflow:
  - step:
      metadata:
        name: "enable_lc"
        description: "Execute configuration to re-enable line card after physical reseat."
      validation: {}
      on_true:
        - echo: 
            args:
              message: "Re-enabling line card after physical reseat."
        - config_cli:
            args:
              commands:
                - "no hw-module slot {{ module_id }} shutdown"
        - wait:
            args:
              duration: 300

```