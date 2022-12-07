# Action Name: manual_action

## Description
This remediation action will temporarily halt execution of the workflow to allow for a manual action to be performed by a third party operator.  For example, in order to complete a line card failure workflow, it may be necessary to physically reseat the line card that is being evaluated for failure.  In such a case, manual_action would be used to hand-off the execution to a third party for performing this action.  

manual_action expects that the alerting pipeline which has executed this workflow will know how to handle a workflow that is halted on a "manual_action" event.  This might look like the pipeline processing the results of the workflow, recognizing that a manual_action was called, and generating a ticket to ensure that the manual action is taken by an operator.  When that operator completes their action, the pipeline should be notified (e.g. by the closing of a ticket) to re-trigger the same workflow against the same target device, and the "resume_step" argument value would be used to determine the name of the step at which the workflow will be resumed.  If no "resume_step" is explicitly supplied, the default value will be the next step in the workflow.

When manual_action executes, it will report a list of all scenario variables maintained by the workflow execution at that time.  The alerting pipeline is responsible for reading these variables and feeding them back into the workflow at the time when the workflow is re-triggered to complete execution after the manual action has been performed.

## Action Definition

### Action Type
Remediation Action

### Supported Input Arguments

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| name | String | A name that describes the action which will be taken by the manual_action. This name can potentially be keyed upon by the alerting pipeline as a way to understand how to handle the manual_action execution. | Yes  |
| description | String | A description of what should be performed during the manual_action event | Yes |
| resume_step | String | The name of the step at which execution of the workflow should resume once the manual_action is completed. If no value is specified, the default value will be the name of the next step in the workflow. Alerting pipeline should supply this as an input variable when re-triggering a workflow after completion of the manual_action. | No |

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
              name: "physical_lc_reseat"
              description: "Physical reseat of Cat9K line card for module"
              resume_step: "enable_lc"
      on_false:
        - echo: 
            args:
              message: |
                Line card failure no longer present after power cycle.  Exiting workflow.
        - exit: {}

```
