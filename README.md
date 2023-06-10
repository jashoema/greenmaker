# Greenmaker
Greenmaker is an Ansible role that consumes YAML-formatted action workflows to automate the diagnosis or remediation of network failure events.  The name "Greenmaker" is derived from this software's ability to **make network monitoring dashboards "green"** through auto-remediation of failure events.

If you'd like to learn more about Greenmaker, a complete overview of Greenmaker's architecture, supported features, and workflow language can be found here: [Greenmaker Ansible Role documentation](roles/greenmaker/README.md).

## Getting Started

These instructions will get you a copy of the Greenmaker project up and running on your local machine. See the deployment section below for notes on how to deploy the project on a live system.

### Prerequisites

Appropriate access privileges to install Python packages and associated dependencies.  The initial versions of Greenmaker has been tested on Ansible 2.9.10 for Python 2 and Python 3.  Testing will be expanded in the future to validate multiple permutations of Ansible and Python releases.

### Installing

1. Clone the Greenmaker repository to your local machine:

```bash
$ git clone https://wwwin-github.cisco.com/spa-ie/greenmaker.git
```

2. Run the `setup_greenmaker.sh` script. The script will create a Python virtualenv, source to it, then proceed to update the pip packaging tools. Next, the supported version of Ansible and other required dependencies are pip-installed. Finally, any required Collections from Ansible Galaxy will be installed.

```bashs
$ cd {git clone path}/greenmaker
$ ./setup_greenmaker.sh
```

TODO: Add Docker instructions

## Deployment

### Usage

The Greenmaker Role is not intended to be directly executed by an end-user. The Role is intended to be [executed and the results consumed](docs/README.md#production-execution-instructions) by a third-party service or network fault management system, typically invoked via an API call to AWX or Tower to execute the `greenmaker.yml` playbook. Extra_vars supplied to the playbook as part of this API call will be used to determine which automated workflow is executed and configurable parameters for the workflow. When the Ansible play finishes, the results are logged to the local filesystem and/or copied ot a configurable remote fileshare for further processing. Running the Greemaker Role from the CLI via the `ansible-playbook` command in [Test Mode](docs/README.md#test-instructions) is also supported.

## Support Information

### Training Materials

* TODO

### Support Contacts

* [Greenmaker Customer Support Mailer](mailto:greenmaker-support@cisco.com)
* [Web Innovation Edge Team](mailto:cisco-ie@cisco.com)

## Contributing
TODO
[Contribution guidelines for this project](./.github/CONTRIBUTING.rst)

## Project Administrators

* [Jason Shoemaker](mailto:jashoema@cisco.com)
* [Darren Powell](mailto:darrpowe@cisco.com)
* [Chitransh Pratyush](mailto:cpratyus@cisco.com)
* [Pablo Lencinas](mailto:plencina@cisco.com)

## License

This project is covered under the terms described in [LICENSE](./LICENSE)
