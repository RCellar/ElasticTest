# ElasticTest

The intent is to be a soup to nuts full instance of ElasticStack that is fully collapsible.  This guide presumes the usage of a Windows workstation, but can be easily modified to accomodate Mac/Linux contexts.

Prerequisities:
* 8 GB of System RAM, but 16+ GB is recommended, particularly if you plan to simulate load or development.
* Visual Studio Code (https://code.visualstudio.com/):
    
    Extensions:
    
    ![image](https://user-images.githubusercontent.com/30252277/137925301-d2d00cb7-384a-4eb9-91bd-a0f597449738.png)
* Git (https://git-scm.com/download/win)
* Docker Desktop (https://www.docker.com/products/docker-desktop)
* Windows Subsystem for Linux / WSL 2

Installation:

I personally prefer to use Chocolatey (https://chocolatey.org/) for most of my local install needs, but I'll explain manual methodologies below.

1) Configure and Install Windows Subsystem for Linux / WSL 2:

    From an elevated Powershell prompt:
    
    `notepad "$env:USERPROFILE/.wslconfig"`

    This will create a blank configuration for WSL to use, tied to your user profile.  I personally set mine to 6GB, as below, but the requirement is for 4GB:
    
    ![image](https://user-images.githubusercontent.com/30252277/137913348-39143db3-14ba-47d0-b11c-4189b39174b3.png)
    
    `wsl --install`
    
    This will run through the install process, potentially requiring a subsequent reboot.  Do so if required.
    
2) Install Git:

    Run the installer.  Select the following options, taking note of any warnings or notifications that are presented:  
    
    ![image](https://user-images.githubusercontent.com/30252277/137911487-313352dc-968e-475a-bf90-c31f4db6ad8e.png)
    ![image](https://user-images.githubusercontent.com/30252277/137913857-b74e80ff-0e9d-415c-8a85-01f3cbc238a5.png)
    ![image](https://user-images.githubusercontent.com/30252277/137913888-fc45a990-390e-492a-a398-25b1b0388c78.png)

    Other options can be chosen at your preference/discretion.  I would advise using the Git Credential Manager.

3) Install Docker Desktop:

    Run the installer and proceed through installation.  Once installation is completed, validate that Docker has both Docker Compose and WSL2 backend enabled:
    
    ![image](https://user-images.githubusercontent.com/30252277/137914822-143899ad-0d8c-4c05-95a7-f21c5efe7e5d.png)

    Pull down the Docker images:
    
    `docker pull docker.elastic.co/elasticsearch/elasticsearch:7.15.1`
    `docker pull docker.elastic.co/enterprise-search/enterprise-search:7.15.0`
    `docker pull docker.elastic.co/kibana/kibana:7.15.1`
    `docker pull vault:latest`
     
4) Clone down the Git repo:
     
    Navigate to a directory of your choosing and clone a copy down:
    `git clone https://github.com/RCellar/ElasticTest.git`
     
5) Build the Certificate Volume and create certificates:

    With "ElasticTest" as your working directory:
     
    `docker compose -f create-certs.yml up`
     
    This creates all the certificates that will be used by the container environment we're about to bring online.  A single instance of ElasticSearch will come        online, create and populate the volume, then turn off.  You should see results in Docker Desktop like the following:
     
    ![image](https://user-images.githubusercontent.com/30252277/137956971-462d15b5-3ee9-4c2b-a243-91fee12c8f54.png)

    Once validated, we can remove the container as it will no longer be in use.  
    
    `docker compose -f create-certs.yml down`
        
    This will remove the containers associated with the runbook, but leave the Volumes behind.  (Note: to also bring down volumes, add `-v` to the previous command)
    
6) Build the Elastic Environment:

    `docker compose -f enchilada.yml up`
