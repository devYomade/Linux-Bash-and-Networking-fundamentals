## Task:
- Create a bash script to run at every hour, saving system memory (RAM) usage to a specified file and at midnight it sends the content of the file to a specified email address, then starts over for the new day.

## Instructions: 
- Submit the content of your script, cronjob and a sample of the email sent, all in the folder for this exercise.

## Steps:
- Firstly to be able to send a mail from my terminal, i had to install `SSMTP` and `Mailutils` with the command `sudo apt install [package]`.
- Then after that i had to configure the SSMTP ussing the command `sudo nano /etc/ssmtp/ssmtp.conf`.
- After the configuration to my own exact need, i then went over to `/home/vagrant`, and then created a bash script for the main puropose of what i wanted to do qith the command ` sudo nano ramusage.sh`.
- 
