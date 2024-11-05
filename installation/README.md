# Ansible Installation Guide (Ubuntu)

This guide provides step-by-step instructions for installing Ansible on Ubuntu.

---

## Prerequisites

- **Python**: Ansible requires Python, which is usually pre-installed on Ubuntu.
- **sudo/root access**: You may need administrator privileges for installation.

---

## Installation Steps

### Step 1: Adding The Repository

Start by adding the ansible repository:

```bash
sudo apt-add-repository ppa:ansible/ansible
```

### Step 2: Update Package Index

Start by updating your package index to ensure you have the latest package listings:

```bash
sudo apt update
```

### Step 2: Install Ansible
Now, install Ansible with the following command:

```bash
sudo apt install -y ansible
```

### Step 3: Verify the Installation
Once installed, you can verify Ansible by checking its version:

```bash
ansible --version
```

If the installation was successful, this command should output the version of Ansible and confirm that it's properly installed.

## Uninstallation
If you need to remove Ansible, you can uninstall it with the following command:

```bash
sudo apt remove --purge ansible
```