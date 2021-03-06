========================================
fortios_endpoint_control_forticlient_ems
========================================


Playbook Task Examples
----------------------

.. code-block:: yaml

    - hosts: localhost
      vars:
       host: "192.168.122.40"
       username: "admin"
       password: ""
       vdom: "root"
      tasks:
      - name: Configure FortiClient Enterprise Management Server (EMS) entries.
        fortios_endpoint_control_forticlient_ems:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          endpoint_control_forticlient_ems:
            state: "present"
            address: "<your_own_value> (source firewall.address.name)"
            admin-password: "<your_own_value>"
            admin-type: "Windows"
            admin-username: "<your_own_value>"
            https-port: "7"
            listen-port: "8"
            name: "default_name_9"
            rest-api-auth: "disable"
            serial-number: "<your_own_value>"
            upload-port: "12"



Playbook File Examples
----------------------

%%PB_FILE_EXAMPLE_TOKEN%%

