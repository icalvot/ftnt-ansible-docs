============================
fortios_webfilter_fortiguard
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
      - name: Configure FortiGuard Web Filter service.
        fortios_webfilter_fortiguard:
          host:  "{{  host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{  vdom }}"
          webfilter_fortiguard:
            cache-mem-percent: "3"
            cache-mode: "ttl"
            cache-prefix-match: "enable"
            close-ports: "enable"
            ovrd-auth-https: "enable"
            ovrd-auth-port: "8"
            ovrd-auth-port-http: "9"
            ovrd-auth-port-https: "10"
            ovrd-auth-port-warning: "11"
            request-packet-size-limit: "12"
            warn-auth-https: "enable"



Playbook File Examples
----------------------

%%PB_FILE_EXAMPLE_TOKEN%%

