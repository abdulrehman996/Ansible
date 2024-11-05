# Ansible Guide 

This guide provides a set of commands for configuring Ansible to manage remote servers. Follow each step to set up and run basic Ansible commands on your servers.

---

## Prerequisites

- **Ansible Installed**: Ensure Ansible is installed on your local machine. [Installation guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- **SSH Key**: Have your SSH private key available to access the remote servers.
- **Servers Accessible via SSH**: Ensure the remote servers can be accessed via SSH.

---

## Step 1: Configure the Ansible Hosts File

1. Open the Ansible hosts configuration file with `vim` (or your preferred text editor):

    ```bash
    sudo vim /etc/ansible/hosts
    ```

2. Add the following configuration to define your servers and variables:

    ```plaintext
    [servers]
    server1 ansible_host=ip
    server2 ansible_host=ip

    [all:vars]
    ansible_python_interpreter=/usr/bin/python3
    ansible_user=ubuntu
    ansible_ssh_private_key_file=/home/ubuntu/key.pem
    ```

    - **[servers]**: Defines a group of servers, which you can refer to as `servers` in your Ansible commands.
    - **ansible_python_interpreter**: Specifies the path to Python 3 on the remote server.
    - **ansible_user**: Sets the remote user for Ansible to connect with (e.g., `ubuntu`).
    - **ansible_ssh_private_key_file**: Path to your private SSH key used for server access.

3. Save and close the file.

---

## Step 2: Verify the Inventory Configuration

To check if the inventory is correctly set up, use the following command:

      ```bash
      ansible-inventory --list
      ```

This command will display the list of hosts and variables as defined in /etc/ansible/hosts.

## Step 3: Test Connectivity to Servers
Ping the Servers: Use the ping module to verify Ansible can connect to each server:

      ```bash
      ansible -m ping servers
      ```
This should return a pong response from each server if the connection is successful.

      ```plaintext
      The authenticity of host 'ip (ip)' can't be established.
      ED25519 key fingerprint is SHA256:
      This key is not known by any other names.
      Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
      server1 | SUCCESS => {
          "changed": false,
          "ping": "pong"
      }
      server2 | SUCCESS => {
          "changed": false,
          "ping": "pong"
      }
      ```

## Step 4: Run Basic Commands on the Servers
Check Free Memory: Run the free -h command to display the memory status on all servers:

```bash
ansible -a "free -h" servers
```
Update Package Index: Run the following command to update the package list on each server:

```bash
ansible -a "sudo apt-get update" servers
```
