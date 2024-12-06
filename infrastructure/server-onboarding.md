# Server onboarding

Currently, we have a few servers. Every time we want to integrate a new one into our infrastructure, we have to make sure they meet our security standards. We've got a few Ansible scripts that do all this work automatically.



First of all, you should upload your SSH Public Key to every new server.

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub USERNAME@IP_ADDRESS
```



I will assume you have Ansible installed on your local machine. Now, create a `inventory.ini` that will contain the new server batch.

```bash
[nodes]
HOSTNAME ansible_host=IP_ADDRESS ansible_user=USERNAME
HOSTNAME ansible_host=IP_ADDRESS ansible_user=USERNAME
```



Before running the setup playbook, you should install the community modules:

```bash
ansible-galaxy collection install community.general
```

You also might need to install \`passlib\`:

```bash
pip install --break-system-packages passlib
```



&#x20;Run the `setup-node.yml` playbook with:

```bash
ansible-playbook -i inventory.ini setup-node.playbook.yml
```
