EC2 API Tools (Java)
====================

Install and configure AWS ec2-api-tools on a target node. This does not use the newer (recommended) python package `awscli` as this was purpose built for use cases that still use the java tools (eg: [Bamboo Elastic Agent](https://confluence.atlassian.com/bamboo/creating-a-custom-elastic-image-289277146.html)).

Requirements
------------

Using this role does not require any explicit requirements other than Ansible itself.

Role Variables
--------------

The following variables can be set to alter execution behaviour.
1. `ec2_api_tools_url`: Set this if you want to use a custom installation source.
2. `ec2_api_tools_dir`: Set this to alter the installation directory.
3. `ec2_api_tools_refresh`: Set this to `yes` if you'd like to force a re-install if a previous installation exists. This is checked for by testing if `ec2_api_tools_dir` exists, and if set will remove all installations of the tool before installing again.

Dependencies
------------

This role itself does not have any external dependencies. However, if you are executing tests, it will require the galaxy role [abn.managed-node-bootstrap](https://galaxy.ansible.com/abn/managed-node-bootstrap) to be installed.

Example Playbook
----------------

A sample playbook that refreshes any existing installations.

    - hosts: all
      roles:
         - { role: abn.ec2-api-tools-java, ec2_api_tools_refresh: yes }

Testing
-------
Before testing, you need to ensure that the submodules required have been cloned.
```sh
git submodule update --init --recursive
```

### Local Environment
This role uses [Molecule](https://molecule.readthedocs.io/en/latest/) and docker instances to enable testing. You can run this locally on your development environment provided you have python installed and are running the docker daemon.

```sh
# install molecule and docker-py requirements
pip install -r test-requirements.txt
molecule test
```

This will as configured in the default molecule scenario, spin up containers of the supported distributions and execute a sample playbook.

### Tox
This project also has [tox](http://tox.readthedocs.io/en/latest/) configured to run against multiple ansible versions with [Molecule](https://molecule.readthedocs.io/en/latest/). This can simply be run using tox.

```sh
tox
```

Refer to the [Molecule documentation](https://molecule.readthedocs.io/en/latest/testing.html) and [tox documentation](http://tox.readthedocs.io/en/latest/) for advance usage instructions.

License
-------

Apache License 2.0
