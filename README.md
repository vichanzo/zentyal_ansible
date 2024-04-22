# zentyal_ansible
Install Zentyal on a Proxmox Container using ansible.

First install the basics:
```bash
sudo apt update
sudo apt install open-sshserver git ansible
```

Create / import your private key:
```bash
nano ~/.ssh/id_rsa
chmod 600 ~/.ssh/id_rsa
```
Create /import your public key:
```bash
nano ~/.ssh/id_rsa.pub
```
Test your keys with git:
```bash
ssh -T git@github.com
```
Clone this repository:
```bash
git clone git@github.com:vichanzo/zentyal_ansible.git

```
Edit a file 'local.yml'

```bash
nano local.yml
```

```yml
---
- hosts: localhost
  connection: local
  become: true
  
  tasks:
  - name: Install htop
    apt:
      name: htop
```



