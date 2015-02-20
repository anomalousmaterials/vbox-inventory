# vbox-inventory
A dynamic inventory script for Ansible and VirtualBox.

What it does
------------
Lets you run Ansible against virtual machines running in VirtualBox without having to check addresses and manually maintain the Ansible hosts file.

How it works
------------
The script uses VBoxManage to fetch the name and IP address of each currently running VM and provides these in a JSON format palatable to Ansible.

How to use it
-------------
Here's one way to set up a combination of static and dynamic inventories:

* Create a directory to hold your host data:

		mkdir ~/ansible_inventory

* Add this line to your .bash_profile:

		export ANSIBLE_HOSTS=~/ansible_inventory

* Put your static host file(s) and the script in ~/ansible_inventory
* Make the script executable:

		chmod 0755 ~/ansible_inventory/vbox_inventory.py

* Test:

		~/ansible_inventory/vbox_inventory.py --list
		ansible all --list-hosts

Limitations
-----------
* Gets the address of the first interface, multihomed hosts may not work as expected.

Customizing
-----------
* The default group name is vbox. Modify the value of constant VBOX_GROUP to change it.
* You can add host variables to constant HOSTVAR_TEMPLATE. For example, to use the root account to log in:

		HOSTVAR_TEMPLATE = {'ansible_ssh_user': 'root'}

