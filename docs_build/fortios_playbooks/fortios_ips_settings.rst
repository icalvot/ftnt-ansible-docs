====================
fortios_ips_settings
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
      - name: Configure IPS VDOM parameter.
        fortios_ips_settings:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          https: "False"
          ips_settings:
            ips-packet-quota: "3"
            packet-log-history: "4"
            packet-log-memory: "5"
            packet-log-post-attack: "6"



Playbook File Examples
----------------------

%%PB_FILE_EXAMPLE_TOKEN%%

