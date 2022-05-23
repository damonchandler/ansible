Role - GES Secure Shell (SSH) Configuration
=========

This role configures SSH against Linux information systems.    

Applicability: RHEL-based distributions >= 7 and Ubuntu >= 16.04

It performs the following:
 
* Backs up the current /etc/ssh/sshd_config file (for legacy reference purposes).
* Provides the Genesis IT Consent Banner file to /etc/issue.
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

**git clone https://developer.nasa.gov/FPD-Ansible/fpd_ssh (HTTP)**

**git clone git@developer.nasa.gov:FPD-Ansible/fpd_ssh (SSH)**

**ansible-playbook -c local -i localhost, fpd_ssh/fpd_ssh.yml**

*Ansible Pull*

**ansible-pull -U https://developer.nasa.gov/FPD-Ansible/fpd_ssh -c local -i localhost, fpd_ssh.yml** 

*Ansible Tower/AWX*

There is a Job Template in the directorate-level Ansible solution that deploys this role against FPD IT Security's target inventory and credentials - FPD SSH Configuration.

Author Information
------------------

Damon Chandler
    
dchandler@genesisesi.com