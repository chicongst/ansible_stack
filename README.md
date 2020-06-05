# ANSIBLE SETUP ENVIRONMENT AND DEPLOY SOURCE

## Introduce
Ansible is simple open source IT engine which automates application deployment, intra service orchestration, cloud provisioning and many other IT tools.

## Setup 
### Prepare needed for the environment: 
- Copy main.yml.example to main.yml and config
- Copy inventory.example to inventory
- Copy laravel.j2 in roles/nginx/templates

## Initial setup | If use Ubuntu 16.04

Because ubuntu 16.04 have no python 2 and aptitude. Without those
programs ansible cannot work. To fix it run:

```sh
$ ansible-playbook initial-setup.yml
```

## Provision server

This playbook setup nginx, php-fpm, postgresql, nodejs, nvm, etc...

```sh
$ ansible-playbook setup.yml -i inventory
```

To run only specific roles
```sh
$ ansible-playbook setup.yml -i inventory --tags=user,nginx
```

To exclude specific roles
```sh
$ ansible-playbook setup.yml -i inventory --skip-tags=user,nginx
```

### For connection through ssh bastion
```
[cms:vars]
ansible_ssh_common_args= '-o ProxyCommand="ssh -W %h:%p mtb-bastion-prod"'
[curation:vars]
ansible_ssh_common_args= '-o ProxyCommand="ssh -W %h:%p mtb-bastion-prod"'
```

## Deploy
Check [deploy] source

