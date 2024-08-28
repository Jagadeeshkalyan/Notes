Configuration Management is a way How DevOps Engineer manage the configuration the servers or configuration of the infrastructure.
On-premise challenges:
1. upgrades
2. secure patches 
3. Default installations

on Cloud Challenges:
1. 1000 servers - managing configuration is very difficult

- Ansible is a push mechanism model where as chef and puppet are pull mechanism model.
if you want to install any packages to the multiple servers, you can witre a ansible playbook on one server ans push it all the servers.
- Ansible uses a agent less model
- write IP address of the servers or DNS of the servers in an Inventory file and have the password less authentication enabled

The master/Control-M server where we write ansible playbook should be able connect to the all servers without any passowords.


Dynamic Inventory: Ansible is capable to auto-detect the server.

- Ansbile playbook written in python language but we write playbooks in yaml format.

- we can write our own moduels in Ansible.

Ansible Galaxy:
we can share the modules, using Ansible Galaxy, we can create our own modules too.

1. What is the language use Ansible
- Ansbile written in python language and we can write our own modules using Python
2. Does Ansible support both Linux and Windows?
- Yes. it supports both. Linux uses a protocal called SSH and Windows uses a protocal called WinRm to connect Windows.
3. Diff between puppet/chef and Ansible?
- 
4. Is push or pull mechanism?

Install Ansible: (Ubuntu)
apt update
apt install ansible
ansible --version   - verify the version

generae a ssh key pair (public and private keys) on Ansible server and add the content of id_rsa.pub to the authorized_keys of traget servers to communicate with each other without password authentication.

ssh-keygen 

Playbook:
Ansible palybook is nothing but Ansible files which required to execute ansible commands
- Sometimes we run ansible adhoc commands instead of writing Ansible playbook all the times.

Inventory file:
- A file where we store the IP addressess of the remote or target servers.
- Default location of the inventory file is /etc/ansible/hosts

Ad-hoc command: to run a single or simple tasks, we run ansible ad-hoc commands.
- ansible -i inventory all -m "shell" -a "touch testfile"

. -m: Module
. -a: arguments to be passed

- Group of the servers in inventory file
    - when you run a specific command/playbook on particular servers, make a group of servers in the inventory file.

    eg.
    [webservers]
    10.2.43.76

    [dbservers]
    10.4.67.34
 
 ansible -i inventory webservers -m "shell" -a "touch testfile"

Playbook: to run/execute set of commands, use Ansible playbook

