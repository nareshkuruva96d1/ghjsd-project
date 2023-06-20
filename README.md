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
# Jenkins server set-up and Installations:
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
