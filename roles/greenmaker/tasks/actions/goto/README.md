# Action Name: goto

## Description
This remediation action will skip ahead ("go to") a future step in the workflow by referencing the name of the step.  This can be useful for scenarios where depending upon the outcome of a validation, you may wish to skip ahead to a step that isn't the next step in the sequence of steps.  The target step should specified by name using the "target" argument.

## Action Definition

### Action Type
Remediation Action

### Supported Input Arguments

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| target | String | Name of the step that should be executed next. Must match the metadata name of the target step. | Yes |

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
          simulation:
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
                Line card failure no longer present after power cycle.  Move to a future step called "future_step" to check for other possible issues.
        - goto:
            args:
              target: "future_step"

```