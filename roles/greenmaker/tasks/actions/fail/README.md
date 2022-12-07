# Action Name: fail

## Description
This remediation action will stop the execution of a workflow by manually injecting a failure and raising an error. the  Workflow execution reporting data will be gathered automatically prior to exit.

## Action Definition

### Action Type
Remediation Action

### Supported Input Arguments

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| reason | string | Supplies a descriptive reason for failing the workflow that can be used for post-processing purposes and/or documentation purposes after workflow execution completes | No |

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
        name: "Fail Action Example "
        description: |
          Execute Fail action test scenario 
      on_true:
        - echo:
            args:
              message: |
                Preparing to invoke fail action.
        - fail:
            args:
              reason: Workflow logic detected a failure situation which required the workflow to exit with as a execution failue 
              
```
