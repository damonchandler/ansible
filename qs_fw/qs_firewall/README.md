Role - QS Firewall (Uncomplicated Firewall and FirewallD) Configuration Against Linux Information Systems
=========

This role configures the application firewall (Uncomplicated Firewall/UFW for Ubuntu >= 18.04; FirewallD for RHEL-based distributions >= 7) on QS informations systems according to the following:

* Ensures inbound access is restricted to SSH (22/tcp).  Applies this rule against the default FirewallD profile.
* Ensures all outbound access is allowed.
* Restarts the respective service.

**This roles does not account for any IPTables implementation since that application-based firewall is defaulted in older Linux operating systems.** 

Requirements
------------
Git is required to perform any cloning commands.

The application-based firewall is generally installed by default in the chosen Linux targets.  The roles does also perform an install task (using the yum or apt modules) in the event that the chosen distribution does not otherwise have the application (and all dependencies) installed.

Local Ansible install is also required in order to locally perform 'ansible-playbook' or 'ansible-pull' commands against the target - https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html.

Tags
----------------

Ansible tagging is now integrated in the tasks/main.yml in order to enforce collective deployments (--tags) or skipping (--skip-tags) of role aspects:

    rhel_fw - Used in tandem with the tasks/configure_firewalld.yml role component.
    ubuntu_fw - Used in tandem with the tasks/configure_ufw.yml role component.

Invoking the Role
----------------

*Repo Clone and Run Locally*

**git clone https://github.com/damonchandler/ansible.git (HTTP)**

**git clone git@github.com:damonchandler/ansible.git (SSH)**

**ansible-playbook -c local -i localhost, qs_fw/qs_firewall.yml**

*Ansible Pull*

**ansible-pull -U https://github.com/damonchandler/ansible.git -c local -i localhost, qs_fw/qs_firewall.yml** 

*Ansible Tower/AWX*

There is a Job Template in the directorate-level Ansible solution that deploys this role against the Org's target inventory and credentials - **QS Firewall Configuration**.

Author Information
------------------

Damon Chandler
    
damon.chandler@quantumspace.us