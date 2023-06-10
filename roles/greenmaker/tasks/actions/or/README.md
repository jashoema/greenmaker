# Action Name: or

## Description
This validation action evaluates the boolean results of a list of other validation actions using a logical OR

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
- step:
      metadata:
        name: "extract_neighbor_addr"
        description: |
          Extract neighbor_addr, neighbor_addr_type, and addr_regex from syslog message that triggered the alert
      validation:
        or:
          - eval_var:
              args:
                var_name: alert_vars.syslog
                pattern: "neighbor ({{ string_ipv4_addr_regex }}) Down"
              output:
                - source: pattern_search[0]
                  target: neighbor_addr
                - source: string_ipv4
                  target: neighbor_addr_type
                - source: string_ipv4_addr_regex
                  target: addr_regex
              settings:
                test:
                  output: extract_neighbor_addr_v4_test_output
          - eval_var:
              args:
                var_name: alert_vars.syslog
                pattern: "neighbor ({{ string_ipv6_addr_regex }}) Down"
              output:
                - source: pattern_search[0]
                  target: neighbor_addr
                - source: string_ipv6
                  target: neighbor_addr_type
                - source: string_ipv6_addr_regex
                  target: addr_regex
              settings:
                test:
                  output: extract_neighbor_addr_v6_test_output
      on_false:
        - exit:
            args:
              reason: "Unable to extract neighbor address from log message.  Exiting."
```
