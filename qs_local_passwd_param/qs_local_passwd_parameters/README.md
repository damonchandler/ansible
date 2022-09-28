Role - QS Local Password Parameters Implementation
=========

This role applies local (pam.d) password parameters against RHEL-based distributions >= 7 and Ubuntu >= 16.04.  It applies the following:

* Applies parameters to the /etc/login.defs file.
* Applies parameters to the /etc/security/pwquality.conf file.
* Installs libpam-cracklib in Ubuntu so that pam_cracklib.so exists.
* In Ubuntu, applies pam configurations to the /etc/pam.d/common-password, common-auth, and common-account files.
* In RHEL/CentOS, applies pam configurations to the /etc/pam.d/system-auth and password-auth files.

End result:
 
* Local password parameters will be set for a 60 day expiry/14 day warn age/1 day before password can be changed/24 passwords remembered against local accounts.
* Password locks for 15 minutes after 5 failed input attempts (RHEL-based distributions uses faillock; Ubuntu uses pam_tally2).  Both faillock and pam_tally2 reset the counts to zero after a successful login is established. 
* Password credits are set with: 
    * Minimum length: 12 
    * Other credit: at least 1 (-1)
    * Upper-case credit: at least 1 (-1)
    * Lower-case credit: at least 1 (-1)
    * Digit (numeric) credit: at least 1 (-1) 
* Enforcement of local accounts are in line with QS Azure Active Directory policies.

Note
------------

Accounts on the system prior to this role deployment will have default parameters integrated into the configuration.  Running the following command as root or with sudo will align the account accordingly:

**chage -M 60 -m 1 -W 14 [account]**

Accounts created after successful execution and configuration will be afforded the adjusted parameters.

Requirements
------------
Git is required to perform any cloning commands.

Local Ansible install is also required in order to locally perform 'ansible-playbook' or 'ansible-pull' commands against the target - https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html.

Role Variables
--------------

See the vars/main.yml file for variables defined against this role.

Tags
----------------

Ansible tagging is now integrated in the tasks/main.yml in order to enforce collective deployments (--tags) or skipping (--skip-tags) of role aspects:
    
    logindefs_pwquality - Only applies configurations against the /etc/login.defs and /etc/security/pwquality.conf files.
    ubuntu_pamd - Invokes the pamd module configurations for Ubuntu.
    rhel7_pamd - Invokes the pamd module configurations for RHEL-based 7.
    rhel8_pamd - Invokes the pamd module configurations for RHEL-based 8.

Invoking the Role
----------------

 *Repo Clone and Run Locally*

**git clone https://github.com/damonchandler/ansible.git (HTTP)**

**git clone git@github.com:damonchandler/ansible.git (SSH)**

**ansible-playbook -c local -i localhost, qs_local_passwd_param/qs_local_passwd_parameters.yml**

*Ansible Pull*

**ansible-pull -U https://github.com/damonchandler/ansible.git -c local -i localhost, fpd_local_passwd_parameters.yml** 

*Ansible Tower/AWX*

There is a Job Template in the QS Ansible solution that deploys this role against target inventory and credentials - **QS Local Password Parameters**.

Author Information
------------------

Damon Chandler
    
damon.chandler@quantumspace.us