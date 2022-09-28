Role - QS Network Time
=========

This role configures the Chrony (RHEL-based distributions) or NTP (Ubuntu) services to sync time from time.nist.gov.

In Ubuntu:

* The ntp and ntpdate packages are installed.
* The ntp.conf file is templatized (Jinja) and copied in place to the /etc/ directory.
* The ntp service is stopped.
* Time sync is forced using the ntpdate command: ntpdate -q time.nist.gov.
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

**git clone https://github.com/damonchandler/ansible.git (HTTP)**

**git clone git@github.com:damonchandler/ansible.git (SSH)**

**ansible-playbook -c local -i localhost, qs_network_time/qs_network_time.yml**

*Ansible Pull*

**ansible-pull -U https://github.com/damonchandler/ansible.git -c local -i localhost, qs_network_time/qs_network_time.yml**

*Ansible Tower/AWX*

There is a Job Template in the QS Ansible solution that deploys this role against Quantum Space IT's target inventory and credentials - **QS Network Time**.

Author Information
------------------

Damon Chandler
    
damon.chandler@quantumspace.us