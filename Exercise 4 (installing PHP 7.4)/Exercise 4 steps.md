## TASK:
- Install PHP 7.4 on your local linux machine using the ppa:ondrej/php package repo.

## Instructions:
- Learn how to use the add-apt-repository command.
- Submit the content of /etc/apt/sources.list and the output of php -v command.

## Steps:
- I spinned up my linux environment with the command `vagarant ssh`.
- I then added a dependency for PHP with the command `sudo apt install software-properties-common apt-transport-https -y`.
- Then i moved on to adding a repositry for PHP using the command `sudo add-apt-repository ppa:ondrej/php -y`.
- Then i ran the command `sudo apt-get update -y`.
- I ran an update using the command `sudo apt-get upgrade -y`.
- Then i moved on to installing PHP 7.4 with the command `sudo apt install -y php7.4 php7.4-common`.
