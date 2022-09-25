## Task:
- You already have Github account, also setup a Gitlab account if you don't have one already.
- You already have a altschool-cloud-exercises project, clone the project to your local system.
- Setup your name and email in Git's global config.

## Instructions:
- [ ] git config -|.
- [ ] git remote -v.
- [ ] git log.

## Steps:
- First i spinned up my linux server, then after that i tried cloning my altschool-cloud-exercises from my github with the command `git clone [https]`.
- But then i ran into an error;
`remote: Support for password authentication was removed on August 13, 2021.
remote: Please see https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently recommended modes of authentication.`
- So i logged into my github account and went to the developer settings to generate a github access token, which i used instead of a password while logging into my github from my terminal.
- After i succesffuly cloned the project to my local machine then i ran the command `git config -l`
<br>

![git config -l](https://user-images.githubusercontent.com/105651785/192138041-9192de74-2802-4d26-99e0-03eaf3615cb8.png)

- Then i ran the command `git remote -v`
<br>

![git remote -v](https://user-images.githubusercontent.com/105651785/192138138-29e73db2-5ea1-44e5-8b06-d7c4af31be30.png)

-Then i also ran the command `git log`
<br>

![git log](https://user-images.githubusercontent.com/105651785/192138165-0621e4fb-aab9-4120-99dd-d31c59a63079.png)





