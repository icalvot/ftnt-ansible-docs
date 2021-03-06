======================
fortios_firewall_vip64
======================


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
      - name: Configure IPv6 to IPv4 virtual IPs.
        fortios_firewall_vip64:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          firewall_vip64:
            state: "present"
            arp-reply: "disable"
            color: "4"
            comment: "Comment."
            extip: "<your_own_value>"
            extport: "<your_own_value>"
            id:  "8"
            ldb-method: "static"
            mappedip: "<your_own_value>"
            mappedport: "<your_own_value>"
            monitor:
             -
                name: "default_name_13 (source firewall.ldb-monitor.name)"
            name: "default_name_14"
            portforward: "disable"
            protocol: "tcp"
            realservers:
             -
                client-ip: "<your_own_value>"
                healthcheck: "disable"
                holddown-interval: "20"
                id:  "21"
                ip: "<your_own_value>"
                max-connections: "23"
                monitor: "<your_own_value> (source firewall.ldb-monitor.name)"
                port: "25"
                status: "active"
                weight: "27"
            server-type: "http"
            src-filter:
             -
                range: "<your_own_value>"
            type: "static-nat"
            uuid: "<your_own_value>"



Playbook File Examples
----------------------

%%PB_FILE_EXAMPLE_TOKEN%%

