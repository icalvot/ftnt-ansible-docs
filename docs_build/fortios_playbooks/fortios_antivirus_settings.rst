==========================
fortios_antivirus_settings
==========================


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
      - name: Configure AntiVirus settings.
        fortios_antivirus_settings:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          antivirus_settings:
            default-db: "normal"
            grayware: "enable"
            override-timeout: "5"



Playbook File Examples
----------------------

%%PB_FILE_EXAMPLE_TOKEN%%

