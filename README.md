# ansible-playbook-symfony-demo

## Requirements

Ansible must be installed.

    ansible-galaxy install -r provision/requirements.txt --force

## Launch dev environment

You should then add to your `/etc/host`:

    12.34.56.78 symfony.dev
    12.34.56.78 symfony.prod

    vagrant up

## Provision production

    ansible-playbook -i provision/hosts/prod provision/playbook.yml -vvv -u ubuntu
