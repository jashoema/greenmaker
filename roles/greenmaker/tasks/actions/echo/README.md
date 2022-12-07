# Action Name: echo

## Description
This remediation action simply provides output of a string to the console.  It is typically used for debugging or logging purposes, and it is analagous to the Ansible "debug" module.  Jinja2 variables can be referenced in the string to print the value of a variable.

## Action Definition

### Action Type
Remediation Action

### Supported Input Arguments

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| message | String | Text that should be output to the console. Can include Jinja2 variables. | Yes |

### Supported Output Parameters

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| N/A | | |

### Supported Simulation Input Parameters

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| N/A | | |

### Return Criteria ###

N/A

### Supported ansible_network_os

- all

### Sample Usage

``` yaml

workflow:
  - step:
      metadata:
        name: "validate_lc_failure_after_reseat"
        description: |
          "Execute diagnostic commands to verify the health of the affected line card after physical reseat
          during manual action.  If failure is still present, open suport case."
      validation:
        eval_cli:
          args:
            commands:
              - show module
            pattern: "{{ module_id | default() }}.+hw-faulty"
          simulation:
            input: validate_lc_failure_after_reseat_sim
      on_true:
        - echo: 
            args:
              message: |
                Line card failure in slot {{ module_id | default() }} still present after physical reseat.  Support case will be opened.
      on_false:
        - echo: 
            args:
              message: |
                Line card failure in slot {{ module_id | default() }} no longer present after physical reseat.  Exiting.
```