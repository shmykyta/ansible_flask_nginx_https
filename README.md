# Ansible deploy Flask app+nginx+ssl

Deploy simple flask app to your remote server and setup NGINX as HTTP reverse proxy

## Requirements for run

Should to create user on remote server which able to switch on root without password and ssh key to connect
Provide parameters to ssh_conf file
    User                    --- user for remote changes -- (example deploy)
    IdentityFile            --- path to your ssh key ----- (example ~/.ssh/key_for_deploy)
    
 ### Variables for role
 
* user_add: 'somecoolguy' # add some user on this server with pass and able to sudo
* user_pass: 'yoursuperpass' # add encrypted key or user ansible vault for user name and pass
* app_user: 'deploy' # installer user what created and provided in ssh_conf file
* app_root: 'root' # root is root
* app_name: 'your_app' # name of your project
* app_dir: '/opt/{{ app_name }}' # example dir for app
* app_log_dir: '/opt/{{ app_name }}/log' # example dir for logs
* app_repo: https://github.com/your_git_repo/{{ app_name }}.git # app repo
* path_ssl: '/etc/ssl' # for generate your self-signed cert
* nginx_cert_path: '/etc/nginx/ssl' # for generate your self-signed cert

### Project tree


```
.
├── README.md
├── ansible_config
│   └── env.cfg
├── inventory
│   └── env.hosts
├── playbooks
│   └── flaskapp_nginx_ssl.yml
├── roles
│   └── init
│       ├── defaults
│       │   └── main.yml
│       ├── handlers
│       │   └── main.yml
│       ├── tasks
│       │   ├── app_build.yml
│       │   ├── app_update.yml
│       │   ├── init.yml
│       │   ├── main.yml
│       │   └── nginx.yml
│       └── templates
│           ├── app.nginx.conf.j2
│           ├── app.service.j2
│           ├── nginx.conf.j2
│           └── nginx.service.j2
└── ssh_conf
    └── env.ssh_config
```


## Run playbook
```
export ANSIBLE_CONFIG=<< path_to_your_project >>/ansible_config/env.cfg; \
ansible-playbook -v << path_to_your_project >>/playbooks/flaskapp_nginx_ssl.yml \
-e host='{{ YOUR HOSTS FROM INVENTORY }}'
```