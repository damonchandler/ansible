Role - Baseline Remediation Configuration
=========

This role configures additional ASCS parameters against RHEL-based distributions >= 7 and Ubuntu >= 18.04.  Configures the following:

*Ubuntu* 

    NASA-ASCS-20053: Verify Permissions on gshadow File 
    NASA-ASCS-20055: Verify Permissions on shadow File 
    NASA-ASCS-20061: Disable Mounting of cramfs 
    NASA-ASCS-20062: Disable DCCP Support 
    NASA-ASCS-20063: Disable Mounting of freevxfs 
    NASA-ASCS-20064: Disable Mounting of hfs 
    NASA-ASCS-20065: Disable Mounting of hfsplus 
    NASA-ASCS-20066: Disable Mounting of jffs2 
    NASA-ASCS-20067: Disable SCTP Support 
    NASA-ASCS-20068: Disable Mounting of squashfs 
    NASA-ASCS-20069: Disable Mounting of udf 
    NASA-ASCS-20012: Disallow Direct root Logins  
    NASA-ASCS-20085: Remove telnet Clients 
    NASA-ASCS-20112: Disable Kernel Parameter for Accepting Secure Redirects for All Interfaces 
    NASA-ASCS-20114: Disable Kernel Parameter for Accepting Secure Redirects By Default 
    NASA-ASCS-20192: Disable Kernel Parameter for Sending ICMP Redirects for All Interfaces 
    NASA-ASCS-20193: Disable Kernel Parameter for Accepting ICMP Redirects By Default 
    NASA-ASCS-20194: Disable Kernel Parameter for Accepting Source-Routed Packets By Default 
    NASA-ASCS-20195: Disable Kernel Parameter for Sending ICMP Redirects by Default 
    NASA-ASCS-20268: Disable Accepting IPv6 Redirects By Default 
    NASA-ASCS-20269: Disable Accepting IPv6 Router Advertisements 
    NASA-ASCS-20270: Disable Accepting IPv6 Redirects By Default
    NASA-ASCS-20364: Disable Ctrl-Alt-Del Reboot Activation
    NASA-ASCS-20365: Disable Ctrl-Alt-Del Burst Action

*RHEL/CentOS/OLE/Scientific Linux*

    NASA-ASCS-20061: Disable Mounting of cramfs 
    NASA-ASCS-20062: Disable DCCP Support 
    NASA-ASCS-20063: Disable Mounting of freevxfs 
    NASA-ASCS-20064: Disable Mounting of hfs 
    NASA-ASCS-20065: Disable Mounting of hfsplus 
    NASA-ASCS-20066: Disable Mounting of jffs2 
    NASA-ASCS-20067: Disable SCTP Support 
    NASA-ASCS-20068: Disable Mounting of squashfs 
    NASA-ASCS-20069: Disable Mounting of udf 
    NASA-ASCS-20012: Disallow Direct root Logins 
    NASA-ASCS-20085: Remove telnet Clients 
    NASA-ASCS-20112: Disable Kernel Parameter for Accepting Secure Redirects for All Interfaces 
    NASA-ASCS-20114: Disable Kernel Parameter for Accepting Secure Redirects By Default 
    NASA-ASCS-20192: Disable Kernel Parameter for Sending ICMP Redirects for All Interfaces 
    NASA-ASCS-20193: Disable Kernel Parameter for Accepting ICMP Redirects By Default 
    NASA-ASCS-20194: Disable Kernel Parameter for Accepting Source-Routed Packets By Default 
    NASA-ASCS-20195: Disable Kernel Parameter for Sending ICMP Redirects by Default 
    NASA-ASCS-20268: Disable Accepting IPv6 Redirects By Default 
    NASA-ASCS-20269: Disable Accepting IPv6 Router Advertisements 
    NASA-ASCS-20270: Disable Accepting IPv6 Redirects By Default 
    NASA-ASCS-20364: Disable Ctrl-Alt-Del Reboot Activation
    NASA-ASCS-20365: Disable Ctrl-Alt-Del Burst Action

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

**git clone https://developer.nasa.gov/FPD-Ansible/fpd_baseline_remediation (HTTP)** 

**git clone git@developer.nasa.gov:FPD-Ansible/fpd_baseline_remediation (SSH)**

**ansible-playbook -c local -i localhost, fpd_baseline_remediation/fpd_baseline_remediation.yml**

*Ansible Pull*

**ansible-pull -U https://developer.nasa.gov/FPD-Ansible/fpd_baseline_remediation -c local -i localhost, fpd_baseline_remediation.yml**

*AWX/Ansible Tower*

If you have access to the FPD Ansible Tower/AWX instance, this role is updated as a universal Job Template (Resources >> Templates): "FPD Baseline Remediation."  It can be run against the target project's self-integrated inventory with the user's declared machine credentials/SSH keys.  

Author Information
------------------

Damon Chandler
    
damon.i.chandler@nasa.gov
