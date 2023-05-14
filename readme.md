# Dante SOCKS5 server setup on Ubuntu

The aim of this playbook is to install and configure a Dante SOCKS5 proxy on a new Ubuntu server. It also configures the server with the basic setup for security.

## Settings

Ansible needs to be able to connect to the server(s) where Dante will be installed. For that, we first need to have the server listed in ansible inventory, as such:

```ini
[servers]
foo ansible_host=<ip> ansible_user=<ssh_user> ansible_ssh_private_key_file=<ssh_key_path>
```

If you cannot locate where the inventory is, just create a new file with this content, and then pass an aditional flag providing its path.

### Testing connection

To test if Ansible is able to connect to your servers, run the following command: `ansible all -m ping -i <inventory_file>`

### Variables

Before you run this playbook, you will need to create a **vars.yml** file with the following variables:

- `username`: the user to run dante. This will be created as both user and group on Ubuntu, the user will be passwordless and be granted sudo permissions.

## Execute

To run the playbook: `ansible-playbook -l <server_name> -i <inventory> -u <user> playbook.yml`
