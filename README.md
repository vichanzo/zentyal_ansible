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
  - name: Add key for Zentyal 7.1
    ansible.builtin.get_url:
      url: http://keys.zentyal.org/zentyal-7.1-packages-org.asc
      dest: /etc/apt/trusted.gpg.d/zentyal.asc
      mode: '0644'
      force: true

  - name: Add repo for Zentyal 7.1
    ansible.builtin.apt_repository:
      repo: deb http://packages.zentyal.org/zentyal 7.1 main extra
      state: present

  - name: Installing Zentyal 7.1
    apt:
      name:
        - zentyal
      state: latest
      force_apt_get: true
      update_cache: true

```



