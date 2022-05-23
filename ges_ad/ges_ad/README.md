Role - HFCS Linux NCAD Posturing
=========

This role installs all required packages and configures a Linux target for binding to the NASA Consolidated Active DIrectory (NCAD) domain - RHEL-based distributions >= 7.

It does the following:

_RHEL 7-based_

* Installs the required packages - krb5-libs, krb5-workstation, sssd, oddjob-mkhomedir, realmd, adcli, and samba-common-tools.
* Modifies the /etc/hosts file with mapping of the '127.0.0.1' entry to both short name and FQDN.
* Copies in the /etc/sssd/sssd.conf file (root:root 0600).
* Copies in the /etc/samba/smb.conf file (root:root 0644).
* Copies in the /etc/krb5.conf file (root:root 0644).
* Creates the /home/NDC directory (0755).
* Runs the 'authconfig --enablesssd --enablesssdauth --enablemkhomedir --update' command to map the proper parameters in PAM.

_RHEL 8-based_

* Installs required packages - krb5-libs, krb5-workstation, sssd, oddjob-mkhomedir, realmd, adcli, and samba-common-tools.
* Modifies the /etc/hosts file with mapping of the '127.0.0.1' entry to both short name and FQDN.
* Copies in the /etc/sssd/sssd.conf file (root:root 0600).
* Copies in the /etc/samba/smb.conf file (root:root 0640).
* Modifies the /etc/oddjobd.conf.d/oddjob-mkhomedir.conf file with the right permission to map to NCAD user home directories created under /home/NDC/ (0077).
* Adjusts the /etc/authselect/user-nsswitch.conf parameters (root:root 0644).
* Runs the 'authselect apply-changes' command.
* Copies in the /etc/krb5.conf file (root:root 0644)
* Creates the /home/NDC directory (0755).
* Runs the 'authselect select sssd' command.
* Runs the 'authselect enable-feature with-mkhomedir' command.

**This role only provisions the configuration.  There are still steps that require manual intervention in line with other client binding strategies.  These include:**

* Creating the object in ICAM DRA.
* Running the 'net ads join -U [username set in DRA]' command to bind the system to the DRA object.
* Running the 'sudo systemctl enable sssd oddjobd' command.
* Running the 'sudo systemctl restart sssd oddjobd' command.
* Rebooting the client system.

Requirements
------------
Git is required to perform any cloning commands.

The scope of the installation requirements are satisfied inside of the role configuration.

Local Ansible install is also required in order to locally perform 'ansible-playbook' or 'ansible-pull' commands against the target - https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html.

It is suggested to run the following Ansible roles in tandem with or as a part of the NCAD posturing process.

[hfcs_gdm]()

[hfcs_nasa_trust_import]()

[hfcs_network_time]()

Role Variables
--------------

Variables exist in this role that copy and store the corresponding files, places them within the OS configuration or installs the required packages for each distribution type.

    vars/main.yml - is only used to map the ad_access_group (mapped the the ad_access_filer option in the /etc/sssd/sssd.conf file) variable to the default HFCSadmin user OU (memberOf=cn=GS-GG-GSFPD06-HFCSadmin,ou=GSFPD06Groups,ou=GSFPD06,ou=GS,dc=ndc,dc=nasa,dc=gov)
    vars/RedHat.yml

Tags
----------------

Ansible tagging is integrated in the tasks/main.yml in order to enforce collective deployments (--tags) or skipping (--skip-tags) of role aspects:

    rhel7_ncad - postures any RHEL 7-based system for NCAD binding
    rhel8_ncad - postures any RHEL 8-based system for NCAD binding

Invoking the Role
----------------

*Repo Clone and Run Locally*

**git clone https://gs408-grays.ndc.nasa.gov/sysadmin.hfcs/ansible.git (HTTP)** 

**git clone git@gs408-grays.ndc.nasa.gov:sysadmin.hfcs/ansible.git (SSH)**

**ansible-playbook -c local -i localhost, ansible/hfcs_ncad/hfcs_ncad.yml -K**

*Ansible Pull*

**ansible-pull -U https://gs408-grays.ndc.nasa.gov/sysadmin.hfcs/ansible.git -c local -i localhost, hfcs_ncad/hfcs_ncad.yml -K** 

*Ansible Tower/AWX*

There is a Job Template in the HFCS Ansible solution that deploys this role against the Org's target inventory and credentials - **HFCS Linux NCAD Posturing**.  Ansible tagging can be selected while grooming the workflow for run against targets using the **Job Tags** or **Skip Tags** prompt.

Author Information
------------------

Damon Chandler
    
damon.i.chandler@nasa.gov