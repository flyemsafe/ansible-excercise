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
``

## Setup Inventory

```
mkdir ansible-workshop
cd ansible-workshop
mkdir {roles,inventory()}
touch ansible.cfg
```
*ansible.cfg*

# Everything from this point is just raws notes
# ----------------------------------------------

## vars
ansible_user: 'localAdminUser'
ansible_password: 'P455w0rd'
ansible_connection: 'winrm'
ansible_port: 5986
ansible_winrm_server_cert_validation: 'ignore'


ansible_user: administrator
ansible_password: <password>
ansible_port: 5985
ansible_connection: winrm
ansible_winrm_scheme: http
ansible_winrm_server_cert_validation: ignor

