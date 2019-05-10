###############
Getting Started
###############
This guide will assist in the initial configuration of Ansible
to work with FortiManager modules, and more specifically the plugin.



Introduction
============

Beginning in Q1 of 2019 all up-to-date FortiManager modules now utilize a connection-plugin.
Existing installations must convert going forward.

- This requires modification to existing playbooks and inventory files that used the previous "connection: local" versions of FortiManager Plugins.

  - Follow the upgrade path defined below to utilize the new plugin.

- All updated modules, module_utils, and plugin will be included in Ansible 2.8 when it is released.

  - Ansible 2.8 is expected 05-16-2019: https://docs.ansible.com/ansible/devel/roadmap/ROADMAP_2_8.html
  - Until then, ansible components must be manually installed. Instructions are below.


Pre-Requisites
==============

- Minimum Ansible Version: 2.7+
- Minimum Python Version: 2.7+

  - Works with Python 3.x

- Minimum FortiManager Version: 6.0+
- FortiManager account with rpc read/write enabled via CLI
- A licensed FortiManager appliance or VM.


Fresh Installation
=============================

Step 1 - Auto Installation Method
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
After about 05-16-2019, the most recent versions of FortiManager ansible components
will be available from a simple software package manager update or install of Ansible.

- Ansible Installation Guide: https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

After install, run the following command:

.. code-block:: shell

   ansible --version

If the version is below 2.8, proceed to step 2.

If the version is 2.8+, skip to step 3.


Step 2 (Optional) - Manual Installation Method
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Summary
"""""""

- Until about 05-16-2019, the most recent versions of FortiManager ansible components
  must be manually installed to an existing Ansible 2.7+ installation.

- Fortinet may make updates to Ansible components in-between Ansible release dates, and they can be installed
  in-between Ansible release schedules, manually.

- These most-recent versions are located on the official FNDN github repo here:
  https://github.com/ftntcorecse/fndn_ansible

Steps
"""""

- First, make sure Ansible is already installed, and shows version 2.7+.

- The plugin and module_utils need to be copied to their correct locations. On Ubuntu running Python 2.7, the paths are:

.. code-block:: shell

   /usr/lib/python2.7/dist-packages/ansible/plugins/httpapi/
   /usr/lib/python2.7/dist-packages/ansible/module_utils/network/fortimanager/

- If you're unsure where to find this path on your own system, run this command:

.. code-block:: shell

    find /usr -name "ansible"

- ... and the path under a python dist-packages should present itself.

- The modules can be copied to any directory such as /usr/ansible_modules,
  as long as the library = <folder_path> line in /etc/ansible/ansible.cfg is edited to include that path.

- For other custom module path methods, see this guide:
  https://docs.ansible.com/ansible/latest/dev_guide/developing_locally.html#adding-a-module-locally

Step 3 - Inventory File
^^^^^^^^^^^^^^^^^^^^^^^
The following variables must be added to the hosts file entries that correspond to the FortiManager hosts:

- ansible_host=<ip/host>

  - Which FortiManager to connect to.
- ansible_network_os=fortimanager

  - Tells Ansible which httpapi plugin to search for

- ansible_user=<fmgr_username>
- ansible_password=<fmgr_password>
- ansible_become=no
- ansible_become_method=disable
- ansible_httpapi_use_ssl=true
- ansible_httpapi_validate_certs=false

  - Switch to True if using in production!
- ansible_httpapi_timeout=300

  - Sometimes it takes a while for FortiManager to process large requests or scripts. A large timeout is preferred.
  - In seconds.

These parameters can be added on the same line, or nested as shown in the code block below:


.. code-block:: shell

    [FortiManager]
    10.7.220.35 ansible_host=10.7.220.35

    [FortiManagerHA]
    10.7.220.36 ansible_host=10.7.220.36

    [fmgr_api:children]
    FortiManager
    FortiManagerHA

    [fmgr_api:vars]
    ansible_network_os=fortimanager
    ansible_user=ansible
    ansible_password=fortinet
    ansible_become=no
    ansible_become_method=disable
    ansible_httpapi_use_ssl=true
    ansible_httpapi_validate_certs=false
    ansible_httpapi_timeout=300


Step 4 - Playbook Test
^^^^^^^^^^^^^^^^^^^^^^^^^^^^
Ansible should be ready to test now. Copy the following code block into a file named "test_fmgr.yml":

.. code-block:: yaml

    ---
    - name: FMGR CONNECTION GET SYS STATUS
      hosts: FortiManager
      connection: httpapi
      gather_facts: False

      tasks:
      - name: TEST FMGR CONNECTION GET SYS STATUS
        fmgr_query:
          adom: "root"
          object: "custom"
          custom_endpoint: "/sys/status"

... and then run it with the following command:

.. code-block:: shell

  ansible-playbook test_fmgr.yml -vvvv

If successful, it should report OK with Green Text and show various information about the target FortiManager.

If not successful, double check the hosts file, username/password combo, and that RPC read/write has been enabled for the FortiManager user.
The -vvvv verbose mode should indicate where the issue lies.



Upgrade to Connection Plugin
=============================
Because all new modules are converted to use the connection plugin,
the old method of using pyFMG and connection:local in playbooks is deprecated.

All playbooks must be converted to use the new plugin, and a few additions to the inventory file are required.


Step 1 - Inventory File
^^^^^^^^^^^^^^^^^^^^^^^
The following variables must be added to the hosts file entries that correspond to the FortiManager hosts:

- ansible_host=<ip/host>

  - Which FortiManager to connect to.
- ansible_network_os=fortimanager

  - Tells Ansible which httpapi plugin to search for

- ansible_user=<fmgr_username>
- ansible_password=<fmgr_password>
- ansible_become=no
- ansible_become_method=disable
- ansible_httpapi_use_ssl=true
- ansible_httpapi_validate_certs=false

  - Switch to True if using in production!
- ansible_httpapi_timeout=300

  - Sometimes it takes a while for FortiManager to process large requests or scripts. A large timeout is preferred.
  - In seconds.

These parameters can be added on the same line, or nested as shown in the code block below:


.. code-block:: shell

    [FortiManager]
    10.7.220.35 ansible_host=10.7.220.35

    [FortiManagerHA]
    10.7.220.36 ansible_host=10.7.220.36

    [fmgr_api:children]
    FortiManager
    FortiManagerHA

    [fmgr_api:vars]
    ansible_network_os=fortimanager
    ansible_user=ansible
    ansible_password=fortinet
    ansible_become=no
    ansible_become_method=disable
    ansible_httpapi_use_ssl=true
    ansible_httpapi_validate_certs=false
    ansible_httpapi_timeout=300

Because the host, username, and password have all been added to
the connection/host level they must be removed from playbooks.

Step 2 - Playbook Conversion
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Previous playbooks might look like this:

.. code-block:: yaml

    ---
    - name: CONFIG FGT HOSTNAME AND INTERFACE
      hosts: FortiManager
      connection: local
      gather_facts: False

      tasks:

      - name: CHANGE HOSTNAME
        fmgr_device_config:
          host: "{{ inventory_hostname }}"
          username: "{{ username }}"
          password: "{{ password }}"
          device_hostname: "ansible-fgt01"
          device_unique_name: "FGT1"
          adom: "ansible"

- The host, username, and password lines from each task need to be deleted.
- The heading attribute "connection: local" must be changed to "connection: httpapi"

Converted version of the above playbook:

.. code-block:: yaml

    ---
    - name: CONFIG FGT HOSTNAME AND INTERFACE
      hosts: FortiManager
      connection: httpapi
      gather_facts: False

      tasks:

      - name: CHANGE HOSTNAME
        fmgr_device_config:
          device_hostname: "ansible-fgt01"
          device_unique_name: "FGT1"
          adom: "ansible"

Step 3a - Auto Installation Method
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
After about 05-16-2019, the most recent versions of FortiManager ansible components
will be available from a simple software package manager update or install of Ansible.

- Ansible Installation Guide: https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html


Step 2 (Optional) - Manual Installation Method
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Summary
"""""""

- Until about 05-16-2019, the most recent versions of FortiManager ansible components
  must be manually installed to an existing Ansible 2.7+ installation.

- Fortinet may make updates to Ansible components in-between Ansible release dates, and they can be installed
  in-between Ansible release schedules, manually.

- These most-recent versions are located on the official FNDN github repo here:
  https://github.com/ftntcorecse/fndn_ansible

Steps
"""""

- First, make sure Ansible is already installed, and shows version 2.7+.

- The plugin and module_utils need to be copied to their correct locations. On Ubuntu running Python 2.7, the paths are:

.. code-block:: shell

  /usr/lib/python2.7/dist-packages/ansible/plugins/httpapi/
  /usr/lib/python2.7/dist-packages/ansible/module_utils/network/fortimanager/

- If you're unsure where to find this path on your own system, run this command:

.. code-block:: shell

    find /usr -name "ansible"

    - ... and the path under a python dist-packages should present itself.

- The modules can be copied to any directory such as /usr/ansible_modules,
  as long as the library = <folder_path> line in /etc/ansible/ansible.cfg is edited to include that path.

- For other custom module path methods, see this guide:
  https://docs.ansible.com/ansible/latest/dev_guide/developing_locally.html#adding-a-module-locally

Step 4 - Playbook Test
^^^^^^^^^^^^^^^^^^^^^^
After modifying the hosts inventory file, and either manually or automatically installing the latest FortiManager Ansible components,
the converted playbooks from Step 2 should now run.

For a sample status check, copy the following code block into a file named "test_fmgr.yml":

.. code-block:: yaml

    ---
    - name: FMGR CONNECTION GET SYS STATUS
      hosts: FortiManager
      connection: httpapi
      gather_facts: False

      tasks:
      - name: TEST FMGR CONNECTION GET SYS STATUS
        fmgr_query:
          adom: "root"
          object: "custom"
          custom_endpoint: "/sys/status"

... and then run it with the following command:

.. code-block:: shell

   ansible-playbook test_fmgr.yml -vvvv

If successful, it should report OK with Green Text and show various information about the target FortiManager.

If not successful, double check the hosts file, username/password combo, and that RPC read/write has been enabled for the FortiManager user.
The -vvvv verbose mode should indicate where the issue lies.



Appendix
========

Enabling FortiManager user for RPC Read/Write via FMGR CLI
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
.. code-block:: shell

    config system admin user
      edit <username>
      set rpc read-write
      next
    end



