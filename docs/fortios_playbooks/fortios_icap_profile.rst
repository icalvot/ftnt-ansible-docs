====================
fortios_icap_profile
====================


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
      - name: Configure ICAP profiles.
        fortios_icap_profile:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          https: "False"
          icap_profile:
            state: "present"
            methods: "delete"
            name: "default_name_4"
            replacemsg-group: "<your_own_value> (source system.replacemsg-group.name)"
            request: "disable"
            request-failure: "error"
            request-path: "<your_own_value>"
            request-server: "<your_own_value> (source icap.server.name)"
            response: "disable"
            response-failure: "error"
            response-path: "<your_own_value>"
            response-server: "<your_own_value> (source icap.server.name)"
            streaming-content-bypass: "disable"



Playbook File Examples
----------------------

%%PB_FILE_EXAMPLE_TOKEN%%

