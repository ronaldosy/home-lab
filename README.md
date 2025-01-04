# Home Lab

This repo for my documentation, so I can build my kubernetes rapidly. 
control-plan and workers VM installed on top proxmox.

All scripts and and guide has been tested on Rocky Linux 9. 

Ansible will be executed on management VM, this mangagement VM also will be used to manage the kubernetes cluster

For kubernetes cluster consist of 1 Control Plane and 2 Worker Nodes.

## Get started
To use this lab we need to install ansible first.
1. Install epel repo 
   ```bash
   sudo dnf install epel-release
   ```

2. Install ansible
   ```bash
    sudo dnf install ansible
   ```
After install ansible, we need to add kernetes repo and install kubectl & kubeadm in Management node 
```bash
sudo ansible homelab/ansible/install_kube_tools.yml
```
## Execute ansible playbook. 

To run the ansible playbook I use the following command 
```bash
ansible-playbook --key-file <location_ssh_key_file> -i <inventory_file> <playbook_file>
```

**Example**
```bash
ansible-playbook --key-file /opt/ansible/ssh-key/ansible -i home-lab/ansible/kube-install/00-kube-hosts.yml home-lab/ansible/kube-install/01-open-port.yml
```
