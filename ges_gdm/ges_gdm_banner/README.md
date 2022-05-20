Role - Gnome 3/GDM Configuration of the Login with IT Consent Banner
=========

This role configures the Gnome 3 (GDM) login interface on FPD informations systems according to the following:

* Creates the required /etc/dconf/db/gdm.d/ directory in Ubuntu.  This directory already exists in RHEL-based distributions.
* Creates the /etc/dconf/db/gdm.d/locks/ directory.
* Creates the /etc/dconf/db/local.d/ directory.
* Creates the /etc/dconf/db/local.d/locks/ directory.
* Modifies the [daemon] parameters in /etc/gdm/custom.conf (RHEL-based) and /etc/gdm3/custom.conf (Ubuntu).
* Places in the /etc/dconf/profile/gdm file.
* Places in the /etc/dconf/profile/user file.
* Places in the /etc/dconf/db/gdm.d/00-nasa file.
* Places in the /etc/dconf/db/gdm.d/locls/00-nasa file.
* Places in the /etc/donf/db/local.d/00-nasa file.
* Places in the /etc/dconf/db/local.d/locks/00-nasa.

To satisfy the following ASCS Parameters:

* NASA-ASCS-40558: Disable Automatic Login
* NASA-ASCS-40561: Disable Ctrl-Alt-Del Reboot Key Sequence in GUI
* NASA-ASCS-40562: Disable GUI Guest Login
* NASA-ASCS-40565: Ensure Display Manager Banner is Enabled
* NASA-ASCS-40566: Ensure Display Manager Provides the Proper Message Banner
* NASA-ASCS-40567: Set the Login Number of Failures to the GUI Display Manager
* NASA-ASCS-40568: Enable Screen Lock
* NASA-ASCS-40569:Enable Screen Lock Idle Delay

**End result: The system login will show a disabled user list (input for user name and password) with the NASA IT Consent Banner on the screen.**

Requirements
------------
Git is required to perform any cloning commands.

The system must have Gnome 3/GDM installed in order to succeed.  The interface does not have to be running, but installed.  This is not an applicable configuration item for systems configured without a GUI (i.e. server implementations of Ubuntu/CentOS/RHEL).  GUI configuration can be modified with the following commands:

*systemctl set-default multi-user.target* (sets the system to start without GUI)

*systemctl set-default graphical.target* (sets system to start with GUI)

Local Ansible install is also required in order to locally perform 'ansible-playbook' or 'ansible-pull' commands against the target - https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html.

Tags
----------------

Ansible tagging is now integrated in the tasks/main.yml in order to enforce collective deployments (--tags) or skipping (--skip-tags) of role aspects:

    rhel_gdm - Used to apply configuration changes against Gnome 3/GDM in RHEL-based distributions.
    ubuntu_gdm - Used to apply configuration changes against Gnome 3/GDM in Ubuntu.
    
Invoking the Role
----------------

*Repo Clone and Run Locally*

**git clone https://developer.nasa.gov/FPD-Ansible/fpd_gdm (HTTP)**

**git clone git@developer.nasa.gov:FPD-Ansible/fpd_gdm (SSH)**

**ansible-playbook -c local -i localhost, fpd_gdm/fpd_gdm_banner.yml**

*Ansible Pull*

**ansible-pull -U https://developer.nasa.gov/FPD-Ansible/fpd_gdm -c local -i localhost, fpd_gdm_banner.yml** 

*Ansible Tower/AWX*

There is a Job Template in the directorate-level Ansible solution that deploys this role against the Org's target inventory and credentials - FPD Enforce GDM Banner (Gnome 3).

Author Information
------------------

Damon Chandler
    
damon.i.chandler@nasa.gov
