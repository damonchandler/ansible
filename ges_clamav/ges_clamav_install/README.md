Role - Clam Antivirus (ClamAV) Installation/Configuration Against Linux Information Systems
=========

This role installs and configures ClamAV according to documented local operating processes against supported Linux operating systems.  It does the following:

* Installs/enables the Extra Packages for Enterprise Linux (EPEL) repositories for CentOS and RHEL 7/8.  Installs the Oracle-specific EPEL repositories against Oracle Linxu 7/8.
* Installs the required packages depending on the distribution type.
    * Ubuntu - clamav and clamav-daemon
    * RHEL-based distributions - clamav, clamd, clamav-update, and clamav-data
* Sets the SELinux boolean against RHEL-based operating systems (since the SELInux policy is mandatory to be set to enabled).
* Creates the /clamscripts/GES_Weekly_Scan.sh script in order to perform a full weekly / scan, with aggregation of data to local syslog (versus discrete log file).
* Configures root cron to process the weekly scan every Friday @ 15:00.
* Configures clamonacc as persistence targeting to the local /home and sub-directories.
* Updates virus definitions every 6 hours (Checks 4).
* RHEL 7-based distributions: removes the /etc/cron.d/clamav-update file - which causes a "condition failed" error on the clamav-freshclam.service.  The file continuously tries to apply a cron job to sleep freshclam (0 */3 * * * root /usr/share/clamav/freshclam-sleep > /dev/null) and seems inconsequential to the deployment as it is not replicated in RHEL 8 based distributions.


Requirements
------------
Git is required to perform any cloning commands.

The scope of the installation requirements are satisfied inside of the role configuration.

Local Ansible install is also required in order to locally perform 'ansible-playbook' or 'ansible-pull' commands against the target - https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html.

Role Variables
--------------

Several variables exist in this role that create the corresponding files and places them within the OS configuration.

    vars/main.yml
    vars/RedHat.yml
    vars/Ubuntu.yml

There is also inclusion of syntax in the tasks/main.yml to allow for reference of the vars particular to each chosen distribution type.

    - name: Gather OS Specific Vars
      include_vars: "{{ item }}"
      with_first_found: 
        - '{{ ansible_os_family }}.yml'
        - '{{ ansible_distribution }}.yml'
        - 'main.yml'

Tags
----------------

Ansible tagging is now integrated in the tasks/main.yml in order to enforce collective deployments (--tags) or skipping (--skip-tags) of role aspects:

    rhel_clamav - Used in tandem with the tasks/FPD_RHEL.yml role component.
    ubuntu_clamav - Used in tandem with the tasks/FPD_Ubuntu.yml role component.

Invoking the Role
----------------

*Repo Clone and Run Locally*

**git clone - ... (HTTP)**

**git clone - ... (SSH)**

**ansible-playbook -c local -i localhost, fpd_clamav/ges_clamav_install.yml**

*Ansible Pull*

**ansible-pull -U ... ges_clamav_install.yml** 

    Both ansible-pull and ansible-playbook commands allow for levergaing the tags at the command line:

    --skip-tags 'rhel_clamav,ubuntu_clamav' (ignore tasks with said tag)
    --tags or -t 'rhel_clamav,ubuntu_clamav' (invoke against tags only)

    Example:

    ansible-playbook -c local -i localhost, ges_clamav_install.yml --skip-tags 'rhel_clamav'

    (runs tasks for Ubuntu-based systems; ignores tasks tagged for RHEL-based systems)

*Ansible Tower/AWX*

There is a Job Template in the GES Ansible solution that deploys this role against the Org's target inventory and credentials - **GES ClamAV Configuration**.  Ansible tagging can be selected while grooming the workflow for run against targets using the **Job Tags** or **Skip Tags** prompt.

Author Information
------------------

Damon Chandler
    
dchandler@genesisesi.com