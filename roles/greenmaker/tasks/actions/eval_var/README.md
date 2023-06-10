# Action Name: eval_var

## Description
This validation action evaluates the contents of a variable to look for the presence of a specified regular expression. If the regular expression is present, the action returns "true".  If the regular expression is not present, the action returns "false".  If parentheses/groups are used in the regular expression of the "pattern" argument, they can be used to extract data from the command output and assign that data to one or more variables.

## Action Definition

### Action Type
Validation Action

### Supported Input Arguments

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| var_name | String | The name of the variable to be evaluated. Dictionary keys and/or list elements can be used to specify a value contained within a data structure. | Yes |
| pattern | String | Regular expression that will be searched for in the content of the variable. If the regex is found in the variable content, the validation renders a true result, and the "on_true" actions for the step are executed. If the regex is not found, the validation renders a false result, and the "on_false" actions for the step are executed. This argument uses Python regular expression syntax. Additionally, parentheses can be used to extract one or more variables from the data matched by the regular expression. The extracted content can be assigned to variables using the "target" output parameter.  | Yes |

### Supported Output Parameters

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| source | String | Source data extracted from regex pattern match that we wish to assign to a variable for future use in Greenmaker.  Must use the value of `pattern_search[<index_number>]` for extracting data from the regex pattern match, where index_number is the index of the capture group from our regex that we want to use, starting with `pattern_search[0]` for the first capture group. | No |
| target | String | Name of the variable to which extracted regex content should be assigned. | No |

### Supported Test Input Parameters

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| N/A | | | |

### Return Criteria ###

- Return true: When the regular expression specified in the "pattern" input argument matches the contents of the specified variable, a boolean value of "true" will be returned
- Return false: When the regular expression specified in the "pattern" input argument does not match the contents of the specified variable, a boolean value of "false" will be returned

### Supported ansible_network_os

- all

### Sample Usage

``` yaml

workflow:
  - step:
      metadata:
        name: "extract_lc_number"
        description: |
          Extract line card number from syslog message that triggered the alert
      validation:
        eval_var:
          args:
            var_name: alert_vars.syslog
            pattern: "HW faulty on Slot ([0-9]+) Subslot"
          output:
            - target: module_id
      on_false:
        - echo: 
            args:
              message: |
                Unable to extract line card ID from log message.  Exiting.
        - exit: {}           

```
