===============================
fortios_vpn.certificate_setting
===============================


Metadata
--------




**Name:** fortios_vpn.certificate_setting

**Description:** This module is able to configure a FortiGate or FortiOS by allowing the user to configure vpn.certificate feature and setting category. Examples includes all options and need to be adjusted to datasources before usage. Tested with FOS v6.0.2


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

vpn.certificate_setting
+++++++++++++++++++++++

- Description: VPN certificate setting.

  

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
    
    

- filter_vpn.certificate_setting_data

 .. code-block:: python

    def filter_vpn.certificate_setting_data(json):
        option_list = ['certname-dsa1024', 'certname-dsa2048', 'certname-ecdsa256',
                       'certname-ecdsa384', 'certname-rsa1024', 'certname-rsa2048',
                       'check-ca-cert', 'check-ca-chain', 'cmp-save-extra-certs',
                       'cn-match', 'ocsp-default-server', 'ocsp-status',
                       'ssl-min-proto-version', 'ssl-ocsp-option', 'ssl-ocsp-status',
                       'strict-crl-check', 'strict-ocsp-check', 'subject-match']
        dictionary = {}
    
        for attribute in option_list:
            if attribute in json and json[attribute] is not None:
                dictionary[attribute] = json[attribute]
    
        return dictionary
    
    

- vpn.certificate_setting

 .. code-block:: python

    def vpn.certificate_setting(data, fos):
        vdom = data['vdom']
        vpn.certificate_setting_data = data['vpn.certificate_setting']
        filtered_data = filter_vpn.certificate_setting_data(
            vpn.certificate_setting_data)
        return fos.set('vpn.certificate',
                       'setting',
                       data=filtered_data,
                       vdom=vdom)
    
    

- fortios_vpn.certificate

 .. code-block:: python

    def fortios_vpn.certificate(data, fos):
        login(data)
    
        methodlist = ['vpn.certificate_setting']
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
            "vpn.certificate_setting": {
                "required": False, "type": "dict",
                "options": {
                    "certname-dsa1024": {"required": False, "type": "str"},
                    "certname-dsa2048": {"required": False, "type": "str"},
                    "certname-ecdsa256": {"required": False, "type": "str"},
                    "certname-ecdsa384": {"required": False, "type": "str"},
                    "certname-rsa1024": {"required": False, "type": "str"},
                    "certname-rsa2048": {"required": False, "type": "str"},
                    "check-ca-cert": {"required": False, "type": "str",
                                      "choices": ["enable", "disable"]},
                    "check-ca-chain": {"required": False, "type": "str",
                                       "choices": ["enable", "disable"]},
                    "cmp-save-extra-certs": {"required": False, "type": "str",
                                             "choices": ["enable", "disable"]},
                    "cn-match": {"required": False, "type": "str",
                                 "choices": ["substring", "value"]},
                    "ocsp-default-server": {"required": False, "type": "str"},
                    "ocsp-status": {"required": False, "type": "str",
                                    "choices": ["enable", "disable"]},
                    "ssl-min-proto-version": {"required": False, "type": "str",
                                              "choices": ["default", "SSLv3", "TLSv1",
                                                          "TLSv1-1", "TLSv1-2"]},
                    "ssl-ocsp-option": {"required": False, "type": "str",
                                        "choices": ["certificate", "server"]},
                    "ssl-ocsp-status": {"required": False, "type": "str",
                                        "choices": ["enable", "disable"]},
                    "strict-crl-check": {"required": False, "type": "str",
                                         "choices": ["enable", "disable"]},
                    "strict-ocsp-check": {"required": False, "type": "str",
                                          "choices": ["enable", "disable"]},
                    "subject-match": {"required": False, "type": "str",
                                      "choices": ["substring", "value"]}
    
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
    
        is_error, has_changed, result = fortios_vpn.certificate(module.params, fos)
    
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
    module: fortios_vpn.certificate_setting
    short_description: VPN certificate setting.
    description:
        - This module is able to configure a FortiGate or FortiOS by
          allowing the user to configure vpn.certificate feature and setting category.
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
        vpn.certificate_setting:
            description:
                - VPN certificate setting.
            default: null
            suboptions:
                certname-dsa1024:
                    description:
                        - 1024 bit DSA key certificate for re-signing server certificates for SSL inspection. Source vpn.certificate.local.name.
                certname-dsa2048:
                    description:
                        - 2048 bit DSA key certificate for re-signing server certificates for SSL inspection. Source vpn.certificate.local.name.
                certname-ecdsa256:
                    description:
                        - 256 bit ECDSA key certificate for re-signing server certificates for SSL inspection. Source vpn.certificate.local.name.
                certname-ecdsa384:
                    description:
                        - 384 bit ECDSA key certificate for re-signing server certificates for SSL inspection. Source vpn.certificate.local.name.
                certname-rsa1024:
                    description:
                        - 1024 bit RSA key certificate for re-signing server certificates for SSL inspection. Source vpn.certificate.local.name.
                certname-rsa2048:
                    description:
                        - 2048 bit RSA key certificate for re-signing server certificates for SSL inspection. Source vpn.certificate.local.name.
                check-ca-cert:
                    description:
                        - Enable/disable verification of the user certificate and pass authentication if any CA in the chain is trusted (default = enable).
                    choices:
                        - enable
                        - disable
                check-ca-chain:
                    description:
                        - Enable/disable verification of the entire certificate chain and pass authentication only if the chain is complete and all of the CAs in
                           the chain are trusted (default = disable).
                    choices:
                        - enable
                        - disable
                cmp-save-extra-certs:
                    description:
                        - Enable/disable saving extra certificates in CMP mode.
                    choices:
                        - enable
                        - disable
                cn-match:
                    description:
                        - When searching for a matching certificate, control how to find matches in the cn attribute of the certificate subject name.
                    choices:
                        - substring
                        - value
                ocsp-default-server:
                    description:
                        - Default OCSP server. Source vpn.certificate.ocsp-server.name.
                ocsp-status:
                    description:
                        - Enable/disable receiving certificates using the OCSP.
                    choices:
                        - enable
                        - disable
                ssl-min-proto-version:
                    description:
                        - Minimum supported protocol version for SSL/TLS connections (default is to follow system global setting).
                    choices:
                        - default
                        - SSLv3
                        - TLSv1
                        - TLSv1-1
                        - TLSv1-2
                ssl-ocsp-option:
                    description:
                        - Specify whether the OCSP URL is from the certificate or the default OCSP server.
                    choices:
                        - certificate
                        - server
                ssl-ocsp-status:
                    description:
                        - Enable/disable SSL OCSP.
                    choices:
                        - enable
                        - disable
                strict-crl-check:
                    description:
                        - Enable/disable strict mode CRL checking.
                    choices:
                        - enable
                        - disable
                strict-ocsp-check:
                    description:
                        - Enable/disable strict mode OCSP checking.
                    choices:
                        - enable
                        - disable
                subject-match:
                    description:
                        - When searching for a matching certificate, control how to find matches in the certificate subject name.
                    choices:
                        - substring
                        - value
    '''
    
    EXAMPLES = '''
    - hosts: localhost
      vars:
       host: "192.168.122.40"
       username: "admin"
       password: ""
       vdom: "root"
      tasks:
      - name: VPN certificate setting.
        fortios_vpn.certificate_setting:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          vpn.certificate_setting:
            certname-dsa1024: "<your_own_value> (source vpn.certificate.local.name)"
            certname-dsa2048: "<your_own_value> (source vpn.certificate.local.name)"
            certname-ecdsa256: "<your_own_value> (source vpn.certificate.local.name)"
            certname-ecdsa384: "<your_own_value> (source vpn.certificate.local.name)"
            certname-rsa1024: "<your_own_value> (source vpn.certificate.local.name)"
            certname-rsa2048: "<your_own_value> (source vpn.certificate.local.name)"
            check-ca-cert: "enable"
            check-ca-chain: "enable"
            cmp-save-extra-certs: "enable"
            cn-match: "substring"
            ocsp-default-server: "<your_own_value> (source vpn.certificate.ocsp-server.name)"
            ocsp-status: "enable"
            ssl-min-proto-version: "default"
            ssl-ocsp-option: "certificate"
            ssl-ocsp-status: "enable"
            strict-crl-check: "enable"
            strict-ocsp-check: "enable"
            subject-match: "substring"
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
    
    
    def filter_vpn.certificate_setting_data(json):
        option_list = ['certname-dsa1024', 'certname-dsa2048', 'certname-ecdsa256',
                       'certname-ecdsa384', 'certname-rsa1024', 'certname-rsa2048',
                       'check-ca-cert', 'check-ca-chain', 'cmp-save-extra-certs',
                       'cn-match', 'ocsp-default-server', 'ocsp-status',
                       'ssl-min-proto-version', 'ssl-ocsp-option', 'ssl-ocsp-status',
                       'strict-crl-check', 'strict-ocsp-check', 'subject-match']
        dictionary = {}
    
        for attribute in option_list:
            if attribute in json and json[attribute] is not None:
                dictionary[attribute] = json[attribute]
    
        return dictionary
    
    
    def vpn.certificate_setting(data, fos):
        vdom = data['vdom']
        vpn.certificate_setting_data = data['vpn.certificate_setting']
        filtered_data = filter_vpn.certificate_setting_data(
            vpn.certificate_setting_data)
        return fos.set('vpn.certificate',
                       'setting',
                       data=filtered_data,
                       vdom=vdom)
    
    
    def fortios_vpn.certificate(data, fos):
        login(data)
    
        methodlist = ['vpn.certificate_setting']
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
            "vpn.certificate_setting": {
                "required": False, "type": "dict",
                "options": {
                    "certname-dsa1024": {"required": False, "type": "str"},
                    "certname-dsa2048": {"required": False, "type": "str"},
                    "certname-ecdsa256": {"required": False, "type": "str"},
                    "certname-ecdsa384": {"required": False, "type": "str"},
                    "certname-rsa1024": {"required": False, "type": "str"},
                    "certname-rsa2048": {"required": False, "type": "str"},
                    "check-ca-cert": {"required": False, "type": "str",
                                      "choices": ["enable", "disable"]},
                    "check-ca-chain": {"required": False, "type": "str",
                                       "choices": ["enable", "disable"]},
                    "cmp-save-extra-certs": {"required": False, "type": "str",
                                             "choices": ["enable", "disable"]},
                    "cn-match": {"required": False, "type": "str",
                                 "choices": ["substring", "value"]},
                    "ocsp-default-server": {"required": False, "type": "str"},
                    "ocsp-status": {"required": False, "type": "str",
                                    "choices": ["enable", "disable"]},
                    "ssl-min-proto-version": {"required": False, "type": "str",
                                              "choices": ["default", "SSLv3", "TLSv1",
                                                          "TLSv1-1", "TLSv1-2"]},
                    "ssl-ocsp-option": {"required": False, "type": "str",
                                        "choices": ["certificate", "server"]},
                    "ssl-ocsp-status": {"required": False, "type": "str",
                                        "choices": ["enable", "disable"]},
                    "strict-crl-check": {"required": False, "type": "str",
                                         "choices": ["enable", "disable"]},
                    "strict-ocsp-check": {"required": False, "type": "str",
                                          "choices": ["enable", "disable"]},
                    "subject-match": {"required": False, "type": "str",
                                      "choices": ["substring", "value"]}
    
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
    
        is_error, has_changed, result = fortios_vpn.certificate(module.params, fos)
    
        if not is_error:
            module.exit_json(changed=has_changed, meta=result)
        else:
            module.fail_json(msg="Error in repo", meta=result)
    
    
    if __name__ == '__main__':
        main()


