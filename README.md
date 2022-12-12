# ansible-demo

This repository contains notes, runbooks for ansible

## What is Ansible?
Ansible is a radically simple IT automation system. It handles configuration management, application deployment, cloud provisioning, ad-hoc task execution, network automation, and multi-node orchestration. Ansible makes complex changes like zero-downtime rolling updates with load balancers easy. 
* It is agentless; works on SSH

![Alt text](images/Ansible_provide_supports_for.png?raw=true "Ansible Supports")

### Design Principles
* Have an extremely simple setup process with a minimal learning curve.
* Manage machines quickly and in parallel.
* Avoid custom-agents and additional open ports, be agentless by leveraging the existing SSH daemon.
* Describe infrastructure in a language that is both machine and human friendly.
* Focus on security and easy auditability/review/rewriting of content.
* Manage new remote machines instantly, without bootstrapping any software.
* Allow module development in any dynamic language, not just Python.
* Be usable as non-root.
* Be the easiest IT automation system to use, ever.
![Alt text](images/Ansible_for_Containers.png?raw=true "Ansible for Containers")


### What problems does Ansible solves for us?
* Human Error
* A lack of Transparency
* A lack of Repeatability
* Documentation
* Portability
* Saves lots of time

### Prerequisites
* Python and pip should be installed

### Installation on Linux or Mac
```
sudo pip install ansible
```

Verify the installation
```
ansible --version
```

### Create SSH Key on Linux/Mac
```
ssh-keygen
```

Copy the public key (.pub file) to create SSH Key in Cloud Provider

## Inventory 
* It contains all the system addresses
  - can be hostnames or IPs
* Groups for organising systems
* Can be a file
* Can be provided on the CLI
* or generated dynamically

## SSH Keys
* Log into the ansible master machine (where ansible is installed)
* Copy the .pem file of the machine to connect to
* Execute the following commands to add the SSH Identity
```
ssh-agent bash
cp <key_name>.pem ~/.ssh/
ssh-add ~/.ssh/<key_name>.pem
```

### Disable Host Key Checking to avoid manual intervention
```
export ANSIBLE_HOST_KEY_CHECKING=False
```
or
Uncomment 'host_key_checking' in /etc/ansible/ansible.cfg

## YAML

### Multiple line statements in YAML
#### Literal Block Scalar (|)
It preserves the nextline '\n'
e.g
```
process: |
        This is line 1
        This is line 2
        This is line 3
```
The corresponding JSON output is:
```
{
  "process": "This is line 1\nThis is line 2\nThis is line 3\n"
}
```
#### Folder Block Scalar (>)
e.g
```
process: >
        This is line 1
        This is line 2
        This is line 3
```
The corresponding JSON output is:
```
{
  "process": "This is line 1 This is line 2 This is line 3\n"
}
```

### Comments in YAML
* Comments starts with #

### Quotes in YAML
* **Single Quotes ('')** - Prints the text as it is
* **Double Quotes ("")** - You can use escape \, also variables are expanded to original value

### Expressions\Variables in YAML
* Add your variable in "{{}}"
e.g file_path: "{{ variable }}"

## Ansible Modules
![Alt text](images/Ansible_Modules.png?raw=true "Ansible Modules")

### What is an Ansbile Module?
![Alt text](images/AnsibleModule.png?raw=true "What is an Ansible Module?")

![Alt text](images/Command_to_Yaml.png?raw=true "What is an Ansible Module?")

![Alt text](images/Ansible_Modules_List.png?raw=true "Ansible Modules List")

### Command Module
![Alt text](images/Command_Module_Example.png?raw=true "Command Module Example")

### Expect Module
![Alt text](images/Expect_Module_Example.png?raw=true "Expect Module Example")

### Expect Module
![Alt text](images/PSExec_Module_Example.png?raw=true "PSExec Module Example")

### RAW Module
![Alt text](images/RAW_Module_Example.png?raw=true "RAW Module Example")

### Script Module
![Alt text](images/Script_Module_Example.png?raw=true "Script Module Example")

### Telnet Module
![Alt text](images/Telnet_Module_Example.png?raw=true "Telnet Module Example")

## Variables in Ansible
![Alt text](images/Ansible_variables.png?raw=true "Variables in Ansible")

### Defining Variables
![Alt text](images/Defining_Variables.png?raw=true "Defining Variables")

### Multi-Value Variables
![Alt text](images/Multi_value_variables.png?raw=true "Multi-Value Variables")

### Register Variables
![Alt text](images/Register_variables.png?raw=true "Register Variables")

### Variable File
![Alt text](images/Variable_file.png?raw=true "Variable File")

### Group Variables
![Alt text](images/Group_Variables.png?raw=true "Group Variables")

### Host Variables
![Alt text](images/Host_Variables.png?raw=true "Host Variables")

### Runtime Variables
![Alt text](images/Runtime_Variables.png?raw=true "Runtime Variables")

## Playbook Execution
![Alt text](images/Playbook_execution.png?raw=true "Playbook Execution")

## Playbook Examples
### Install Nginx
```
ansible-playbook -i inventory/inventory.ini playbooks/install_nginx.yaml -v
```

# References
Pythoholic - https://www.youtube.com/watch?v=MNGfPn0Yvs8
Michael Crilly - https://www.youtube.com/playlist?list=PL0yQYCnvTmOv7ctKBb66YQx11NrQPWSrx