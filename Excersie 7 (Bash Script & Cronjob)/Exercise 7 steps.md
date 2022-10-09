## Task:
- Create a bash script to run at every hour, saving system memory (RAM) usage to a specified file and at midnight it sends the content of the file to a specified email address, then starts over for the new day.

## Instructions: 
- Submit the content of your script, cronjob and a sample of the email sent, all in the folder for this exercise.

## Steps:
- Firstly to be able to send a mail from my terminal, i had to install `SSMTP` and `Mailutils` with the command `sudo apt install [package]`.
- Then after that i had to configure the SSMTP ussing the command `sudo nano /etc/ssmtp/ssmtp.conf`.
- After the configuration to my own exact need, i then went over to `/home/vagrant`, and then created a bash script for the main puropose of what i wanted to do with the command `sudo nano ramusage.sh`.
- Then i wrote the basic command for the script to run when executed to be able to send a mail containing the ramusage at midnight;
<br>

![ram script](https://user-images.githubusercontent.com/105651785/194752029-f4e7d166-b9c1-40c6-8383-4efd46e883ba.png).
- After that i had to install `CRONTAB` so as to be able to tell the script exactly when to run, so installed `CRONTAB` with the command `apt-get install cron`.
- After that i edited the crontab with the command `crontab -e`;
<br>

![script crontab](https://user-images.githubusercontent.com/105651785/194752212-2391115d-53d5-4def-a261-4f4a7b16d738.png).
- After that by exactly 12am i got the email that i instructed the Bash Script to run.



