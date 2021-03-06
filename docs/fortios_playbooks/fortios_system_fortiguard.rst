=========================
fortios_system_fortiguard
=========================


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
      - name: Configure FortiGuard services.
        fortios_system_fortiguard:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          system_fortiguard:
            antispam-cache: "enable"
            antispam-cache-mpercent: "4"
            antispam-cache-ttl: "5"
            antispam-expiration: "6"
            antispam-force-off: "enable"
            antispam-license: "8"
            antispam-timeout: "9"
            auto-join-forticloud: "enable"
            ddns-server-ip: "<your_own_value>"
            ddns-server-port: "12"
            load-balance-servers: "13"
            outbreak-prevention-cache: "enable"
            outbreak-prevention-cache-mpercent: "15"
            outbreak-prevention-cache-ttl: "16"
            outbreak-prevention-expiration: "17"
            outbreak-prevention-force-off: "enable"
            outbreak-prevention-license: "19"
            outbreak-prevention-timeout: "20"
            port: "53"
            sdns-server-ip: "<your_own_value>"
            sdns-server-port: "23"
            service-account-id: "<your_own_value>"
            source-ip: "84.230.14.43"
            source-ip6: "<your_own_value>"
            update-server-location: "usa"
            webfilter-cache: "enable"
            webfilter-cache-ttl: "29"
            webfilter-expiration: "30"
            webfilter-force-off: "enable"
            webfilter-license: "32"
            webfilter-timeout: "33"



Playbook File Examples
----------------------


../ansible_fgt_modules/v6.0.2/system/fortios_system_fortiguard_example.yml
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: yaml
            - hosts: localhost
      vars:
       host: "192.168.122.40"
       username: "admin"
       password: ""
       vdom: "root"
      tasks:
      - name: Configure FortiGuard services.
        fortios_system_fortiguard:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          system_fortiguard:
            antispam-cache: "enable"
            antispam-cache-mpercent: "4"
            antispam-cache-ttl: "5"
            antispam-expiration: "6"
            antispam-force-off: "enable"
            antispam-license: "8"
            antispam-timeout: "9"
            auto-join-forticloud: "enable"
            ddns-server-ip: "<your_own_value>"
            ddns-server-port: "12"
            load-balance-servers: "13"
            outbreak-prevention-cache: "enable"
            outbreak-prevention-cache-mpercent: "15"
            outbreak-prevention-cache-ttl: "16"
            outbreak-prevention-expiration: "17"
            outbreak-prevention-force-off: "enable"
            outbreak-prevention-license: "19"
            outbreak-prevention-timeout: "20"
            port: "53"
            sdns-server-ip: "<your_own_value>"
            sdns-server-port: "23"
            service-account-id: "<your_own_value>"
            source-ip: "84.230.14.43"
            source-ip6: "<your_own_value>"
            update-server-location: "usa"
            webfilter-cache: "enable"
            webfilter-cache-ttl: "29"
            webfilter-expiration: "30"
            webfilter-force-off: "enable"
            webfilter-license: "32"
            webfilter-timeout: "33"




