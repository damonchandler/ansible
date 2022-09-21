Role - GES Linux NCAD Posturing
=========

This role installs all required packages and configures a Linux target for binding to the Genesis Active Directory (AD) domain - RHEL-based distributions >= 7 and Ubuntu >= 18.04.

It does the following:

_RHEL 7-based_

* Installs the required packages - krb5-libs, krb5-workstation, sssd, oddjob-mkhomedir, realmd, adcli, and samba-common-tools.
* Modifies the /etc/hosts file with mapping of the '127.0.0.1' entry to both short name and FQDN.
* Copies in the /etc/sssd/sssd.conf file (root:root 0600).
* Copies in the /etc/samba/smb.conf file (root:root 0644).
* Copies in the /etc/krb5.conf file (root:root 0644).
* Creates the /home/GES directory (0755).
* Runs the 'authconfig --enablesssd --enablesssdauth --enablemkhomedir --update' command to map the proper parameters in PAM.

_RHEL 8-based_

* Installs required packages - krb5-libs, krb5-workstation, sssd, oddjob-mkhomedir, realmd, adcli, and samba-common-tools.
* Modifies the /etc/hosts file with mapping of the '127.0.0.1' entry to both short name and FQDN.
* Copies in the /etc/sssd/sssd.conf file (root:root 0600).
* Copies in the /etc/samba/smb.conf file (root:root 0640).
* Modifies the /etc/oddjobd.conf.d/oddjob-mkhomedir.conf file with the right permission to map to AD user home directories created under /home/GES/ (0077).
* Adjusts the /etc/authselect/user-nsswitch.conf parameters (root:root 0644).
* Runs the 'authselect apply-changes' command.
* Copies in the /etc/krb5.conf file (root:root 0644).
* Creates the /home/GES directory (0755).
* Runs the 'authselect select sssd' command.
* Runs the 'authselect enable-feature with-mkhomedir' command.

_Ubuntu_

* Installs required packages - libnss-sss, libpam-sss, libsss-sudo, sssd, sssd-tools, adcli, samba-common, krb5-user, oddjob-mkhomedir.
* Modifies the /etc/hosts file with mapping of the '127.0.1.1' entry to both short name and FQDN.
* Copies in the /etc/sssd/sssd.conf file (root:root 0600).
* Copies in the /etc/samba/smb.conf file (root:root 0640).
* Copies in the /usr/share/pam-configs/mkhomedir file with the appropriate configuration to be aggregated into the /etc/pam.d/common-session file.
* Copies in the /etc/nsswitch.conf file.
* Copies in the /etc/krb5.conf file (root:root 0644).
* Creates the /home/GES directory (0755).
* Updates the PAM configuration.

**This role only provisions the configuration.  There are still steps that require manual intervention in line with other client binding strategies.  These include:**

* Running the 'net ads join -U [username] --no-dns-updates' command to bind the system to AD.
* Running the 'sudo systemctl enable sssd oddjobd' command.
* Running the 'sudo systemctl restart sssd oddjobd' command.
* Rebooting the client system.

Requirements
------------
Git is required to perform any cloning commands.

The scope of the installation requirements are satisfied inside of the role configuration.

Local Ansible install is also required in order to locally perform 'ansible-playbook' or 'ansible-pull' commands against the target - https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html.

It is suggested to run the following Ansible roles in tandem with or as a part of the NCAD posturing process.

Role Variables
--------------

Variables exist in this role that copy and store the corresponding files, places them within the OS configuration or installs the required packages for each distribution type.

    vars/main.yml - is only used to map the ad_access_group (mapped the the ad_access_filer option in the /etc/sssd/sssd.conf file) variable to the default HFCSadmin user OU (memberOf=cn=GS-GG-GSFPD06-HFCSadmin,ou=GSFPD06Groups,ou=GSFPD06,ou=GS,dc=ndc,dc=nasa,dc=gov)
    vars/RedHat.yml
    vars/Ubuntu.yml

Tags
----------------

Ansible tagging is integrated in the tasks/main.yml in order to enforce collective deployments (--tags) or skipping (--skip-tags) of role aspects:

    rhel7_ad - postures any RHEL 7-based system for AD binding
    rhel8_ad - postures any RHEL 8-based system for AD binding
    ubuntu_ad - postures all Ubuntu systems for AD binding

Invoking the Role
----------------

*Repo Clone and Run Locally*

**git clone https://ges-gitlab-01.genesis.local/ges-it/ansible.git (HTTP)** 

**git clone ssh://git@ges-gitlab-01.genesis.local:2222/ges-it/ansible.git (SSH)**

**ansible-playbook -c local -i localhost, ansible/ges_ad/ges_ad.yml -K**

*Ansible Pull*

**ansible-pull -U https://ges-gitlab-01.genesis.local/ges-it/ansible.git -c local -i localhost, ges_ad/ges_ad.yml -K** 

*Ansible Tower/AWX*

There is a Job Template in the HFCS Ansible solution that deploys this role against the Org's target inventory and credentials - **GES AD Posturing**.  Ansible tagging can be selected while grooming the workflow for run against targets using the **Job Tags** or **Skip Tags** prompt.

Author Information
------------------

Damon Chandler
    
dchandler@genesisesi.com