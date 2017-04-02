# Ansible Demo
This is a simplistic demo of a few of [Ansible's](https://www.ansible.com/) features. 
It will install an Apache server with SSL and PHP on a pair of web servers, and a MySQL database on a separate database server.

## Requirements
Ansible relies on SSH and Python. 
 * An SSH client (preferably OpenSSH) must be installed on the control machine. 
 * An SSH server (preferably OpenSSH) must be running on each managed node.
 * Python 2.6 or later must also be installed on each managed node.
 * You must define the three hosts (web01, web02, db01) in DNS, hosts files, or SSH configs so the machines can resolve them properly.
 * The control node must be able to SSH to all managed nodes. This includes setting proper firewall rules.
 * The webservers must have a route to the database.
  * A user on each managed node with `sudo` privileges. For simplicity, the user should have the same password on all managed nodes.

## Environment
### Servers
Three total servers will be configured: two webservers (web01 and web02), and one database server (db01). The nodes can be physical servers, virtual machines, or cloud-based images as long as they meet the requirements above.
This code was written and tested againt Ubuntu 16.04 machines. It should work with any Ubuntu-based distro (and really, any Debian-based distro), but it has not been tested as such.

### Software
Ansible 2.2.2.0 was installed on the control machine. Python 2.7.12 was installed on all servers.  

### User Authentication
The control node should have an SSH keypair generated. The public key should be added to the `authorized_keys` file on each managed node and the private key should be added to the ssh-agent on the control node.


## Running the Playbook
    ansible-playbook -i hosts -K demo.yml  
`-i hosts` forces the playbook to use the inventory file `hosts` in the current directory, provided by the repo.  
`-K` prompts the user for the sudo password for the user on the managed nodes.
