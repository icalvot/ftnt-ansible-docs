=================================
fortios_application_rule_settings
=================================


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
      - name: Configure application rule settings.
        fortios_application_rule_settings:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          application_rule_settings:
            state: "present"
            id:  "3"



Playbook File Examples
----------------------

%%PB_FILE_EXAMPLE_TOKEN%%

