========================
fortios_router_auth_path
========================


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
      - name: Configure authentication based routing.
        fortios_router_auth_path:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          https: "False"
          router_auth_path:
            state: "present"
            device: "<your_own_value> (source system.interface.name)"
            gateway: "<your_own_value>"
            name: "default_name_5"



Playbook File Examples
----------------------

%%PB_FILE_EXAMPLE_TOKEN%%

