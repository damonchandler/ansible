Role - Quantum Space Baseline Remediation Configuration
=========

This role configures additional CIS parameters against RHEL-based distributions >= 7 and Ubuntu >= 18.04.  Configures the following:

*Ubuntu* 

    Verify Permissions on gshadow File 
    Verify Permissions on shadow File 
    Disable Mounting of cramfs 
    Disable DCCP Support 
    Disable Mounting of freevxfs 
    Disable Mounting of hfs 
    Disable Mounting of hfsplus 
    Disable Mounting of jffs2 
    Disable SCTP Support 
    Disable Mounting of squashfs 
    Disable Mounting of udf 
    Disallow Direct root Logins  
    Remove telnet Clients 
    Disable Kernel Parameter for Accepting Secure Redirects for All Interfaces 
    Disable Kernel Parameter for Accepting Secure Redirects By Default 
    Disable Kernel Parameter for Sending ICMP Redirects for All Interfaces 
    Disable Kernel Parameter for Accepting ICMP Redirects By Default 
    Disable Kernel Parameter for Accepting Source-Routed Packets By Default 
    Disable Kernel Parameter for Sending ICMP Redirects by Default 
    Disable Accepting IPv6 Redirects By Default 
    Disable Accepting IPv6 Router Advertisements 
    Disable Accepting IPv6 Redirects By Default
    Disable Ctrl-Alt-Del Reboot Activation
    Disable Ctrl-Alt-Del Burst Action

*RHEL/CentOS/OLE/Scientific Linux*

    Disable Mounting of cramfs 
    Disable DCCP Support 
    Disable Mounting of freevxfs 
    Disable Mounting of hfs 
    Disable Mounting of hfsplus 
    Disable Mounting of jffs2 
    Disable SCTP Support 
    Disable Mounting of squashfs 
    Disable Mounting of udf 
    Disallow Direct root Logins 
    Remove telnet Clients 
    Disable Kernel Parameter for Accepting Secure Redirects for All Interfaces 
    Disable Kernel Parameter for Accepting Secure Redirects By Default 
    Disable Kernel Parameter for Sending ICMP Redirects for All Interfaces 
    Disable Kernel Parameter for Accepting ICMP Redirects By Default 
    Disable Kernel Parameter for Accepting Source-Routed Packets By Default 
    Disable Kernel Parameter for Sending ICMP Redirects by Default 
    Disable Accepting IPv6 Redirects By Default 
    Disable Accepting IPv6 Router Advertisements 
    Disable Accepting IPv6 Redirects By Default 
    Disable Ctrl-Alt-Del Reboot Activation
    Disable Ctrl-Alt-Del Burst Action

Requirements
------------
Git is required to perform any cloning commands.

Ansible install is also required in order to locally perform 'ansible-playbook' or 'ansible-pull' commands against the target.

Python APT and DNF modules are also required for uninstall of packages defined in the role.

Role Variables
--------------

Several variables exist in this role that create the corresponding files or place data in files that already exist.  See the vars/main.yml for all directory and file/configuration assumptions used in this case. The vars/RHEL.yml file is not used in this case and is present for fidelity, but may be used if the role is modified to require specific configurations/parameters.

Tags
----------------

Ansible tagging is integrated in the tasks/main.yml in order to enforce collective deployments (--tags) or skipping (--skip-tags) of role aspects:

    rhel_remediation - Applies or skips deployments applicable to RHEL-based distributions.
    ubuntu_remediation - Applies or skips deployments applicable to Ubuntu.

Invoking the Role
----------------

This role can be deployed in several ways:

*Repo Clone and Run Locally*

**git clone https://github.com/damonchandler/ansible.git (HTTP)** 

**git clone git@github.com:damonchandler/ansible.git (SSH)**

**ansible-playbook -c local -i localhost, qs_baseline_remediation/qs_baseline_remediation.yml**

*Ansible Pull*

**ansible-pull -U https://github.com/damonchandler/ansible.git -c local -i localhost, qs_baseline_remediation/qs_baseline_remediation.yml**

*AWX/Ansible Tower*

If you have access to the QS Ansible Tower/AWX instance, this role is updated as a universal Job Template (Resources >> Templates): **QS Baseline Remediation**.  It can be run against the target project's self-integrated inventory with the user's declared machine credentials/SSH keys.  

Author Information
------------------

Damon Chandler
    
damon.chandler@quantumspace.us