==========================
fortios_dlp_fp_sensitivity
==========================


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
      - name: Create self-explanatory DLP sensitivity levels to be used when setting sensitivity under config fp-doc-source.
        fortios_dlp_fp_sensitivity:
          host:  "{{ host }}"
          username: "{{ username }}"
          password: "{{ password }}"
          vdom:  "{{ vdom }}"
          dlp_fp_sensitivity:
            state: "present"
            name: "default_name_3"



Playbook File Examples
----------------------

%%PB_FILE_EXAMPLE_TOKEN%%

