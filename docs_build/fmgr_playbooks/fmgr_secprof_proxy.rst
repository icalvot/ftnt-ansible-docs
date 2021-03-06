==================
fmgr_secprof_proxy
==================


Playbook Task Examples
----------------------

.. code-block:: yaml

      - name: DELETE Profile
        fmgr_secprof_proxy:
          name: "Ansible_Web_Proxy_Profile"
          mode: "delete"
    
      - name: CREATE Profile
        fmgr_secprof_proxy:
          name: "Ansible_Web_Proxy_Profile"
          mode: "set"
          header_client_ip: "pass"
          header_front_end_https: "add"
          header_via_request: "remove"
          header_via_response: "pass"
          header_x_authenticated_groups: "add"
          header_x_authenticated_user: "remove"
          strip_encoding: "enable"
          log_header_change: "enable"
          header_x_forwarded_for: "pass"
          headers_action: "add-to-request"
          headers_content: "test"
          headers_name: "test_header"



Playbook File Examples
----------------------


proxy.yml
+++++++++

.. code-block:: yaml



    - name: Create and Delete security profile in FMG
      hosts: FortiManager
      connection: httpapi
      gather_facts: False
    
      tasks:
    
      - name: DELETE Profile
        fmgr_secprof_proxy:
          name: "Ansible_Web_Proxy_Profile"
          mode: "delete"
    
      - name: CREATE Profile
        fmgr_secprof_proxy:
          name: "Ansible_Web_Proxy_Profile"
          mode: "set"
          header_client_ip: "pass"
          header_front_end_https: "add"
          header_via_request: "remove"
          header_via_response: "pass"
          header_x_authenticated_groups: "add"
          header_x_authenticated_user: "remove"
          strip_encoding: "enable"
          log_header_change: "enable"
          header_x_forwarded_for: "pass"
          headers_action: "add-to-request"
          headers_content: "test"
          headers_name: "test_header"

fmgr_secprof_proxy_run_all.sh
+++++++++++++++++++++++++++++

.. code-block:: shell

            #!/bin/bash
    ansible-playbook proxy.yml -vvvv




