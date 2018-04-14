# ansible-admin-roles

Role Name
------------

### Role user
Create a new account on an system
We'll create a user who is able to login with the following attributes:

Requirements
------------

Step 1 — Installing Ansible
To begin exploring Ansible as a means of managing our various servers, we need to install the Ansible software on at least one machine.    
To get Ansible for CentOS 7, first ensure that the CentOS 7 EPEL repository is installed:

    sudo yum install epel-release

Once the repository is installed, install Ansible with yum:

    sudo yum install ansible


Role Variables
--------------


Dependencies
------------


Example Playbook Role Usage
----------------

    User: "mynewUser"
    Password: secret
    Home Directory: /home/userdirectory
    Shell: /bin/bash

We we're creating a "regular" user, one that can login. That user will likely assigned to an UID of 1000 or greater.

The Ansible task file with a user definition which uses the "
[user module](http://docs.ansible.com/ansible/latest/modules/user_module.html)" to create a user:

    
    ---
    - name: Create a login user
     user:
      name: newUser
      password: '???'
      groups: # Empty by default, here we give it some groups
       - sudo
      state: present
      shell: /bin/bash       # Defaults to /bin/bash
      system: no             # Defaults to no
      createhome: yes        # Defaults to yes
      home: /home/newUser  # Defaults to /home/<username>


I little more about tasks **definition**
<pre><code><b>name</b>: Set the username (the primary group they belong to will be the same).
<b>password</b>: Set the password.
<b>groups</b>: Assign secondary groups. Their "sudo" (group sudo allows the user to run sudo commands on Ubuntu and Debian linux or CentOS).
<b>state</b>: Tell ansible we want the user to exist.
<b>shell</b>: You can define any shell. The default is /bin/bash.
<b>system</b>: Set this to "yes" to make it a system user. No shell or home directory will be made unless specified otherwise.
<b>createhome</b>: Yes to create a home directory, no to not create one
<b>home</b>: If you don't want to use the default location, set it here
</pre></code>

Testing
----------------
To test the playbook locally, first install the required dependencies locally.

    $ ansible-galaxy install --role-file=./tasks/requirements.yml --roles-path=roles --force


License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).

Contributors
------------


References
-----------
[1] https://serversforhackers.com/c/create-user-in-ansible
