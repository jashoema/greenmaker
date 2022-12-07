# Action Name: and

## Description
This validation action evaluates the boolean results of a list of other validation actions using a logical AND

## Action Definition

### Action Type
Validation Action

### Supported Input Arguments

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| N/A |  |  |  |

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
        name: "Simple AND Sample Scenario postive matching"
        description: |
          Demonstration of postive matching on the and action by matching both embedded eval_var actions
      validation:
        and:
          - eval_var:
              args:
                var_name: and_test_string
                pattern: " AND condition matching "
              output:
                - source: pattern_search[0]
                  target: result_string
                  
              settings:
                test:
                  output: and_test_scenario_output
          - eval_var:
              args:
                var_name: and_test_string
                pattern: " AND condition matching "
              output:
                - source: pattern_search[0]
                  target: result_string
              settings:
                test:
                  output: and_test_scenario_output
      on_true:
        - echo: 
            args:
              message: |
               "Exiting workflow as and scenario made a postive match ."
      on_false:
        - echo: 
            args:
              message: |
               "Exiting workflow as conditon was not met in the scenario."
  - step:
      metadata:
        name: "Simple AND Sample Scenario negative matching"
        description: |
          Demonstration of the and action by not matching both embedded eval_var actions
      validation:
        and:
          - eval_var:
              args:
                var_name: and_test_string
                pattern: " AND condition matching "
              output:
                - source: pattern_search[0]
                  target: result_string
                  
              settings:
                test:
                  output: and_test_scenario_output
          - eval_var:
              args:
                var_name: and_test_string
                pattern: " AND NOT condition matching "
              output:
                - source: pattern_search[0]
                  target: result_string
              settings:
                test:
                  output: and_test_scenario_output
      on_true:
        - echo: 
            args:
              message: |
               "Exiting workflow as both conditions made a postive made a postive match ."
      on_false:
        - echo: 
            args:
              message: |
               "Exiting workflow as both conditons were not met in the scenario."

```
