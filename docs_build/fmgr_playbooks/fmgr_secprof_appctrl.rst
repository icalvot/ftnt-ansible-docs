====================
fmgr_secprof_appctrl
====================


Playbook Task Examples
----------------------

.. code-block:: yaml

      - name: DELETE Profile
        fmgr_secprof_appctrl:
          name: "Ansible_Application_Control_Profile"
          comment: "Created by Ansible Module TEST"
          mode: "delete"
    
      - name: CREATE Profile
        fmgr_secprof_appctrl:
          name: "Ansible_Application_Control_Profile"
          comment: "Created by Ansible Module TEST"
          mode: "set"
          entries: [{
                    action: "block",
                    log: "enable",
                    log-packet: "enable",
                    protocols: ["1"],
                    quarantine: "attacker",
                    quarantine-log: "enable",
                    },
                    {action: "pass",
                    category: ["2","3","4"]},
                  ]



Playbook File Examples
----------------------

%%PB_FILE_EXAMPLE_TOKEN%%

