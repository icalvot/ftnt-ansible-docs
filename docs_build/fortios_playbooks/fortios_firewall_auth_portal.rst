============================
fortios_firewall_auth_portal
============================


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
      - name: Configure firewall authentication portals.
        fortios_firewall_auth_portal:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          firewall_auth_portal:
            groups:
             -
                name: "default_name_4 (source user.group.name)"
            identity-based-route: "<your_own_value> (source firewall.identity-based-route.name)"
            portal-addr: "<your_own_value>"
            portal-addr6: "<your_own_value>"



Playbook File Examples
----------------------

%%PB_FILE_EXAMPLE_TOKEN%%

