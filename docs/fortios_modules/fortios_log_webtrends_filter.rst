============================
fortios_log_webtrends_filter
============================


Metadata
--------




**Name:** fortios_log_webtrends_filter

**Description:** This module is able to configure a FortiGate or FortiOS by allowing the user to set and modify log_webtrends feature and filter category. Examples include all parameters and values need to be adjusted to datasources before usage. Tested with FOS v6.0.2


**Author(s):** 

- Miguel Angel Munoz (github: @mamunozgonzalez)

- Nicolas Thomas (github: @thomnico)



**Ansible Version Added/Required:** 2.8

**Dev Status:** No status updates, yet. Contact Authors.

Parameters
----------

host
++++

- Description: FortiOS or FortiGate ip address.

  

- Required: True

https
+++++

- Description: Indicates if the requests towards FortiGate must use HTTPS protocol

  

- default: True

log_webtrends_filter
++++++++++++++++++++

- Description: Filters for WebTrends.

  

- default: None

password
++++++++

- Description: FortiOS or FortiGate password.

  

- default: 

username
++++++++

- Description: FortiOS or FortiGate username.

  

- Required: True

vdom
++++

- Description: Virtual domain, among those defined previously. A vdom is a virtual instance of the FortiGate that can be configured and used as a different unit.

  

- default: root




Functions
---------




- login

 .. code-block:: python

    def login(data, fos):
        host = data['host']
        username = data['username']
        password = data['password']
    
        fos.debug('on')
        if 'https' in data and not data['https']:
            fos.https('off')
        else:
            fos.https('on')
    
        fos.login(host, username, password)
    
    

- filter_log_webtrends_filter_data

 .. code-block:: python

    def filter_log_webtrends_filter_data(json):
        option_list = ['anomaly', 'dns', 'filter',
                       'filter-type', 'forward-traffic', 'gtp',
                       'local-traffic', 'multicast-traffic', 'netscan-discovery',
                       'netscan-vulnerability', 'severity', 'sniffer-traffic',
                       'ssh', 'voip']
        dictionary = {}
    
        for attribute in option_list:
            if attribute in json and json[attribute] is not None:
                dictionary[attribute] = json[attribute]
    
        return dictionary
    
    

- log_webtrends_filter

 .. code-block:: python

    def log_webtrends_filter(data, fos):
        vdom = data['vdom']
        log_webtrends_filter_data = data['log_webtrends_filter']
        filtered_data = filter_log_webtrends_filter_data(log_webtrends_filter_data)
    
        return fos.set('log.webtrends',
                       'filter',
                       data=filtered_data,
                       vdom=vdom)
    
    

- fortios_log_webtrends

 .. code-block:: python

    def fortios_log_webtrends(data, fos):
        login(data, fos)
    
        if data['log_webtrends_filter']:
            resp = log_webtrends_filter(data, fos)
    
        fos.logout()
        return not resp['status'] == "success", resp['status'] == "success", resp
    
    

- main

 .. code-block:: python

    def main():
        fields = {
            "host": {"required": True, "type": "str"},
            "username": {"required": True, "type": "str"},
            "password": {"required": False, "type": "str", "no_log": True},
            "vdom": {"required": False, "type": "str", "default": "root"},
            "https": {"required": False, "type": "bool", "default": True},
            "log_webtrends_filter": {
                "required": False, "type": "dict",
                "options": {
                    "anomaly": {"required": False, "type": "str",
                                "choices": ["enable", "disable"]},
                    "dns": {"required": False, "type": "str",
                            "choices": ["enable", "disable"]},
                    "filter": {"required": False, "type": "str"},
                    "filter-type": {"required": False, "type": "str",
                                    "choices": ["include", "exclude"]},
                    "forward-traffic": {"required": False, "type": "str",
                                        "choices": ["enable", "disable"]},
                    "gtp": {"required": False, "type": "str",
                            "choices": ["enable", "disable"]},
                    "local-traffic": {"required": False, "type": "str",
                                      "choices": ["enable", "disable"]},
                    "multicast-traffic": {"required": False, "type": "str",
                                          "choices": ["enable", "disable"]},
                    "netscan-discovery": {"required": False, "type": "str"},
                    "netscan-vulnerability": {"required": False, "type": "str"},
                    "severity": {"required": False, "type": "str",
                                 "choices": ["emergency", "alert", "critical",
                                             "error", "warning", "notification",
                                             "information", "debug"]},
                    "sniffer-traffic": {"required": False, "type": "str",
                                        "choices": ["enable", "disable"]},
                    "ssh": {"required": False, "type": "str",
                            "choices": ["enable", "disable"]},
                    "voip": {"required": False, "type": "str",
                             "choices": ["enable", "disable"]}
    
                }
            }
        }
    
        module = AnsibleModule(argument_spec=fields,
                               supports_check_mode=False)
        try:
            from fortiosapi import FortiOSAPI
        except ImportError:
            module.fail_json(msg="fortiosapi module is required")
    
        fos = FortiOSAPI()
    
        is_error, has_changed, result = fortios_log_webtrends(module.params, fos)
    
        if not is_error:
            module.exit_json(changed=has_changed, meta=result)
        else:
            module.fail_json(msg="Error in repo", meta=result)
    
    



Module Source Code
------------------

.. code-block:: python

    #!/usr/bin/python
    from __future__ import (absolute_import, division, print_function)
    # Copyright 2019 Fortinet, Inc.
    #
    # This program is free software: you can redistribute it and/or modify
    # it under the terms of the GNU General Public License as published by
    # the Free Software Foundation, either version 3 of the License, or
    # (at your option) any later version.
    #
    # This program is distributed in the hope that it will be useful,
    # but WITHOUT ANY WARRANTY; without even the implied warranty of
    # MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    # GNU General Public License for more details.
    #
    # You should have received a copy of the GNU General Public License
    # along with this program.  If not, see <https://www.gnu.org/licenses/>.
    
    __metaclass__ = type
    
    ANSIBLE_METADATA = {'status': ['preview'],
                        'supported_by': 'community',
                        'metadata_version': '1.1'}
    
    DOCUMENTATION = '''
    ---
    module: fortios_log_webtrends_filter
    short_description: Filters for WebTrends in Fortinet's FortiOS and FortiGate.
    description:
        - This module is able to configure a FortiGate or FortiOS by allowing the
          user to set and modify log_webtrends feature and filter category.
          Examples include all parameters and values need to be adjusted to datasources before usage.
          Tested with FOS v6.0.2
    version_added: "2.8"
    author:
        - Miguel Angel Munoz (@mamunozgonzalez)
        - Nicolas Thomas (@thomnico)
    notes:
        - Requires fortiosapi library developed by Fortinet
        - Run as a local_action in your playbook
    requirements:
        - fortiosapi>=0.9.8
    options:
        host:
           description:
                - FortiOS or FortiGate ip address.
           required: true
        username:
            description:
                - FortiOS or FortiGate username.
            required: true
        password:
            description:
                - FortiOS or FortiGate password.
            default: ""
        vdom:
            description:
                - Virtual domain, among those defined previously. A vdom is a
                  virtual instance of the FortiGate that can be configured and
                  used as a different unit.
            default: root
        https:
            description:
                - Indicates if the requests towards FortiGate must use HTTPS
                  protocol
            type: bool
            default: true
        log_webtrends_filter:
            description:
                - Filters for WebTrends.
            default: null
            suboptions:
                anomaly:
                    description:
                        - Enable/disable anomaly logging.
                    choices:
                        - enable
                        - disable
                dns:
                    description:
                        - Enable/disable detailed DNS event logging.
                    choices:
                        - enable
                        - disable
                filter:
                    description:
                        - Webtrends log filter.
                filter-type:
                    description:
                        - Include/exclude logs that match the filter.
                    choices:
                        - include
                        - exclude
                forward-traffic:
                    description:
                        - Enable/disable forward traffic logging.
                    choices:
                        - enable
                        - disable
                gtp:
                    description:
                        - Enable/disable GTP messages logging.
                    choices:
                        - enable
                        - disable
                local-traffic:
                    description:
                        - Enable/disable local in or out traffic logging.
                    choices:
                        - enable
                        - disable
                multicast-traffic:
                    description:
                        - Enable/disable multicast traffic logging.
                    choices:
                        - enable
                        - disable
                netscan-discovery:
                    description:
                        - Enable/disable netscan discovery event logging.
                netscan-vulnerability:
                    description:
                        - Enable/disable netscan vulnerability event logging.
                severity:
                    description:
                        - Lowest severity level to log to WebTrends.
                    choices:
                        - emergency
                        - alert
                        - critical
                        - error
                        - warning
                        - notification
                        - information
                        - debug
                sniffer-traffic:
                    description:
                        - Enable/disable sniffer traffic logging.
                    choices:
                        - enable
                        - disable
                ssh:
                    description:
                        - Enable/disable SSH logging.
                    choices:
                        - enable
                        - disable
                voip:
                    description:
                        - Enable/disable VoIP logging.
                    choices:
                        - enable
                        - disable
    '''
    
    EXAMPLES = '''
    - hosts: localhost
      vars:
       host: "192.168.122.40"
       username: "admin"
       password: ""
       vdom: "root"
      tasks:
      - name: Filters for WebTrends.
        fortios_log_webtrends_filter:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          https: "False"
          log_webtrends_filter:
            anomaly: "enable"
            dns: "enable"
            filter: "<your_own_value>"
            filter-type: "include"
            forward-traffic: "enable"
            gtp: "enable"
            local-traffic: "enable"
            multicast-traffic: "enable"
            netscan-discovery: "<your_own_value>"
            netscan-vulnerability: "<your_own_value>"
            severity: "emergency"
            sniffer-traffic: "enable"
            ssh: "enable"
            voip: "enable"
    '''
    
    RETURN = '''
    build:
      description: Build number of the fortigate image
      returned: always
      type: str
      sample: '1547'
    http_method:
      description: Last method used to provision the content into FortiGate
      returned: always
      type: str
      sample: 'PUT'
    http_status:
      description: Last result given by FortiGate on last operation applied
      returned: always
      type: str
      sample: "200"
    mkey:
      description: Master key (id) used in the last call to FortiGate
      returned: success
      type: str
      sample: "id"
    name:
      description: Name of the table used to fulfill the request
      returned: always
      type: str
      sample: "urlfilter"
    path:
      description: Path of the table used to fulfill the request
      returned: always
      type: str
      sample: "webfilter"
    revision:
      description: Internal revision number
      returned: always
      type: str
      sample: "17.0.2.10658"
    serial:
      description: Serial number of the unit
      returned: always
      type: str
      sample: "FGVMEVYYQT3AB5352"
    status:
      description: Indication of the operation's result
      returned: always
      type: str
      sample: "success"
    vdom:
      description: Virtual domain used
      returned: always
      type: str
      sample: "root"
    version:
      description: Version of the FortiGate
      returned: always
      type: str
      sample: "v5.6.3"
    
    '''
    
    from ansible.module_utils.basic import AnsibleModule
    
    
    def login(data, fos):
        host = data['host']
        username = data['username']
        password = data['password']
    
        fos.debug('on')
        if 'https' in data and not data['https']:
            fos.https('off')
        else:
            fos.https('on')
    
        fos.login(host, username, password)
    
    
    def filter_log_webtrends_filter_data(json):
        option_list = ['anomaly', 'dns', 'filter',
                       'filter-type', 'forward-traffic', 'gtp',
                       'local-traffic', 'multicast-traffic', 'netscan-discovery',
                       'netscan-vulnerability', 'severity', 'sniffer-traffic',
                       'ssh', 'voip']
        dictionary = {}
    
        for attribute in option_list:
            if attribute in json and json[attribute] is not None:
                dictionary[attribute] = json[attribute]
    
        return dictionary
    
    
    def log_webtrends_filter(data, fos):
        vdom = data['vdom']
        log_webtrends_filter_data = data['log_webtrends_filter']
        filtered_data = filter_log_webtrends_filter_data(log_webtrends_filter_data)
    
        return fos.set('log.webtrends',
                       'filter',
                       data=filtered_data,
                       vdom=vdom)
    
    
    def fortios_log_webtrends(data, fos):
        login(data, fos)
    
        if data['log_webtrends_filter']:
            resp = log_webtrends_filter(data, fos)
    
        fos.logout()
        return not resp['status'] == "success", resp['status'] == "success", resp
    
    
    def main():
        fields = {
            "host": {"required": True, "type": "str"},
            "username": {"required": True, "type": "str"},
            "password": {"required": False, "type": "str", "no_log": True},
            "vdom": {"required": False, "type": "str", "default": "root"},
            "https": {"required": False, "type": "bool", "default": True},
            "log_webtrends_filter": {
                "required": False, "type": "dict",
                "options": {
                    "anomaly": {"required": False, "type": "str",
                                "choices": ["enable", "disable"]},
                    "dns": {"required": False, "type": "str",
                            "choices": ["enable", "disable"]},
                    "filter": {"required": False, "type": "str"},
                    "filter-type": {"required": False, "type": "str",
                                    "choices": ["include", "exclude"]},
                    "forward-traffic": {"required": False, "type": "str",
                                        "choices": ["enable", "disable"]},
                    "gtp": {"required": False, "type": "str",
                            "choices": ["enable", "disable"]},
                    "local-traffic": {"required": False, "type": "str",
                                      "choices": ["enable", "disable"]},
                    "multicast-traffic": {"required": False, "type": "str",
                                          "choices": ["enable", "disable"]},
                    "netscan-discovery": {"required": False, "type": "str"},
                    "netscan-vulnerability": {"required": False, "type": "str"},
                    "severity": {"required": False, "type": "str",
                                 "choices": ["emergency", "alert", "critical",
                                             "error", "warning", "notification",
                                             "information", "debug"]},
                    "sniffer-traffic": {"required": False, "type": "str",
                                        "choices": ["enable", "disable"]},
                    "ssh": {"required": False, "type": "str",
                            "choices": ["enable", "disable"]},
                    "voip": {"required": False, "type": "str",
                             "choices": ["enable", "disable"]}
    
                }
            }
        }
    
        module = AnsibleModule(argument_spec=fields,
                               supports_check_mode=False)
        try:
            from fortiosapi import FortiOSAPI
        except ImportError:
            module.fail_json(msg="fortiosapi module is required")
    
        fos = FortiOSAPI()
    
        is_error, has_changed, result = fortios_log_webtrends(module.params, fos)
    
        if not is_error:
            module.exit_json(changed=has_changed, meta=result)
        else:
            module.fail_json(msg="Error in repo", meta=result)
    
    
    if __name__ == '__main__':
        main()


