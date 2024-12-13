# Server onboarding

Currently, we have a few servers. Every time we want to integrate a new one into our infrastructure, we have to make sure they meet our security standards. We've got a few Ansible scripts that do all this work automatically.

## Steps

### Preparing your environment

First of all, you'll need to install Ansible and the community modules.

```bash
# Install pipx
brew install pipx
pipx ensurepath
sudo pipx ensurepath --global # optional to allow pipx actions with --global argument

# Install Ansible
pipx install --include-deps ansible

# Install ansible-dev-tools if you plan on developing Ansible modules
pipx inject ansible ansible-dev-tools

# Install passlib
pipx inject ansible passlib
```

If you installed `ansible-dev-tools`, you'll have to make sure to select the correct Python interpreter on VSCode. It is typically located at `~/.local/pipx/venvs/ansible/bin/python3`.

### Preparing the servers

First of all, you should upload your SSH Public Key to every new server. You can do that with the following command:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub USERNAME@IP_ADDRESS
```

### Creating the inventory file

Create a `inventory.ini` file that will contain the new server batch.

```ini
[nodes]
HOSTNAME ansible_host=IP_ADDRESS ansible_user=USERNAME
# ...
```

### Running the playbook

Everything should be ready now. You can run the playbook with:

```bash
ansible-playbook -i inventory.ini playbooks/setup-node.yml
```
