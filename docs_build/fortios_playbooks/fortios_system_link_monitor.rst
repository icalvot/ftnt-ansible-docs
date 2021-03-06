===========================
fortios_system_link_monitor
===========================


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
      - name: Configure Link Health Monitor.
        fortios_system_link_monitor:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          system_link_monitor:
            state: "present"
            addr-mode: "ipv4"
            failtime: "4"
            gateway-ip: "<your_own_value>"
            gateway-ip6: "<your_own_value>"
            ha-priority: "7"
            http-get: "<your_own_value>"
            http-match: "<your_own_value>"
            interval: "10"
            name: "default_name_11"
            packet-size: "12"
            password: "<your_own_value>"
            port: "14"
            protocol: "ping"
            recoverytime: "16"
            security-mode: "none"
            server:
             -
                address: "<your_own_value>"
            source-ip: "84.230.14.43"
            source-ip6: "<your_own_value>"
            srcintf: "<your_own_value> (source system.interface.name)"
            status: "enable"
            update-cascade-interface: "enable"
            update-static-route: "enable"



Playbook File Examples
----------------------


../ansible_fgt_modules/v6.0.2/system/fortios_system_link_monitor_example.yml
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: yaml
            - hosts: localhost
      vars:
       host: "192.168.122.40"
       username: "admin"
       password: ""
       vdom: "root"
      tasks:
      - name: Configure Link Health Monitor.
        fortios_system_link_monitor:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          system_link_monitor:
            state: "present"
            addr-mode: "ipv4"
            failtime: "4"
            gateway-ip: "<your_own_value>"
            gateway-ip6: "<your_own_value>"
            ha-priority: "7"
            http-get: "<your_own_value>"
            http-match: "<your_own_value>"
            interval: "10"
            name: "default_name_11"
            packet-size: "12"
            password: "<your_own_value>"
            port: "14"
            protocol: "ping"
            recoverytime: "16"
            security-mode: "none"
            server:
             -
                address: "<your_own_value>"
            source-ip: "84.230.14.43"
            source-ip6: "<your_own_value>"
            srcintf: "<your_own_value> (source system.interface.name)"
            status: "enable"
            update-cascade-interface: "enable"
            update-static-route: "enable"




