So Ansible seams to have change how the dependencies are included.

Relative isssue: https://github.com/ansible/ansible/issues/81486

Ansible 2.9.4:
```
PLAY [Test ansible dependencies.] ****************************************************************************************************************************************************************************************************************************

TASK [common : Debug] ****************************************************************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [containers/one : Debug] ********************************************************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [common : Debug] ****************************************************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "changed": false,
    "msg": "Common dependency run."
}

TASK [containers/two : Debug] ********************************************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "changed": false,
    "msg": "Role two."
}

TASK [containers/three : Debug] ******************************************************************************************************************************************************************************************************************************
skipping: [localhost]

PLAY RECAP ***************************************************************************************************************************************************************************************************************************************************
localhost                  : ok=2    changed=0    unreachable=0    failed=0    skipped=3    rescued=0    ignored=0   

```

Ansible 2.14.8 and 2.14.9:

```
~/.virtualenvs/tmp-b815a9028a0924e/test » ansible-playbook -i inventory.ini play.yml

PLAY [Test ansible dependencies.] **************************************************************************************************************************************************************************************

TASK [common : Debug] **************************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [containers/one : Debug] ******************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [common : Debug] **************************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Common dependency run."
}

TASK [containers/two : Debug] ******************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Role two."
}

TASK [containers/three : Debug] ****************************************************************************************************************************************************************************************
skipping: [localhost]

PLAY RECAP *************************************************************************************************************************************************************************************************************
localhost                  : ok=2    changed=0    unreachable=0    failed=0    skipped=3    rescued=0    ignored=0   
```

Ansible 2.15.3:
```
~/.virtualenvs/tmp-b815a9028a0924e/test » ansible-playbook -i inventory.ini play.yml

PLAY [Test ansible dependencies.] **************************************************************************************************************************************************************************************

TASK [common : Debug] **************************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [containers/one : Debug] ******************************************************************************************************************************************************************************************
skipping: [localhost]

TASK [containers/two : Debug] ******************************************************************************************************************************************************************************************
ok: [localhost] => {
    "msg": "Role two."
}

TASK [containers/three : Debug] ****************************************************************************************************************************************************************************************
skipping: [localhost]

PLAY RECAP *************************************************************************************************************************************************************************************************************
localhost                  : ok=1    changed=0    unreachable=0    failed=0    skipped=3    rescued=0    ignored=0   
```
