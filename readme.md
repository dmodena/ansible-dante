# Dante SOCKS5 server setup on Ubuntu

This playbook installs and configures a Dante SOCKS5 proxy on a new Ubuntu server. It also configures the server with the basic setup for security.

## Settings

Ansible needs to be able to connect to the server(s) where Dante will be installed. For that, we first need to have the server listed in the inventory, as such:

```ini
[servers]
<server_name> ansible_host=<ip> ansible_user=<ssh_user> ansible_ssh_private_key_file=<ssh_key_path>
```

The inventory is usually located in /etc/ansible/hosts. If you can't find the file, just create a new one, and pass it's path as argument to Ansible commands with the `-i` flag.

### Testing connection

To test if Ansible is able to connect to your servers, run the following command: `ansible all -m ping -i <inventory_file>`.

### Variables

Before you run this playbook, you will need to create a **vars.yml** file. This file should not be added to the repository since it may contain sensitive data. The following variables should be added to it:

- `username`: the user to run Dante. This will be created as both user and group on Ubuntu.
- `password`: Dante user password. The password needs to be hashed, not added to the file as plain text. On Linux you can create hashed passwords with the following command: `mkpasswd -m sha-512`. For other options, follow the instructions [here](https://docs.ansible.com/ansible/latest/reference_appendices/faq.html#how-do-i-generate-encrypted-passwords-for-the-user-module).

## Execute

To run the playbook: `ansible-playbook -l <server_name> -i <inventory> -u <user> playbook.yml`

## Limitations

Although the configuration file has the setup for IPv6, I wasn't able to successfully test an IPv6 proxy connection.

---

Douglas Modena  
2023  
MIT License
