=========================
fortios_application_group
=========================


Metadata
--------




**Name:** fortios_application_group

**Description:** This module is able to configure a FortiGate or FortiOS by allowing the user to configure application feature and group category. Examples includes all options and need to be adjusted to datasources before usage. Tested with FOS v6.0.2


**Author(s):** 

- Miguel Angel Munoz (github: @mamunozgonzalez)

- Nicolas Thomas (github: @thomnico)



**Ansible Version Added/Required:** 2.8

**Dev Status:** No status updates, yet. Contact Authors.

Parameters
----------

application_group
+++++++++++++++++

- Description: Configure firewall application groups.

  

- default: None

host
++++

- Description: FortiOS or FortiGate ip address.

  

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
    
    

- filter_application_group_data

 .. code-block:: python

    def filter_application_group_data(json):
        option_list = ['application', 'category', 'comment',
                       'name', 'type']
        dictionary = {}
    
        for attribute in option_list:
            if attribute in json and json[attribute] is not None:
                dictionary[attribute] = json[attribute]
    
        return dictionary
    
    

- application_group

 .. code-block:: python

    def application_group(data, fos):
        vdom = data['vdom']
        application_group_data = data['application_group']
        filtered_data = filter_application_group_data(application_group_data)
        if application_group_data['state'] == "present":
            return fos.set('application',
                           'group',
                           data=filtered_data,
                           vdom=vdom)
    
        elif application_group_data['state'] == "absent":
            return fos.delete('application',
                              'group',
                              mkey=filtered_data['name'],
                              vdom=vdom)
    
    

- fortios_application

 .. code-block:: python

    def fortios_application(data, fos):
        login(data)
    
        methodlist = ['application_group']
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
            "application_group": {
                "required": False, "type": "dict",
                "options": {
                    "state": {"required": True, "type": "str",
                              "choices": ["present", "absent"]},
                    "application": {"required": False, "type": "list",
                                    "options": {
                                        "id": {"required": True, "type": "int"}
                                    }},
                    "category": {"required": False, "type": "list",
                                 "options": {
                                     "id": {"required": True, "type": "int"}
                                 }},
                    "comment": {"required": False, "type": "str"},
                    "name": {"required": True, "type": "str"},
                    "type": {"required": False, "type": "str",
                             "choices": ["application", "category"]}
    
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
    
        is_error, has_changed, result = fortios_application(module.params, fos)
    
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
    module: fortios_application_group
    short_description: Configure firewall application groups in Fortinet's FortiOS and FortiGate.
    description:
        - This module is able to configure a FortiGate or FortiOS by
          allowing the user to configure application feature and group category.
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
            default: false
        application_group:
            description:
                - Configure firewall application groups.
            default: null
            suboptions:
                state:
                    description:
                        - Indicates whether to create or remove the object
                    choices:
                        - present
                        - absent
                application:
                    description:
                        - Application ID list.
                    suboptions:
                        id:
                            description:
                                - Application IDs.
                            required: true
                category:
                    description:
                        - Application category ID list.
                    suboptions:
                        id:
                            description:
                                - Category IDs.
                            required: true
                comment:
                    description:
                        - Comment
                name:
                    description:
                        - Application group name.
                    required: true
                type:
                    description:
                        - Application group type.
                    choices:
                        - application
                        - category
    '''
    
    EXAMPLES = '''
    - hosts: localhost
      vars:
       host: "192.168.122.40"
       username: "admin"
       password: ""
       vdom: "root"
      tasks:
      - name: Configure firewall application groups.
        fortios_application_group:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          application_group:
            state: "present"
            application:
             -
                id:  "4"
            category:
             -
                id:  "6"
            comment: "Comment"
            name: "default_name_8"
            type: "application"
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
    
    
    def filter_application_group_data(json):
        option_list = ['application', 'category', 'comment',
                       'name', 'type']
        dictionary = {}
    
        for attribute in option_list:
            if attribute in json and json[attribute] is not None:
                dictionary[attribute] = json[attribute]
    
        return dictionary
    
    
    def application_group(data, fos):
        vdom = data['vdom']
        application_group_data = data['application_group']
        filtered_data = filter_application_group_data(application_group_data)
        if application_group_data['state'] == "present":
            return fos.set('application',
                           'group',
                           data=filtered_data,
                           vdom=vdom)
    
        elif application_group_data['state'] == "absent":
            return fos.delete('application',
                              'group',
                              mkey=filtered_data['name'],
                              vdom=vdom)
    
    
    def fortios_application(data, fos):
        login(data)
    
        methodlist = ['application_group']
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
            "application_group": {
                "required": False, "type": "dict",
                "options": {
                    "state": {"required": True, "type": "str",
                              "choices": ["present", "absent"]},
                    "application": {"required": False, "type": "list",
                                    "options": {
                                        "id": {"required": True, "type": "int"}
                                    }},
                    "category": {"required": False, "type": "list",
                                 "options": {
                                     "id": {"required": True, "type": "int"}
                                 }},
                    "comment": {"required": False, "type": "str"},
                    "name": {"required": True, "type": "str"},
                    "type": {"required": False, "type": "str",
                             "choices": ["application", "category"]}
    
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
    
        is_error, has_changed, result = fortios_application(module.params, fos)
    
        if not is_error:
            module.exit_json(changed=has_changed, meta=result)
        else:
            module.fail_json(msg="Error in repo", meta=result)
    
    
    if __name__ == '__main__':
        main()


