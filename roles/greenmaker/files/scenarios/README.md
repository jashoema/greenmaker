# Scenarios

This folder contains scenario definitions that can be invoked by Greenmaker.  If you wish to create a new scenario definition for use, it must be added to this folder.  

## Scenario Definitions
A scenario definition is a YAML file that provides metadata (documentation) about a specific failure scenario, trigger conditions for the failure scenario, the auto-remediation workflow (ordered list of steps) which invokes pre-defined actions to validate and remediate the potential failure event, and a list of tests that can be performed to verify the workflow.

A scenario definition has the following sections:

* metadata
* triggers
* workflow
* tests
* library

## Sample Scenario Walkthrough

### Flow Map

The following diagram explains the logic for scenario definition [coming_soon.yml](coming_soon.yml), which will be referenced in the documentation and examples below.

![coming_soon.yml Flow Map](../../docs/images/coming_soon.png)

### metadata

The metadata section of a scenario definition provides documentation associated with the scenario.  This documentation is intended to provide human-readable information that can be used to describe the nature of the network failure and what actions should be taken to troubleshoot and remediate the network failure.

#### Supported fields:

TODO: Document supported fields for metadata

#### Example:

``` yaml

Coming Soon

```

### triggers

The triggers sectins of a scenario definition provides details about the network events that are associated with this scenario, such as syslog events that indicate the presence of a network failure for which this scenario provides troubleshooting and remediation actions.  The triggers section can be used to automate the generation of alerts that identify the presence of these triggers in the network, and it specifies relevant alert information such as the regex pattern needed for capturing a syslog event.

#### Supported fields:

TODO: Document supported fields for triggers

### Example:

``` yaml

Coming Soon

```

### workflow

The workflow is a programmatic representation of the steps and actions that should be taken to validate and remediate the network failure event(s) associated with this scenario.   

#### Example:

``` yaml

Coming Soon

```

#### Workflows Steps (`step`)

##### Actions

TODO: Explain the anatomy of an action

**custom_fields** - Custom fields can be specified under any action using the `custom_fields` key. The purpose of custom fields is to help support potential needs for custom post-processing of workflows by the alert pipeline or ticketing system *after* execution of the workflow has completed.  For example, when using the `open_case` action, an operator may choose to add the custom field that is needed for routing of the ticket to the proper service owners.  Below is an example of what this might look like.

``` yaml
open_case:
  custom_fields:
    service_owner: WAN_TEAM
```

##### Validation Actions (`validation`)

##### Remediation Actions (`on_true`/`on_false`)

TODO: Explain difference, returning values, etc.

### tests

#### Example:

``` yaml

Coming Soon   

```

#### Validation Tests

### library

TODO: Document library

## Scenario Schema

*NOTE: The following documentation is a work-in-progress; key information is missing*

The Scenario Schema is a JSON schema that defines available actions, action arguments, and all other components of the syntax of a Scenario Definition.  It can be used in VS Code editor or a CI/CD pipeline to automatically detect syntax errors in scenario definition.

We define a JSON schema to formalize the data structure of the scenario definition file. Even though  the name says "JSON Schema", it can be used for YAML files as well. 
See here for the reference doc for JSON schema: https://json-schema.org/understanding-json-schema/#

Our schema is defined in `greenmaker-scenario-schema.json` file. 

Schema file provides the following benefits:

-  Agreement on the data structure and basic validation.
-  Auto code generation to serialize/deserialize config files.
-  Editor support. Several free editors (including Visual Studio Code) provides 'code complete' and 'quick validation feedback' while editing schema based documents. See full list of editors here: https://json-schema.org/implementations.html#editors


## Schema validation with Visual Studio Code

- Install the extension "YAML" from "Red Hat"
- Point out schema for the TSG files.
  - Create a folder called `.vscode` in your workspace.
  - Create `settings.json` under that folder.
  - In `settings.json` file point to the schema file. The extension page has more documentation about this step. 
```
{
    "yaml.schemas": {
        "\\greenmaker_scenario-schema.json": ["sample_*.yml", "test_*.yml"]
    }    
}
```
