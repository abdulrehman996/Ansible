# Ansible Custom Inventory Setup

This guide provides instructions on setting up custom inventory files in Ansible for managing different environments (e.g., `dev` and `prod`).

---

## Prerequisites

- **Ansible Installed**: Ensure Ansible is installed on your local machine. [Installation guide](https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html)
- **SSH Key**: Have your SSH private key available to access the remote servers.

---

## Step-by-Step Setup

### Step 1: Create a Project Directory

1. Start by creating a new directory for your Ansible files:

    ```bash
    mkdir ansible/
    cd ansible/
    ```

### Step 2: Create an Inventory Directory

1. Inside the `ansible` directory, create a directory for your inventory files:

    ```bash
    mkdir inventories
    ```

### Step 3: Create Custom Inventory Files for Different Environments

1. Navigate to the `ansible` directory:

    ```bash
    cd ~/ansible
    ```

2. Create the `dev` inventory file with the following command:

    ```bash
    sudo vim dev
    ```

3. Add the following content to the `dev` file to define your development environment servers:

    ```plaintext
    [servers]
    server1 ansible_host=54.221.60.141

    [servers:vars]
    ansible_python_interpreter=/usr/bin/python3
    ansible_user=ubuntu
    ansible_ssh_private_key_file=/home/ubuntu/keys/key.pem
    ```

4. Create the `prod` inventory file:

    ```bash
    sudo vim prod
    ```

5. Add the following content to the `prod` file to define your production environment servers:

    ```plaintext
    [servers]
    server2 ansible_host=54.90.71.205

    [servers:vars]
    ansible_python_interpreter=/usr/bin/python3
    ansible_user=ubuntu
    ansible_ssh_private_key_file=/home/ubuntu/keys/key.pem
    ```

6. To confirm the content of both files, you can use:

    ```bash
    cat dev prod
    ```

### Step 4: Test Connectivity to Each Environment

1. To test connectivity to the `dev` environment, use the following command:

    ```bash
    ansible -a "uptime" servers -i dev
    ```

   This should return the uptime information for `server1` defined in the `dev` inventory file.

---

## Summary of Inventory Files

- **dev**: Defines the servers and variables for the development environment.
- **prod**: Defines the servers and variables for the production environment.

Each inventory file specifies:
- **[servers]**: A group name for the servers in that environment.
- **[servers:vars]**: Variables applied to all servers in the group, including:
  - `ansible_python_interpreter`: Specifies the path to Python 3 on the remote server.
  - `ansible_user`: Remote user for Ansible to connect with.
  - `ansible_ssh_private_key_file`: Path to the private SSH key for server access.

---

## Additional Commands

- **List Inventory Content**: To check the contents of an inventory file, use:

    ```bash
    ansible-inventory -i dev --list
    ```

- **Run Commands on Specific Inventory**: Specify the inventory file with `-i <inventory_file>` when running Ansible commands:

    ```bash
    ansible -a "free -h" servers -i prod
    ```

---

## Additional Resources

- [Ansible Documentation](https://docs.ansible.com/): Official Ansible documentation.
- [Ansible Module Index](https://docs.ansible.com/ansible/latest/collections/index_module.html): A list of all available Ansible modules.

---

With this setup, you can easily manage multiple environments using customized inventory files in Ansible!
