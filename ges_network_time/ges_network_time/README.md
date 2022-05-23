Role - GES Network Time
=========

This role configures the Chrony (RHEL-based distributions) or NTP (Ubuntu) services to sync time from genesis-dc1.genesis.local.

In Ubuntu:

* The ntp and ntpdate packages are installed.
* The ntp.conf file is templatized (Jinja) and copied in place to the /etc/ directory.
* The ntp service is stopped.
* Time sync is forced using the ntpdate command: ntpdate -q genesis-dc1.genesis.local.
* The ntp service is started.

In RHEL-based distributions:

* Chrony is installed if it is not already otherwise in the baseline (pre-installed).
* The chrony.conf is templatized (Jinja) and copied in place to the /etc/ directory.
* The chronyd service is restarted.

Requirements
------------
Git is required to perform any cloning commands.

Local Ansible install is also required in order to locally perform 'ansible-playbook' or 'ansible-pull' commands against the target - https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html.

Tags
----------------

Ansible tagging is integrated in the tasks/main.yml in order to enforce collective deployments (--tags) or skipping (--skip-tags) of role aspects:

    ubuntu_time - Configures NTP against Ubuntu.
    rhel_time - Configures Chrony against RHEL-based distributions.

Invoking the Role
----------------
 *Repo Clone and Run Locally*

**git clone https://developer.nasa.gov/FPD-Ansible/fpd_network_time (HTTP)**

**git clone git@developer.nasa.gov:FPD-Ansible/fpd_network_time (SSH)**

**ansible-playbook -c local -i localhost, fpd_network_time/fpd_network_time.yml**

*Ansible Pull*

**ansible-pull -U https://developer.nasa.gov/FPD-Ansible/fpd_network_time -c local -i localhost, fpd_network_time.yml**

*Ansible Tower/AWX*

There is a Job Template in the directorate-level Ansible solution that deploys this role against FPD IT Security's target inventory and credentials - FPD Network Time.

Author Information
------------------

Damon Chandler
    
dchandler@genesisesi.com