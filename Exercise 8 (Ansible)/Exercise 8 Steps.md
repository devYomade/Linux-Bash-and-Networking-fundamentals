## [Exercise]() 8

### Task:
* Create an Ansible Playbook to setup a server with Apache
* The server should be set to the Africa/Lagos Timezone
* Host an index.php file with the following content, as the main file on the server:
```php
<?php
 date("F d, Y h:i:s A e", time());
?>
```

### Instruction:
- [ ] Submit the Ansible playbook, the output of `systemctl status apache2` after deploying the playbook and a screenshot of the rendered page

### Steps:
- Firstly i had to create a multi machine (A Slave and Master Machine).
- Then i had to install `python3` on my master machine using the command `sudo apt install python3`, because ansible works with python.
- Then i installed `ansible` it self using the command `sudo apt install ansible`.
- After that i went to a open another terminal and ssh into a slave machine on the multi machine for east movement, and then i edited the `sshd_config` to allow password authentication with the command `sudo nano /etc/ssh/sshd_config`.
<br>

- Then i went to line 58 and change `PasswordAuthentication no` to `PasswordAuthentication yes` and saved the changes.
- Then i restatrted the service with the command `sudo systemcl restart sshd`
- And then i generated the ssh-keygen and copied it to the master machine with the command `ssh-copy-id -i vagrant@[ip address]`.
- Then i went back to the master machine and made a directory  with the command `mkdir [directory name]`.
- So i created an iventory file and added all the ip address i needed which was just one and it belonged to the master machine.
- Then i created a playbook file and added the task i want it to carry out;
<br>

![playbook yml](https://user-images.githubusercontent.com/105651785/197257514-4a7ceb81-04fe-4742-aacf-958d91415f01.png)
- Then i had to go back and create a index.php file to be copied to the server.
- Then after the above i ran a check to see if everything is working fine with the command `ansible-playbook playbook.yml -i iventory --check`.
- After that i ran the real command which is `ansible-playbook playbook.yml -i iventory`. 

