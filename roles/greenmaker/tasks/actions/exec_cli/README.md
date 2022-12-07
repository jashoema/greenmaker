# Action Name: exec_cli

## Description
This remediation action executes exec-mode CLI commands against the target device using an OS-specific abstraction.  It is used for action-oriented changes, such as reloading a device, and is not used for applying persistent configuration to a target device (for that, see config_cli).  It is analagous to Ansible network OS configuration modules such as ios_command, eos_command, iosxr_command, etc.  

## Action Definition

### Action Type
Remediation Action

### Supported Input Arguments

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| commands | List of Strings | List of CLI commands that should be applied to the target device. J2 templating for variables is supported. | Yes |
| timeout | Integer | Timeout value in seconds for execution of CLI commands against the target device (default 60 seconds) | No |
| ignore_errors | Boolean | When set to true (default: false), the exec_cli action will not generate a failure condition when one or more of the specified commands fails to execute correctly due to syntax.  This can be helpful when executing exec_cli across different types of devices that may require different syntax for retrieving the same diagnostic data, allowing execution of multiple commands and running the pattern search against any commands that succeed. | No |

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

- ios
- iosxr
- nxos
- eos

### Sample Usage

``` yaml

workflow:
  - step:
      metadata:
        name: "validate_lc_failure"
        description: |
          Execute diagnostic commands to verify the health of the affected line card.
          If failure is present, reload the affected line card.
      validation:
        eval_cli:
          args:
            commands:
              - show module
            pattern: "{{ module_id }}.+hw-faulty"
          simulation:
            input: validate_lc_failure_sim
      on_true:
        - echo: 
            args:
              message: |
                Possible line card failure present in module {{ module_id }}.
                Attempting power cycle of line card to resolve.
        - exec_cli:
            args:
              commands:
                - "hw-module subslot {{ module_id }}/0 oir power-cycle force"
        - wait:
            args:
              duration: 1
      on_false:
        - echo: 
            args:
              message: |
                Line card failure not detected.  Exiting.
        - exit: {}

```
