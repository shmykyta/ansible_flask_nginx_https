# use

```
export ANSIBLE_CONFIG=<<project_path>>/ansible_config/env.cfg; \
ansible-playbook -v <<project_path>>/playbooks/takeoff_task.yml
\ -e host='google_cloud'
```