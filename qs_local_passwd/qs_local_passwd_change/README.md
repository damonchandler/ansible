Role - QS Local Password (On-Demand) Change
=========

This role forces an automated password change on local accounts when necessary.  By default, it changes the following accounts:

* root
* qs_admin
* qs_ansible

Requirements
------------
Git is required to perform any cloning commands.

Local Ansible install is also required in order to locally perform 'ansible-playbook' or 'ansible-pull' commands against the target - https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html.

The vars/main.yml file must have the following parameters (static) populated with a encrypted/hashed password in order to work:

* root_password_change
* qs_admin_password_change
* qs_ansible_password_change

**The encrypted/hashed password must be contained inside of '' (quotes) in the roles var/main.yml.**

In order to create the password, run the following from terminal:

python3 -c 'import crypt; print(crypt.crypt("*predefined_password*",crypt.mksalt(crypt.METHOD_SHA512)))'

or 

openssl passwd -6 -salt (*salted_passphrase_to_be_included_in_the_hash*)

(*The second option allows you to provide a hidden password at terminal versus the python3 method which may place your intended password into bash history.*)

The parameters can also be invoked dynamically by passing the '-e' option when running Ansible locally or via ansible-pull.  This can also be set in Ansible Tower/AWX as an extra var in YAML of JSON format.  As follows:

ansible-playbook or ansible-pull

    -e 'root_password_change=XXXXXXXXXX qs_admin_password_change=XXXXXXXXXX qs_ansible_password_change=XXXXXXXXX'

Ansible Tower/AWX (YAML)

    root_password_change: XXXXXXXXXX
    qs_admin_password_change: XXXXXXXXXX
    qs_ansible_password_change: XXXXXXXXXX

Tags
----------------

Ansible tagging is now integrated in the tasks/main.yml in order to enforce collective deployments (--tags) or skipping (--skip-tags) of role aspects:

    root_passwd - Only change root password and configure 60/14/1 against the parameters.
    qs_admin_passwd - Only change fpdadmin password and configure 60/14/1 against the parameters.
    qs_ansible_passwd - Only change fpd_ansible password and configure 60/14/1 against the parameters.

Invoking the Role
----------------

This role is for QS IT administrative use only and is not available to the greater IT community. 

*Ansible Tower/AWX*

There is a Job Template in the QS Ansible solution that deploys this role against IT's target inventory and credentials - **QS Password Change**.

Author Information
------------------

Damon Chandler
    
damon.chandler@quantumspace.us