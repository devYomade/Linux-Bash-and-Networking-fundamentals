[Vagrantfile.zip](https://github.com/devYomade/altschool-cloud-exercises/files/9554306/Vagrantfile.zip)

![Screenshot 2022-09-09 133211](https://user-images.githubusercontent.com/105651785/189837386-2451f564-a9a6-4e15-a99d-013a0025f563.png)
## TASK:
* Setup Ubuntu 20.04 LTS on your local machine using Vagrant.

## Instructions:
- CUstomize your Vagrant file as necessary with private_network set to DHCP.
- Once the machine is up, run ifconfig and share the output in your submission along with your vagrant file.

## Steps:
- I went over to vagrants website and downloaded the right version for my local machine(HP ELITEBOOK)
- I then installed Virtualbox so as to be able to spin up the vagrant file succesfully.

> After having both vagrant and virtual box running on my host machine, I proceeded to create my ubuntu os with the the steps below.

- I created a directory for hosting my vagrant file.
- I created an empty vagrantfile by running the `the touch vagrantfile` command
- I proceeded to configure my vagrantfile
- Then i provisioned my ubuntu virtual machine usuing the `vagrant up` command.
- To login to my newly created linux virtual machine i issued the `vagrant ssh` command.
- While in the virtual space i installed the `net-tools` package so as to be able to check my ip address.
- By running the `ifconfig` command i am able to display my virtual machines IP address.
- To exit from my virtual machine to the host, i entered the `exit` command.
- Then to stop the virtual machine from running i issue the `vagrant halt` command.
