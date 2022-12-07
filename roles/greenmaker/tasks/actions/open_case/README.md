# Action Name: open_case

## Description
This remediation action will collect specified diagnostic commands from a device, open a support case with a network vendor, and attach the collected data to the case to help further assist in diagnosing an issue.

To open a case, the workflow engine (i.e. Greenmaker role) implements vendor-specific abstractions for interacting with the available support case API for each vendor (e.g. ServiceGrid REST API for Cisco).

When a case is opened, all collected data, including diagnostic commands from the "attach_commands" arguments and logs from workflow execution are compressed and attached to the support case.

For scenarios in which the alerting pipeline will handle case creation, the open_case action can be executed in "passive" mode.  In passive mode, only the collection/compression of diagnostic data will occur, and no interaction with the vendor's support case API will occur.

Diagnostic data captured by attach_commands will be saved in a file called `<hostname>_attach.zip` and saved in the same folder as the log files (remotely or locally, depending upon configured settings).

Certain input variables are required for case creation support via Cisco ServiceGrid.  These input variables will be documented at a later date.

## Action Definition

### Action Type
Remediation Action

### Supported Input Arguments

| Name | Type | Description | Mandatory |
|------|------|-------------|-----------|
| title | String | Title of the vendor support case. May be trucated depending upon vendor API character limits. | Yes |
| description | String | Description of the issue experienced by the target device. | Yes |
| severity | String | Severity number to use when opening the case. Dependent upon vendor severity definitions. | Yes |
| mode | String | Supported modes are "passive" and "active". "active" mode will attempt to create a support case with the vendor using available API and attach data to the case. "passive" mode will simply collect the "attach_commands" from the target device and package together diagnostic data in a compressed file, but will not open a vendor case.  Default is "passive".  Note: "active" mode is currently only supported for Cisco operating systems (via ServiceGrid API integration) | No |
| destinations | List of Strings | Supported destinations are "internal" and "external".  \["internal"\] specifies that the destination ticketing system for this open_case action is the internal ticketing system. Handling of ticket creation will be handed off to the alert piepline; no action is required by greenmaker.  \["external"\] specifies that the destination ticketing system for this open_case action is an external vendor ticketing system. When open_case "mode" argument is set to "active", this will result in a support case being created via vendor ticketing system API, such as Cisco ServiceGrid. When open_case "mode" argument is set to "passive", no action is required by Greenmaker, and it is expected that the alert pipeline will handle external ticket creation with the vendor.  \["internal","external"\] specifies that both an internal and external ticket should be created. Default value is \["internal"\]. | No |
| attach_commands | List of Strings | CLI diagnostic commands for which output should be collected, zipped, and attached to the support case.  | No |
| timeout | Integer | Timeout value in seconds for execution of attach_commands against the target device (default 120 seconds) | No |
| ignore_errors | Boolean | When set to true (default: false), the open_case action will not generate a failure condition when one or more of the specified commands fails to execute correctly due to syntax.  This can be helpful when executing open_case across different types of devices that may require different syntax for retrieving the same diagnostic data, allowing execution of multiple commands and running the pattern search against any commands that succeed. | No |

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
- aruba

### Sample Usage

``` yaml

workflow:
  - step:
      metadata:
        name: "open_support_case"
        description: |
          "Failure is present or additional assistance is needed. Open support case and attach relevant show cmds."
      on_true:
        - echo: 
            args:
              message: |
                Opening support case.
        - open_case:
            args:
              title: "Line card failure on {{ inventory_hostname }}"
              description: |
                Line card failure identified. RMA may be needed.
                See workflow_log.txt attachment for troubleshooting steps that were performed.
              severity: "3"
              mode: active
              destinations:
                - internal
                - external
              attach_commands:
                - "show platform hardware authentication status"
                - "show diagnostic status"
                - "show environment status"
                - "show power detail"
                - "show power module"
                - "show power inline"
                - "show module"
                - "show diagnostic result module {{ module_id | default('') }} detail"
                - "show post"
                - "show platform"
                - "show logging onboard slot {{ module_id | default('') }} uptime"
                - "show logging onboard slot {{ module_id | default('') }} temperature"
                - "show platform software iomd {{ module_id | default('') }}/0 oir"
                - "show hw-module subslot  {{ module_id | default('') }}/0 oir internal"
                - "show idprom module  {{ module_id | default('') }}"
                - "request platform soft tracelog archive"

```
