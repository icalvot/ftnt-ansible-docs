===========================
fortios_vpn.ipsec_manualkey
===========================


Metadata
--------




**Name:** fortios_vpn.ipsec_manualkey

**Description:** This module is able to configure a FortiGate or FortiOS by allowing the user to configure vpn.ipsec feature and manualkey category. Examples includes all options and need to be adjusted to datasources before usage. Tested with FOS v6.0.2


**Author(s):** 

- Miguel Angel Munoz (github: @mamunozgonzalez)

- Nicolas Thomas (github: @thomnico)



**Ansible Version Added/Required:** 2.8

**Dev Status:** No Data Exists. Contact DevOps Team.

Parameters
----------

host
++++

- Description: FortiOS or FortiGate ip adress.

  

- Required: True

https
+++++

- Description: Indicates if the requests towards FortiGate must use HTTPS protocol

  

- default: False

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

vpn.ipsec_manualkey
+++++++++++++++++++

- Description: Configure IPsec manual keys.

  

- default: None




Functions
---------




- login

 .. code-block:: python

    def login(data):
        host = data['host']
        username = data['username']
        password = data['password']
    
        fos.debug('on')
        if 'https' in data and not data['https']:
            fos.https('off')
        else:
            fos.https('on')
    
        fos.login(host, username, password)
    
    

- filter_vpn.ipsec_manualkey_data

 .. code-block:: python

    def filter_vpn.ipsec_manualkey_data(json):
        option_list = ['authentication', 'authkey', 'enckey',
                       'encryption', 'interface', 'local-gw',
                       'localspi', 'name', 'npu-offload',
                       'remote-gw', 'remotespi']
        dictionary = {}
    
        for attribute in option_list:
            if attribute in json and json[attribute] is not None:
                dictionary[attribute] = json[attribute]
    
        return dictionary
    
    

- vpn.ipsec_manualkey

 .. code-block:: python

    def vpn.ipsec_manualkey(data, fos):
        vdom = data['vdom']
        vpn.ipsec_manualkey_data = data['vpn.ipsec_manualkey']
        filtered_data = filter_vpn.ipsec_manualkey_data(vpn.ipsec_manualkey_data)
        if vpn.ipsec_manualkey_data['state'] == "present":
            return fos.set('vpn.ipsec',
                           'manualkey',
                           data=filtered_data,
                           vdom=vdom)
    
        elif vpn.ipsec_manualkey_data['state'] == "absent":
            return fos.delete('vpn.ipsec',
                              'manualkey',
                              mkey=filtered_data['name'],
                              vdom=vdom)
    
    

- fortios_vpn.ipsec

 .. code-block:: python

    def fortios_vpn.ipsec(data, fos):
        login(data)
    
        methodlist = ['vpn.ipsec_manualkey']
        for method in methodlist:
            if data[method]:
                resp = eval(method)(data, fos)
                break
    
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
            "https": {"required": False, "type": "bool", "default": "False"},
            "vpn.ipsec_manualkey": {
                "required": False, "type": "dict",
                "options": {
                    "state": {"required": True, "type": "str",
                              "choices": ["present", "absent"]},
                    "authentication": {"required": False, "type": "str",
                                       "choices": ["null", "md5", "sha1",
                                                   "sha256", "sha384", "sha512"]},
                    "authkey": {"required": False, "type": "str"},
                    "enckey": {"required": False, "type": "str"},
                    "encryption": {"required": False, "type": "str",
                                   "choices": ["null", "des"]},
                    "interface": {"required": False, "type": "str"},
                    "local-gw": {"required": False, "type": "str"},
                    "localspi": {"required": False, "type": "str"},
                    "name": {"required": True, "type": "str"},
                    "npu-offload": {"required": False, "type": "str",
                                    "choices": ["enable", "disable"]},
                    "remote-gw": {"required": False, "type": "str"},
                    "remotespi": {"required": False, "type": "str"}
    
                }
            }
        }
    
        module = AnsibleModule(argument_spec=fields,
                               supports_check_mode=False)
        try:
            from fortiosapi import FortiOSAPI
        except ImportError:
            module.fail_json(msg="fortiosapi module is required")
    
        global fos
        fos = FortiOSAPI()
    
        is_error, has_changed, result = fortios_vpn.ipsec(module.params, fos)
    
        if not is_error:
            module.exit_json(changed=has_changed, meta=result)
        else:
            module.fail_json(msg="Error in repo", meta=result)
    
    



Module Source Code
------------------

.. code-block:: python

    #!/usr/bin/python
    from __future__ import (absolute_import, division, print_function)
    # Copyright 2018 Fortinet, Inc.
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
    #
    # the lib use python logging can get it if the following is set in your
    # Ansible config.
    
    __metaclass__ = type
    
    ANSIBLE_METADATA = {'status': ['preview'],
                        'supported_by': 'community',
                        'metadata_version': '1.1'}
    
    DOCUMENTATION = '''
    ---
    module: fortios_vpn.ipsec_manualkey
    short_description: Configure IPsec manual keys.
    description:
        - This module is able to configure a FortiGate or FortiOS by
          allowing the user to configure vpn.ipsec feature and manualkey category.
          Examples includes all options and need to be adjusted to datasources before usage.
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
                - FortiOS or FortiGate ip adress.
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
            default: false
        vpn.ipsec_manualkey:
            description:
                - Configure IPsec manual keys.
            default: null
            suboptions:
                state:
                    description:
                        - Indicates whether to create or remove the object
                    choices:
                        - present
                        - absent
                authentication:
                    description:
                        - Authentication algorithm. Must be the same for both ends of the tunnel.
                    choices:
                        - null
                        - md5
                        - sha1
                        - sha256
                        - sha384
                        - sha512
                authkey:
                    description:
                        - Hexadecimal authentication key in 16-digit (8-byte) segments separated by hyphens.
                enckey:
                    description:
                        - Hexadecimal encryption key in 16-digit (8-byte) segments separated by hyphens.
                encryption:
                    description:
                        - Encryption algorithm. Must be the same for both ends of the tunnel.
                    choices:
                        - null
                        - des
                interface:
                    description:
                        - Name of the physical, aggregate, or VLAN interface. Source system.interface.name.
                local-gw:
                    description:
                        - Local gateway.
                localspi:
                    description:
                        - Local SPI, a hexadecimal 8-digit (4-byte) tag. Discerns between two traffic streams with different encryption rules.
                name:
                    description:
                        - IPsec tunnel name.
                    required: true
                npu-offload:
                    description:
                        - Enable/disable NPU offloading.
                    choices:
                        - enable
                        - disable
                remote-gw:
                    description:
                        - Peer gateway.
                remotespi:
                    description:
                        - Remote SPI, a hexadecimal 8-digit (4-byte) tag. Discerns between two traffic streams with different encryption rules.
    '''
    
    EXAMPLES = '''
    - hosts: localhost
      vars:
       host: "192.168.122.40"
       username: "admin"
       password: ""
       vdom: "root"
      tasks:
      - name: Configure IPsec manual keys.
        fortios_vpn.ipsec_manualkey:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          vpn.ipsec_manualkey:
            state: "present"
            authentication: "null"
            authkey: "<your_own_value>"
            enckey: "<your_own_value>"
            encryption: "null"
            interface: "<your_own_value> (source system.interface.name)"
            local-gw: "<your_own_value>"
            localspi: "<your_own_value>"
            name: "default_name_10"
            npu-offload: "enable"
            remote-gw: "<your_own_value>"
            remotespi: "<your_own_value>"
    '''
    
    RETURN = '''
    build:
      description: Build number of the fortigate image
      returned: always
      type: string
      sample: '1547'
    http_method:
      description: Last method used to provision the content into FortiGate
      returned: always
      type: string
      sample: 'PUT'
    http_status:
      description: Last result given by FortiGate on last operation applied
      returned: always
      type: string
      sample: "200"
    mkey:
      description: Master key (id) used in the last call to FortiGate
      returned: success
      type: string
      sample: "key1"
    name:
      description: Name of the table used to fulfill the request
      returned: always
      type: string
      sample: "urlfilter"
    path:
      description: Path of the table used to fulfill the request
      returned: always
      type: string
      sample: "webfilter"
    revision:
      description: Internal revision number
      returned: always
      type: string
      sample: "17.0.2.10658"
    serial:
      description: Serial number of the unit
      returned: always
      type: string
      sample: "FGVMEVYYQT3AB5352"
    status:
      description: Indication of the operation's result
      returned: always
      type: string
      sample: "success"
    vdom:
      description: Virtual domain used
      returned: always
      type: string
      sample: "root"
    version:
      description: Version of the FortiGate
      returned: always
      type: string
      sample: "v5.6.3"
    
    '''
    
    from ansible.module_utils.basic import AnsibleModule
    
    fos = None
    
    
    def login(data):
        host = data['host']
        username = data['username']
        password = data['password']
    
        fos.debug('on')
        if 'https' in data and not data['https']:
            fos.https('off')
        else:
            fos.https('on')
    
        fos.login(host, username, password)
    
    
    def filter_vpn.ipsec_manualkey_data(json):
        option_list = ['authentication', 'authkey', 'enckey',
                       'encryption', 'interface', 'local-gw',
                       'localspi', 'name', 'npu-offload',
                       'remote-gw', 'remotespi']
        dictionary = {}
    
        for attribute in option_list:
            if attribute in json and json[attribute] is not None:
                dictionary[attribute] = json[attribute]
    
        return dictionary
    
    
    def vpn.ipsec_manualkey(data, fos):
        vdom = data['vdom']
        vpn.ipsec_manualkey_data = data['vpn.ipsec_manualkey']
        filtered_data = filter_vpn.ipsec_manualkey_data(vpn.ipsec_manualkey_data)
        if vpn.ipsec_manualkey_data['state'] == "present":
            return fos.set('vpn.ipsec',
                           'manualkey',
                           data=filtered_data,
                           vdom=vdom)
    
        elif vpn.ipsec_manualkey_data['state'] == "absent":
            return fos.delete('vpn.ipsec',
                              'manualkey',
                              mkey=filtered_data['name'],
                              vdom=vdom)
    
    
    def fortios_vpn.ipsec(data, fos):
        login(data)
    
        methodlist = ['vpn.ipsec_manualkey']
        for method in methodlist:
            if data[method]:
                resp = eval(method)(data, fos)
                break
    
        fos.logout()
        return not resp['status'] == "success", resp['status'] == "success", resp
    
    
    def main():
        fields = {
            "host": {"required": True, "type": "str"},
            "username": {"required": True, "type": "str"},
            "password": {"required": False, "type": "str", "no_log": True},
            "vdom": {"required": False, "type": "str", "default": "root"},
            "https": {"required": False, "type": "bool", "default": "False"},
            "vpn.ipsec_manualkey": {
                "required": False, "type": "dict",
                "options": {
                    "state": {"required": True, "type": "str",
                              "choices": ["present", "absent"]},
                    "authentication": {"required": False, "type": "str",
                                       "choices": ["null", "md5", "sha1",
                                                   "sha256", "sha384", "sha512"]},
                    "authkey": {"required": False, "type": "str"},
                    "enckey": {"required": False, "type": "str"},
                    "encryption": {"required": False, "type": "str",
                                   "choices": ["null", "des"]},
                    "interface": {"required": False, "type": "str"},
                    "local-gw": {"required": False, "type": "str"},
                    "localspi": {"required": False, "type": "str"},
                    "name": {"required": True, "type": "str"},
                    "npu-offload": {"required": False, "type": "str",
                                    "choices": ["enable", "disable"]},
                    "remote-gw": {"required": False, "type": "str"},
                    "remotespi": {"required": False, "type": "str"}
    
                }
            }
        }
    
        module = AnsibleModule(argument_spec=fields,
                               supports_check_mode=False)
        try:
            from fortiosapi import FortiOSAPI
        except ImportError:
            module.fail_json(msg="fortiosapi module is required")
    
        global fos
        fos = FortiOSAPI()
    
        is_error, has_changed, result = fortios_vpn.ipsec(module.params, fos)
    
        if not is_error:
            module.exit_json(changed=has_changed, meta=result)
        else:
            module.fail_json(msg="Error in repo", meta=result)
    
    
    if __name__ == '__main__':
        main()


