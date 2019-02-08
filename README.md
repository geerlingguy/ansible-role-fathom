# Ansible Role: Fathom

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-fathom.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-fathom)

Installs [Fathom](https://github.com/usefathom/fathom), a Go-based website analytics system.

After the playbook is finished, visit the fathom interface (on port 9000 by default), and you can see instructions for configuring websites to send analytics to your Fathom server.

## Requirements

N/A, though you may wish to also install and configure Nginx as a proxy for security and stability reasons, and Certbot to acquire and use a valid TLS certificate for HTTPS (recommended roles: `geerlingguy.nginx` and `geerlingguy.certbot`).

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    fathom_binary_url: https://github.com/usefathom/fathom/releases/download/v1.2.1/fathom_1.2.1_linux_amd64.tar.gz

The URL from which Fathom will be downloaded. Override for a newer or different version, or to lock in a specific version.

    fathom_force_update: false

If changing versions, use this flag to force Ansible to change Fathom versions on the server.

    fathom_manage_service: true
    fathom_service_state: started
    fathom_service_enabled: true
    fathom_service_user: root

Fathom service controls; useful if you want to stop the service, not have it enabled at boot, or are running Fathom inside a container where the service configuration is not helpful.

    fathom_directory: /opt/fathom

The directory inside which Fathom configuration and the default SQLite database are stored.

    fathom_http_port: "9000"
    fathom_database_name: fathom.db
    fathom_secret: secret-string-here

Fathom configuration options. Make sure you override `fathom_secret` in your playbook for better security!

## Dependencies

None.

## Example Playbook

    - hosts: analytics
    
      vars_files:
        - vars/main.yml
    
      roles:
        - geerlingguy.fathom

*Inside `vars/main.yml`*:

    fathom_secret: insert-a-secret-string-here

## Use with Nginx as a proxy

**See**: [Fathom playbook example using Nginx as a proxy](molecule/default/playbook-nginx.yml).

Note that you can also add the role `geerlingguy.certbot` if you want to install certbot and configure a default certificate to work with the Nginx server configuration for HTTPS on your Fathom installation.

## License

MIT / BSD

## Author Information

This role was created in 2019 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
