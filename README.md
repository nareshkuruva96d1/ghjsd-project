# ghjsd-project
# project flow
1. get the CSS templates from https://www.free-css.com/
2. pusch it to the github repo.
3. set-up the jenkins server and create pipeline.
4. set-up SonarQube server and integrate it with the jenkins pipeline.
5. set-up the Docker server and integrate it with the jenkins pipeline.
6. Access the website in the browser.

# 1. get the CSS templates from https://www.free-css.com/
* get the CSS templates from https://www.free-css.com/
* download any one of the template and extract it on any of the folder in the machine.

# 2. pusch it to the github repo.
* now login to the github and create one repository for the project and copy that link and now in the machine go to the folder where the tempalte has been extracted and then do gitbash here and
* git init in that folder and then clone the github repo using git clone https://github.com/nareshkuruva96d1/ghjsd-project.git
* now check the git status
* git add .
* git commit -m "message"
* now set the remote repository in git using
* git remote add origin master https://github.com/nareshkuruva96d1/ghjsd-project.git
* and then push the changes to the github repo.

# Create three instances:
*   * Jenkins
    * SonarQube
    * Docker
# 3. Jenkins server set-up and Installations:
## prerequiste for Jenkins installations:
* java needs to installed in the machine and that to it should be 11 or more than that.
* machine should be of t2.medium.
# in the follow the steps:
* once login to the machine update the machine using
* ``` bash
  sudo apt update
  and then install the openjdk-17 using
  sudo apt install openjdk-17-jre -y 
  ```
  * goto this website https://www.jenkins.io/doc/book/installing/linux/#debianubuntu
    ``` bash
    pass this commands 
    curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
    /usr/share/keyrings/jenkins-keyring.asc > /dev/null
    echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
    https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
    /etc/apt/sources.list.d/jenkins.list > /dev/null
    sudo apt-get update
    sudo apt-get install jenkins
    ```
* now jenkins will be installed into the machine
* jenkins will work on port 8080, so we have to allow that port in the security part of our machine.
* once it is done, we have copy the public IP of the jenkins server and paste it in the browser and pass the port 8080.
* once it gets loaded we can see the getting started page in that we can find the file path there we can get the administrator password the path is
  ``` bash
  /var/lib/jenkins/secrets/initialAdminPassword
  ```
* we need to copy that from the machine and paste in that page and click on continue.
* in the next page click on install suggested plugins.
* once it install the plugins, now we will get the create first admin user page. Here we need enter the username, password,fullname and any gmail address. and click on save and continue.
* and in the next page click on finish.
* Now we can start using jenkins
* 1st what we have to do is we have to create a pipeline. for that just click on the newitem,and give it any name like automated-pipeline.
* and select the project i our case we are going with the freestyle project. and click on ok then project will be create on the given name.
* after that we have to click on the project, then we will get the configuration settings of that project.
* now we go to the source code management --> and select the git radio icon.
* Then it will ask for the github repo url, so we have to copy the github project url and paste it hare.
* and then check the name of the branch. github branch and this should be same.
* now go to the build triggers, here we need to select the Github hook trigger for GITScm polling.
* after enabling this we have to go to the github repo and click settings and search for the webhooks.
* click on the webhooks and click on add webhook and here we need to copy and paste the jenkins server public IP and port after pasting it type /github-webhook/.
* and below select the let me select the idividual events. and in the events we have to allow the pull requests and pushes.
* after click on add webhook.
* after completing the configuration, just verify the webhook functionality by adding some files to the github repo and commit it, so in the jenkins it should automatically trigger the build.
* if the build is getting triggerd automatically, then our webhook is working properly.

# 4. set-up SonarQube server and integrate it with the jenkins pipeline:
## prerequiste for SonarQube installations:
* java needs to installed in the machine and that to it should be 11 or more than that.
* machine should be of min t2.medium.
# in machine follow the steps:
* once login to the machine update the machine using
* ``` bash
  sudo apt update
  and then install the openjdk-17 using
  sudo apt install openjdk-17-jre -y 
  ```
* the below steps should be performed as a normal user not the root user.
* goto the sonarqube website and get this link https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.0.65466.zip
* and we can install the Sonarqube using wget command and by using the above link we can download the sonarqube-9.9.0.65466 version.
```bash
wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.9.0.65466.zip
```
* after it gets downloaded, we have to unzip it so we need unzip package for that
```bash
sudo install unzip -y
```
* afetr installing the unzip, we have to unzip the package.
```bash
unzip sonarqube-9.9.0.65466.zip
```
* after unziping the package go the package directory
  ```bash
  cd sonarqube-9.9.0.65466/bin/linux-x86-64
  ls 
  ./sonar.sh console
  ```
* if the above file not executed we have do this step Change the root access to the sonar file. Try running in normal user access.
  ```bash
  chown <another user>:<user group> sonar.sh
  ```
* after performing the above command sonarqube server will get started.
* now we have to enable the port 9000 for the sonarqube server for our machine.
* now we need to copy the public IP of the sonarqube and paste it in the browser with port number 9000.
* now the sonarqube will get loaded and default login credentials for sonarqube is admin and admin and click on the login.
* now we need to update the password, pass the old password and set the new password for the sonarqube server and update it.
* once we update, we can now loged into the sonarqube webpage.
* in the sonarqube webpage click on the project type is manual and click on manually and now we need to create the project.
* give the project diaplay name, project-key and then the branch in that page and click on the set-up.
* in the next page we have to select the CI method, so we will be usign jenkins so select the jenins.
* now click on the github-->configure analysis-->continue-->continue.
* now click on the other --> now we have to copy the project key and paste it in the notepad for future use, and then click on finish the tutorial.
* in the next page go to admin user-->click on my account-->click on security-->now we have to create a token.
* name-->jenkis-token-->type-->global analysis token-->expires-->no expiration-->and click on generate.
* now the token will be generated now we need to copy the token and paste it in the note pad for later use.
* once it is done we have to go back to the jenkins.
## SonarQube intigration with Jenkins:
* goto the Jenkins click on the manage jenkins-->plugins-->available plugins-->search for sonarqube scanner-->select the plugin and click on the install without restart.
* now install anther plugin manage jenkins-->plugins-->available plugins-->search for SSH2 Easy-->select the plugin and click on the install without restart.
* now we have to go to the global tool configuration here scrolle down we can see sonarqube scanner-->click on add sonarqube scanner-->give any name-->check the install automatically-->and then click on save.
* now goto the configure system scrolle down we can see sonarqube servers-->click on add sonarqube-->give any name-->and we have to copy paste the url of the sonarqube server-->and save it.
* now we have to goto the pipeline what we have created-->and goto the configure-->goto the build step-->select execute the sonarqube scanner--> in the Analysis properties paste the projectkey that we have pasted in the note pad-->and save it.
*  again go back to the manage jenkins-->configure system-->sonarqube servers-->click on add and select jenkins-->in the pop-up -->kind - secret text-->in secret we have to paste the token that we have copied into the notepad-->and give any ID-->add and in next page select the token and click on save.
* now move back to pipeline, check if we need to add anything or not. if not just verify the pipeline by clicking the build now.
* if the build is successful we can check the code scans in sonarqube. in the Sonarqube if the code is gets passed then we have to deploy that into the Docker.

# 5. set-up the Docker server and integrate it with the jenkins pipeline:
## in machine follow the steps:
* once login to the machine update the machine using
* ``` bash
  sudo apt update
  and then install the openjdk-17 using
  sudo apt install openjdk-17-jre -y 
  ```
  * goto the Docker website-->install-->ubuntu-->goto set up the repository
  * and follw the steps:
     ```bash
     1. Update the apt package index and install packages to allow apt to use a repository over HTTPS:
     sudo apt-get update
     sudo apt-get install ca-certificates curl gnupg
     
     2. Add Docker’s official GPG key:
     sudo install -m 0755 -d /etc/apt/keyrings
     curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
     sudo chmod a+r /etc/apt/keyrings/docker.gpg
     3. Use the following command to set up the repository:
      echo \
        "deb [arch="$(dpkg --print-architecture)" signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \
        "$(. /etc/os-release && echo "$VERSION_CODENAME")" stable" | \
        sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
     4. Update the apt package index:
         sudo apt-get update
     
     5.Install Docker Engine, containerd, and Docker Compose.
         * To install the latest version, run:
         sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
      ```
