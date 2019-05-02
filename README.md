######################################
# --- BAREKUBE --- #
######################################

It is a cloud which has been created using Kubernetes technology. You can use this code for creating a cloud on dedicated servers. More information about infrastructure and installation you can find below.

How to install:


First, you should install Ansible software for using playbooks

                sudo apt-get install ansible -y

Second, install python for using Ansible on all servers

                sudo apt-get install python -y

After installing the software you should update group_vars and hosts files in inventories directory, you should change parameters on existed in your infrastructure.

		├── inventories
		    └── stand
		        ├── group_vars
		        │   └── all.yml  <---
		        └── hosts        <---

After updating configurations files you should run Ansible playbooks in the following order:

                export ANSIBLE_HOST_KEY_CHECKING=False

                ansible-playbook -i inventories/stand/hosts barekube.yml -t users -e 'ansible_ssh_user=tester' -e 'become_user=tester' -Kk

                ansible-playbook -i inventories/stand/hosts barekube.yml

Reset cluster:

                ansible -i inventories/stand/hosts -a "kubeadm reset -f" all -b 

                ansible -i inventories/stand/hosts -a "rm -rf /root/cluster_initialized.txt /root/node_joined.txt" all -b
