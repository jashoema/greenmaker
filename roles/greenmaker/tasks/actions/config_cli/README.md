# Action Name: config_cli

## Description
This remediation action applies specified CLI configuration changes to the target device using an OS-specific abstraction.  It is analagous to Ansible network OS configuration modules such as ios_config, eos_config, iosxr_config, etc.  

## Action Definition

### Action Type
Remediation Action

### Supported Input Arguments

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| commands | List of Strings | List of CLI commands that should be applied to the persistent configuration on the target device. J2 templating for variables is supported. | Yes |
| timeout | Integer | Timeout value in seconds for execution of CLI commands against the target device (default 60 seconds) | No |

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

- ios
- iosxr
- nxos
- eos

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