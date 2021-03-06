=========================
fortios_firewall_address6
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
      - name: Configure IPv6 firewall addresses.
        fortios_firewall_address6:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          firewall_address6:
            state: "present"
            cache-ttl: "3"
            color: "4"
            comment: "Comment."
            end-ip: "<your_own_value>"
            fqdn: "<your_own_value>"
            host: "<your_own_value>"
            host-type: "any"
            ip6: "<your_own_value>"
            list:
             -
                ip: "<your_own_value>"
            name: "default_name_13"
            obj-id: "<your_own_value>"
            sdn: "nsx"
            start-ip: "<your_own_value>"
            subnet-segment:
             -
                name: "default_name_18"
                type: "any"
                value: "<your_own_value>"
            tagging:
             -
                category: "<your_own_value> (source system.object-tagging.category)"
                name: "default_name_23"
                tags:
                 -
                    name: "default_name_25 (source system.object-tagging.tags.name)"
            template: "<your_own_value> (source firewall.address6-template.name)"
            type: "ipprefix"
            uuid: "<your_own_value>"
            visibility: "enable"



Playbook File Examples
----------------------

%%PB_FILE_EXAMPLE_TOKEN%%

