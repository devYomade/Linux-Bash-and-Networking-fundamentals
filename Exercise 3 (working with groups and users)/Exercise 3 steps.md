## TASK:
* Create 3 groups -admin, support & engineering and add the admin group to sudoers.
* Create a user in each of the groups.
* Generate SSH keys for the user in the admin group.

## Instructions:
- Submit the contents of /etc/group,/etc/sudoers.

## Steps:
- I went to my machine and spinned up my linux enivronment using `vagrant ssh`.
- Then i switched to the root user to be able to create users, and group using the command `sudo su`.
- Then i created 3 groups using the command `groupadd [group]`.
- Then i created 3 users assigning them to the 3 already available group using the command `useradd -g [group] -m -s /usr/bin/bash [user]`.
- Then i went ahead and signed into the user i assigned to the admin group so as to be able to generate SSH keys for that user using the command `su - [user]`.
- To generate the SSH key i used the command `ssh-keygen` and followed prompt.

