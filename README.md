# Ansible Setup

Create a master, and two slave VM's.

On master, switch to root  
`sudo su -`  
`apt-get install ansible`  
`ansible --version`

Change network adapter on master node to "Bridged."

Playbooks: Specific set of tasks to do something to an environment you specify.  
Roles: Fully self contained packages that include tasks, variables, config files, etc.  
Modules: Does the heavy lifting, implemented in languages such as Python and Powershell.

Set slave network adapters to "Bridged."

Slave-1: 10.1.1.169  
Slave-2: 10.1.1.169

Check master can ping both of these.

Add the following lines:

`
[web]
10.1.1.169
`

## Set up SSH keys on each VM
`ssh-keygen`
`ssh-copy-id -i <location of id_rsa.pub> <ip-address of host>`

On master:
`ansible web -m ping`

Should get response like:

`10.1.1.169 | success > > {     
    "changed": false,  
    "ping": "pong"  
}  
`
Call run the ansible module 'date', across all the hosts associated with the web group, will get the time that's set on each of these machines.

`ansible web -a /bin/date`

Check packages are up to date (yum on Redhat, apt on Debian-based systems)
`ansible web -s -m apt -a "name=openssl state=latest"`

Run playbooks with:
`ansible-playbook playbook.yaml`



