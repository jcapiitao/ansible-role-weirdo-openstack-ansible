ansible-role-weirdo-openstack-ansible
------------------------------------
This role provides an implementation of the
openstack-ansible_ gate jobs for
the WeIRDO_ project.

.. _openstack-ansible: https://github.com/openstack/openstack-ansible
.. _WeIRDO: https://github.com/redhat-openstack/weirdo


Role variables
~~~~~~~~~~~~~~

For default values, see `defaults/main.yml`_

* ``project``: Name of the project, analogous to the role name
* ``openstack_release``: Name of the OpenStack release to select which trunk repository to use by default
* ``version``: Version/tag/branch of openstack-ansible to clone
* ``manage_repos``: Whether openstack-ansible should manage repository setup
* ``repository``: URL to the openstack-ansible repository
* ``clone_path``: Path where openstack-ansible will be cloned
* ``delorean_url``: URL to the delorean repository .repo file.
* ``delorean_deps_url``: URL to the delorean-deps repository .repo file.
* ``copy_puppet_logs_url``: URL to the copy_puppet_logs.sh script for openstack-ansible log retrieval
* ``osa_workspace``: Path where openstack-ansible should believe the jenkins workspace is at
* ``required_packages``: Required packaged dependencies to install prior to running the tests

.. _defaults/main.yml: https://github.com/redhat-openstack/ansible-role-weirdo-openstack-ansible/blob/master/defaults/main.yml

Included tasks
~~~~~~~~~~~~~~

* ``repositories``: Ensures required repositories are setup
* ``packages``: Ensures required dependencies are installed
* ``setup``: Clones the openstack-ansible repository and prepares log retrieval
* ``logs``: Retrieves logs with the copy_puppet_logs.sh script
* ``run``: Runs the integration tests

Dependencies
~~~~~~~~~~~~

`ansible-role-weirdo-common`_ to be installed as ``common``

.. _ansible-role-weirdo-common: https://github.com/redhat-openstack/ansible-role-weirdo-common

Example playbook
~~~~~~~~~~~~~~~~

.. code-block:: yaml

    - name: Run openstack-ansible test
      hosts: openstack_nodes
      force_handlers: True
      roles:
        - { role: "openstack-ansible" }
