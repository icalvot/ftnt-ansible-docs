============================
fortios_log.syslogd4_setting
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
      - name: Global settings for remote syslog server.
        fortios_log.syslogd4_setting:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          log.syslogd4_setting:
            certificate: "<your_own_value> (source certificate.local.name)"
            custom-field-name:
             -
                custom: "<your_own_value>"
                id:  "6"
                name: "default_name_7"
            enc-algorithm: "high-medium"
            facility: "kernel"
            format: "default"
            mode: "udp"
            port: "12"
            server: "192.168.100.40"
            source-ip: "84.230.14.43"
            status: "enable"



Playbook File Examples
----------------------


../ansible_fgt_modules/v6.0.2/log.syslogd4/fortios_log.syslogd4_setting_example.yml
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

.. code-block:: yaml
            - hosts: localhost
      vars:
       host: "192.168.122.40"
       username: "admin"
       password: ""
       vdom: "root"
      tasks:
      - name: Global settings for remote syslog server.
        fortios_log.syslogd4_setting:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          log.syslogd4_setting:
            certificate: "<your_own_value> (source certificate.local.name)"
            custom-field-name:
             -
                custom: "<your_own_value>"
                id:  "6"
                name: "default_name_7"
            enc-algorithm: "high-medium"
            facility: "kernel"
            format: "default"
            mode: "udp"
            port: "12"
            server: "192.168.100.40"
            source-ip: "84.230.14.43"
            status: "enable"




