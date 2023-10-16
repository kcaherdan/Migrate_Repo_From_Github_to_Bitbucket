# Migrate_Repo_From_Github_to_Bitbucket
Steps to Migrate Repo From Github to Bitbucket

<ins>**Solution : Create two ubuntu docker containers with ssh access**</ins>

![image](https://github.com/kcaherdan/Migrate_Repo_From_Github_to_Bitbucket/assets/71196354/e3f22697-fd80-41a5-b84c-5d6170c43093)



This project involves setting up and establishing a **Secure Shell** connection between two **Ubuntu** containers in docker.

First run **shhserver-container** which is Ubuntu container after pulling it from [**DockerHub**](https://hub.docker.com/) then we will do SSH configuration specifically we are going to install **openssh-server** package on first container because it enables container to act as an SSH server and accept incoming SSH connections.

Next we will run a second container and do the same SSH configuration but this time we will install **openssh-client** package because it allows the container to act as an SSH client and inititate outgoing SSH connection also the package includes the neccessary components for connecting to an SSH server.

Next we need to set a **new password** for the root user inside the first container. Finally the end result is two Ubuntu container that can communicate with each other securely over SSH.

&nbsp;

![fc42911c392de1ddbe886c84de2c8c72.png](file:///C:/Users/kcaher/.config/joplin-desktop/resources/d89191b238b7493baddfc07388b39e87.png)

**To pull Ubuntu Image**

docker pull ubuntu

&nbsp;

**To check image is pulled or not**

docker image ls

# Create First DockerContainer

1. Now create first Ubuntu container by,

docker run -it --name sshserver-container ubuntu  
**“ -it** means run container in interactive mode ”

**2. To install SSH-Server**

apt-get install openssh-server -y

**3. Install vim editor**

apt-get install vim -y

**4. configure ssh_config file in first container (sshserver-container)**

vim /etc/ssh/sshd_config

In this file go to the Authentication part and uncomment  
“**permitRootLogin prohobit-password** ” line and change to  
“**permitRootLogin yes** ”

**To check SSHservice start**

service --status-all

**if SSH is not start then write**

service ssh start

**then again check SSH status**

service --status-all

**SSH server started**

so we configure our first container (**sshserver-container**)then go outside the container by,

exit

# Create Second Docker Container

Now create second **Ubuntu** container

docker run -it name sshclient-container ubuntu

In this container repeat the above command but instead of installing openssh-server we need to install **openssh-client**

apt-get update

**To install SSH Client**

apt-get install openssh-client -y

so we install SSH client in our second container then go outside the container by,

exit

Now, go to the first container (**sshserver-container**)and set new password for **root,**

docker exec -it sshserver-container bash

passwd root

This is will allow to set the new password.

Also find the IP Address of the First container
