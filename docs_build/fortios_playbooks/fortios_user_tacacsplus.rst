=======================
fortios_user_tacacsplus
=======================


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
      - name: Configure TACACS+ server entries.
        fortios_user_tacacsplus:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          https: "False"
          user_tacacsplus:
            state: "present"
            authen-type: "mschap"
            authorization: "enable"
            key: "<your_own_value>"
            name: "default_name_6"
            port: "7"
            secondary-key: "<your_own_value>"
            secondary-server: "<your_own_value>"
            server: "192.168.100.40"
            source-ip: "84.230.14.43"
            tertiary-key: "<your_own_value>"
            tertiary-server: "<your_own_value>"



Playbook File Examples
----------------------

%%PB_FILE_EXAMPLE_TOKEN%%

