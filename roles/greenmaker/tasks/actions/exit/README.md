# Action Name: exit

## Description
This remediation action will stop the execution of a workflow and exit cleanly.  Workflow execution reporting data will be gathered automatically prior to exit.

## Action Definition

### Action Type
Remediation Action

### Supported Input Arguments

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| reason | string | Supplies a descriptive reason for exiting the workflow that can be used for post-processing purposes and/or documentation purposes after workflow execution completes | No |

### Supported Output Parameters

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| N/A |  |  |  |

### Supported Test Input Parameters

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
        name: "validate_lc_failure_after_reboot"
        description: |
          Execute diagnostic commands to verify the health of the affected line card after reboot.
          If failure is still present, shutdown line card and attempt physical reseat.
      validation:
        eval_cli:
          args:
            commands:
              - show module
            pattern: "{{ module_id }}.+hw-faulty"
          test:
            input: validate_lc_failure_after_reboot_sim
      on_true:
        - echo: 
            args:
              message: |
                Line card failure present after power cycle.  Shutting down line card
                in preparation for physical reseat.
        - config_cli:
            args:
              commands:
                - "hw-module slot {{ module_id }} shutdown"
        - manual_action:
            args:
              name: "Physical reseat of Cat9K line card for module"
              resume_step: "enable_lc"
      on_false:
        - echo: 
            args:
              message: |
                Line card failure no longer present after power cycle.  Exiting workflow.
        - exit: {}

```
