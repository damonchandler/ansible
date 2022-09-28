Role - Gnome 3/GDM Configuration of the Login with Quantum Space IT Consent Banner
=========

This role configures the Gnome 3 (GDM) login interface on QS informations systems according to the following:

* Creates the required /etc/dconf/db/gdm.d/ directory in Ubuntu.  This directory already exists in RHEL-based distributions.
* Creates the /etc/dconf/db/gdm.d/locks/ directory.
* Creates the /etc/dconf/db/local.d/ directory.
* Creates the /etc/dconf/db/local.d/locks/ directory.
* Modifies the [daemon] parameters in /etc/gdm/custom.conf (RHEL-based) and /etc/gdm3/custom.conf (Ubuntu).
* Places in the /etc/dconf/profile/gdm file.
* Places in the /etc/dconf/profile/user file.
* Places in the /etc/dconf/db/gdm.d/00-qs file.
* Places in the /etc/dconf/db/gdm.d/locks/00-qs file.
* Places in the /etc/donf/db/local.d/00-qs file.
* Places in the /etc/dconf/db/local.d/locks/00-qs.

To satisfy the following Parameters:

* Disable Automatic Login
* Disable Ctrl-Alt-Del Reboot Key Sequence in GUI
* Disable GUI Guest Login
* Ensure Display Manager Banner is Enabled
* Ensure Display Manager Provides the Proper Message Banner
* Set the Login Number of Failures to the GUI Display Manager
* Enable Screen Lock
* Enable Screen Lock Idle Delay

**End result: The system login will show a disabled user list (input for user name and password) with the QS IT Consent Banner on the screen.**

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

**git clone https://github.com/damonchandler/ansible.git (HTTP)**

**git clone git@github.com:damonchandler/ansible.git (SSH)**

**ansible-playbook -c local -i localhost, qs_gdm/qs_gdm_banner.yml**

*Ansible Pull*

**ansible-pull -U https://github.com/damonchandler/ansible.git -c local -i localhost, qs_gdm/qs_gdm_banner.yml** 

*Ansible Tower/AWX*

There is a Job Template in the QS Ansible solution that deploys this role against the Org's target inventory and credentials - QS Enforce GDM Banner (Gnome 3).

Author Information
------------------

Damon Chandler
    
damon.chandler@quantumspace.us