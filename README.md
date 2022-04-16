# Ansible Scripts for Automations

![alt text](https://github.com/gil906/automation/docker/1_1Sgx9cqa-nCwva6aDYq9uQ.png?raw=true)

## Create an Ansible playbook to configure, provision, retrieve new Container IPs, and Update the Inventory file for future use


## Ansible Cisco Switch Backup
This is a playbook to backup cisco switch configuration, made to run on a daily base

## Execution Requirements
- Tested with Alma8
- Tested with Ansible 2.9, but keep in mind, that name of modules will change in later version

## Variables
  It is strongly recommended to protect the passwords in group_vars at least in a vault   
  https://github.com/joe-speedboat/workshop.ansible/blob/master/20%20Protect%20variables%20with%20vaults.md
* check ansible config for
  * vault settings    
  * group_vars

### The following variables may be overridden:
* `ansible_become_password`
* `ansible_password`
* `config_backup_dir_cisco`

## How to use
`ansible-playbook switchBackup.yml`

## Dependencies
* You need an existing git repo with deployment key    
  for the backup location: ```config_backup_dir_cisco```
* You need the ansible collections depending on your ansible version and device types:
  * https://docs.ansible.com/ansible/5/collections/community/network/
* With this command you can install the needed collections for this specific playbook int the project:
  ```ansible-galaxy collection install -r collections/requirements.yml -p collections/```

## License
https://opensource.org/licenses/LGPL-3.0    
Copyright (c) Chris Ruettimann <chris@bitbull.ch>  

## Inventory host_var example
```
ansible-inventory --list --vars
...snip...
            "fw-asa-01": {
                "ansible_become": true,
                "ansible_become_method": "enable",
                "ansible_become_password": "xxxxxx",
                "ansible_connection": "network_cli",
                "ansible_network_os": "asa",
                "ansible_password": "xxxxxx",
                "ansible_user": "admin",
                "config_backup_dir_cisco": "/etc/git/cisco_backup"
            },
            "switch-01": {
                "ansible_become": true,
                "ansible_become_method": "enable",
                "ansible_become_password": "xxxxxx",
                "ansible_connection": "network_cli",
                "ansible_network_os": "ios",
                "ansible_password": "xxxxxx",
                "ansible_user": "admin",
                "config_backup_dir_cisco": "/etc/git/cisco_backup"
            },
            "wlan-controller-01": {
                "ansible_become": false,
                "ansible_connection": "local",
                "ansible_network_os": "aireos",
                "ansible_password": "xxxxxx",
                "ansible_user": "admin",
                "config_backup_dir_cisco": "/etc/git/cisco_backup"
            }
...snip...
```

# Gitea diff hint
1. https://git.domain.local/TeamX/backup.cisco    
2. Branch > Tag > choose Date X (eg. 20210101)    
3. Choose Device Config (z.B. as-a-225-02_show_run.txt)    
   Now, device config for day X is showing up    
4. Click History    
   Now you see all possible versions of this file, which are older than X    
5. On column "Message" choose date Y (eg. 20201218)    
   Now you see the diff, "split view" option may help to compare the configs    




# Ansible-Playbooks-for-Cisco-IOS


Mission:

Ansible-Playbooks-for-Cisco-IOS is a repository of Ansible Playbooks for Cisco IOS devices.

To use, download the .zip and extract the contents or clone the repository by typing

```git clone https://github.com/gil906/ansible-playbooks-for-cisco-ios.git```



Your host vars should look something like this if you're using Ansible >= 2.5

```yaml


ansible_pass=foo
ansible_user=foo
ansible_network_os=ios
ansible_connection=network_cli

# If using an enable password add these

ansible_become_pass=foo
ansible_become=yes
ansible_become_method=enable


```

Here is a link to a blog explaining the changes that took place for Ansible 2.5

https://www.ansible.com/blog/coming-soon-networking-features-in-ansible-2.5





