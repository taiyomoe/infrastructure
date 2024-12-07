# Server onboarding

Currently, we have a few servers. Every time we want to integrate a new one into our infrastructure, we have to make sure they meet our security standards. We've got a few Ansible scripts that do all this work automatically.

## Steps

### Preparing the servers

First of all, you should upload your SSH Public Key to every new server. You can do that with the following command:

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub USERNAME@IP_ADDRESS
```

### Installing Ansible and dependencies

We're using Ansible to automate the setup of our servers. After installing it, you'll have have to also install the community modules:

```bash
ansible-galaxy collection install community.general
```

You might also need to install `passlib`:

```bash
pip install --break-system-packages passlib
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
