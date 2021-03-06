===============================
fortios_firewall.service_custom
===============================


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
      - name: Configure custom services.
        fortios_firewall.service_custom:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          firewall.service_custom:
            state: "present"
            app-category:
             -
                id:  "4"
            app-service-type: "disable"
            application:
             -
                id:  "7"
            category: "<your_own_value> (source firewall.service.category.name)"
            check-reset-range: "disable"
            color: "10"
            comment: "Comment."
            fqdn: "<your_own_value>"
            helper: "auto"
            icmpcode: "14"
            icmptype: "15"
            iprange: "<your_own_value>"
            name: "default_name_17"
            protocol: "TCP/UDP/SCTP"
            protocol-number: "19"
            proxy: "enable"
            sctp-portrange: "<your_own_value>"
            session-ttl: "22"
            tcp-halfclose-timer: "23"
            tcp-halfopen-timer: "24"
            tcp-portrange: "<your_own_value>"
            tcp-timewait-timer: "26"
            udp-idle-timer: "27"
            udp-portrange: "<your_own_value>"
            visibility: "enable"



Playbook File Examples
----------------------


../ansible_fgt_modules/v6.0.2/firewall.service/fortios_firewall.service_custom_example.yml
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: yaml
            - hosts: localhost
      vars:
       host: "192.168.122.40"
       username: "admin"
       password: ""
       vdom: "root"
      tasks:
      - name: Configure custom services.
        fortios_firewall.service_custom:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          firewall.service_custom:
            state: "present"
            app-category:
             -
                id:  "4"
            app-service-type: "disable"
            application:
             -
                id:  "7"
            category: "<your_own_value> (source firewall.service.category.name)"
            check-reset-range: "disable"
            color: "10"
            comment: "Comment."
            fqdn: "<your_own_value>"
            helper: "auto"
            icmpcode: "14"
            icmptype: "15"
            iprange: "<your_own_value>"
            name: "default_name_17"
            protocol: "TCP/UDP/SCTP"
            protocol-number: "19"
            proxy: "enable"
            sctp-portrange: "<your_own_value>"
            session-ttl: "22"
            tcp-halfclose-timer: "23"
            tcp-halfopen-timer: "24"
            tcp-portrange: "<your_own_value>"
            tcp-timewait-timer: "26"
            udp-idle-timer: "27"
            udp-portrange: "<your_own_value>"
            visibility: "enable"




