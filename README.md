# lxc-ssh-setup

Effortlessly provision and secure your LXC containers with SSH access. The `lxc-ssh-setup` Ansible playbook automates the installation of the OpenSSH server, enables root login, and deploys your SSH public key across your LXC containers, streamlining your container management and enhancing security protocols.

## Prerequisites

- Ansible installed on the host machine.
- LXC/LXD installed and configured on the host machine.
- Access to manage LXC containers from the host machine.
- An SSH public key you wish to deploy to the containers.

## Configuration

1. **SSH Public Key**: Place your SSH public key file in the `files/` directory of this project. Rename the key to `my_public_key.pub` or update the playbook with the correct file name.

2. **Playbook Variables**: The playbook uses variables to specify the container name. These can be set in the playbook file itself or passed as extra variables when running the playbook.

## Playbook Overview

The playbook `setup-lxc.yml` performs the following tasks:

- Installs `openssh-server` inside the specified LXC container.
- Configures SSH to allow root login by modifying `/etc/ssh/sshd_config`.
- Ensures the `.ssh` directory exists for the root user.
- Copies the specified SSH public key to the root user's `authorized_keys` file.
- Restarts the SSH service to apply changes.

## Usage

Run the playbook using the following command, substituting `your-container-name` with the name of your LXC container:

```bash
ansible-playbook setup-lxc.yml --extra-vars "container_name=your-container-name"
