Role - QS Secure Shell (SSH) Configuration
=========

This role configures SSH against Linux information systems.    

Applicability: RHEL-based distributions >= 7 and Ubuntu >= 18.04

It performs the following:
 
* Backs up the current /etc/ssh/sshd_config file (for legacy reference purposes).
* Provides the Quantum Space IT Consent Banner file to /etc/issue.
* Configures sshd_config parameters in the vars/main.yml and applies them to the applicable Jinja (.j2) templates.  Copies templates to the target as the new sshd_config file.
* Restarts the secure shell service.

Requirements
------------
Git is required to perform any cloning commands.

Local Ansible install is also required in order to locally perform 'ansible-playbook' or 'ansible-pull' commands against the target - https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html.

Role Variables
--------------

See the vars/main.yml file for variables defined against this role.

Invoking the Role
----------------

 *Repo Clone and Run Locally*

**git clone https://github.com/damonchandler/ansible.git (HTTP)**

**git clone git@github.com:damonchandler/ansible.git (SSH)**

**ansible-playbook -c local -i localhost, qs_ssh/qs_ssh.yml**

*Ansible Pull*

**ansible-pull -U https://github.com/damonchandler/ansible.git -c local -i localhost, qs_ssh/qs_ssh.yml** 

*Ansible Tower/AWX*

There is a Job Template in the QS Ansible solution that deploys this role against Quantum Space IT's target inventory and credentials - **QS SSH Configuration**.

Author Information
------------------

Damon Chandler
    
damon.chandler@quantumspace.us