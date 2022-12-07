# Action Name: call

## Description
The "call" action is used to call a re-usable workflow logic from the "library" section of the scenario.  Its purpose is to allow for repeatable action sequences to be variable-ized and maintained in a separate portion of the scenario to help make workflows more readable and easier to maintain.  The call action can be referenced in all places where actions can typically be referenced, including the validation section, the on_true section, and the on_false section.  

## Action Definition

### Action Type
Validation Action or Remediation Action

### Supported Input Arguments

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| label | String | Name of library workflow logic variable that should be invoked  | Yes |

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
        name: "validate_lc_failure"
        description: |
          Execute diagnostic commands to verify the health of the affected line card.
          If failure is present, reload the affected line card.
      validation:
        eval_cli:
          args:
            commands:
              - show module
            pattern: "{{ module_id | default('') }}.+hw-faulty"
          simulation:
            input: validate_lc_failure_sim
      on_true:
        - call:
            args:
              label: linecard_reboot
      on_false:
        - echo: 
            args:
              message: |
                Line card failure not detected.  Exiting.
        - exit: {}

library:
  linecard_reboot:
    - echo: 
        args:
          message: |
            Possible line card failure present in module {{ module_id | default('') }}.
            Attempting power cycle of line card to resolve.
    - exec_cli:
        args:
          commands:
            - "hw-module subslot {{ module_id | default('') }}/0 oir power-cycle force"
    - wait:
        args:
          duration: 100

```