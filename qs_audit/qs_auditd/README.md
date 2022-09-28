Role - Auditd Configuration for Linux Systems
=========

This role configures auditd (RHEL-based distributions >= 7 and Ubuntu >= 18.04) based on CIS guidelines. It performs the following:

* Assumes use of augenrules for aggregation of the /etc/audit/audit.rules against target individual *.rules files in /etc/audit/rules.d/.  Defines the following:
    * access_rules.rules
    * audit.rules
    * audit_time_rules.rules
    * file_deletion_events.rules
    * immutable.rules
    * kernel_module_loading.rules
    * mac_modification.rules
    * networkconfig_modification.rules
    * privileged_commands.rules
    * sysadmin_actions.rules
    * unsuccessful-create.rules
    * unsuccessful-delete.rules
    * unsuccessful-modification.rules
    * unsuccessful-perm-change.rules
    * usergroup_modification_rules.rules
* Adds the 'audit=1' flag to /etc/default/grub/ under the GRUB_CMDLINE_LINUX parameter.  
* Configures the /etc/audit/auditd.conf with OS-based parameters.  
* Backs up the current in place /etc/audit/rules.d/ directory (as /etc/audit/rules.d.bak/) as to not overwrite any custom rules that may need to be placed back into the target system configuration or may need to be referenced for legacy purposes.
* Reloads the audit rules (RHEL-based) or restarts the auditd service via systemctl (Ubuntu).

Requirements
------------
Git is required to perform any cloning commands.

The main requisite for this role - auditd - is assumed to be preinstalled (RHEL-based) or installed using the corresponding module (yum/apt) in the install_auditd.yml task.  Ansible install is also required in order to locally perform 'ansible-playbook' or 'ansible-pull' commands against the target.

Role Variables
--------------

Several variables exist in this role that create the corresponding files and places them where they need to go in the /etc/audit/ directory.  See the vars/main.yml for all directory and file/configuration assumptions used in this case. 

Tags
----------------

Ansible tagging is now integrated in the tasks/main.yml in order to enforce collective deployments (--tags) or skipping (--skip-tags) of role aspects:

    rhel_audit - Used in tandem with the tasks/QS_RHEL.yml role component.
    ubuntu_audit - Used in tandem with the tasks/QS_UBuntu.yml role component.

Invoking the Role
----------------

This role can be deployed in several ways:

*Repo Clone and Run Locally*

**git clone https://github.com/damonchandler/ansible.git (HTTP)** 

**git clone git@github.com:damonchandler/ansible.git (SSH)**

**ansible-playbook -c local -i localhost, qs_auditd/qs_auditd.yml**

*Ansible Pull*

**ansible-pull -U https://github.com/damonchandler/ansible.git -c local -i localhost, qs_auditd/qs_auditd.yml**

*AWX/Ansible Tower*

If you have access to the Ansible Tower/AWX instance, this role is updated as a universal Job Template (Resources >> Templates) as **QS Auditd Configuration**.  It can be run as against the target project's self-integrated inventory with the user's declared machine credentials/SSH keys.  

Author Information
------------------

Damon Chandler
    
damon.chandler@quantumspace.us