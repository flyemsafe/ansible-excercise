# Enable remote execution on Windows

## Option A
[Use this tool from SolarWinds] (http://www.solarwinds.com/products/freetools/remote-execution-enabler-for-powershell.aspx)

## Option B
[Use the Ansible provided PowerShell Script] (https://raw.githubusercontent.com/ansible/ansible/devel/examples/scripts/ConfigureRemotingForAnsible.ps1
)
```
powershell.exe  -ExecutionPolicy Bypass -File ConfigureRemotingForAnsible.ps1 -CertValidityDays 3650 -Verbose
```

# Setup Control Node

Install ansible
```
yum install epel-release
yum install ansible
yum install python2-winrm
```

We need python2-winrim 

_Option A_

```
yum install python2-winrim 
```
*OR*

_Option B_

```
pip install "pywinrm>=0.2.2"
```

## Setup Inventory

```
mkdir ansible-workshop
cd ansible-workshop
mkdir {roles,inventory,host_vars,group_vars}
touch host_vars/<linux_host>
touch host_var/<windows_host>
touch group_vars/linux
touch group_vars/windows
touch group_vars/drupal
touch group_vars/iis
touch ansible.cfg
```
## Setup ansible.cfg

```
[defaults]
inventory      = <FILLIN>/ansible-workshop/inventory
gathering = smart
roles_path    = <FILLIN>/ansible-workshop/roles
remote_user = root
#private_key_file = 
#vault_password_file = 
ansible_managed = Ansible managed: {file} modified on %Y-%m-%d %H:%M:%S by {uid} on {host}
[privilege_escalation]
[paramiko_connection]
[ssh_connection]
pipelining = True
scp_if_ssh = True
[persistent_connection]
connect_timeout = 30
connect_retries = 30
connect_interval = 1
[accelerate]
[selinux]
[colors]
[diff]

```

# Windows Connection vars

## vars

```
ansible_user: 'localAdminUser'
ansible_password: 'P455w0rd'
ansible_connection: 'winrm'
ansible_port: 5986
ansible_winrm_server_cert_validation: 'ignore'
```

# Linux Connection Vars

```
ansible_user: ec2-user
ansible_ssh_private_key_file: /path/to/aws/pem/aws-personal.pem
```

# Playbooks

## Check if host is windows
```
---
- hosts: all
  
  tasks:
    - fail:
        msg: "This is not a Windows system"
      when: ansible_os_family != "Windows"
```
      "
