# ElasticTest

The intent is to be a soup to nuts full instance of ElasticStack that is fully collapsible.

Prerequisities:

* Visual Studio Code (https://code.visualstudio.com/)
* Git (https://git-scm.com/download/win)
* Docker Desktop (https://www.docker.com/products/docker-desktop)
* Windows Subsystem for Linux / WSL 2

Installation:

I personally prefer to use Chocolatey (https://chocolatey.org/) for most of my local install needs, but I'll explain manual methodologies below.

1) Install Windows Subsystem for Linux / WSL 2
    From an elevated Powershell prompt:
    
    `notepad "$env:USERPROFILE/.wslconfig"`

    This will create a blank configuration for WSL to use, tied to your user profile.  I personally set mine to 6GB, as below, but the requirement is for 4GB:
    
    ![image](https://user-images.githubusercontent.com/30252277/137913348-39143db3-14ba-47d0-b11c-4189b39174b3.png)
    
    `wsl --install`
    
    This will run through the install process, potentially requiring a subsequent reboot.  Do so if required.
    
2) Install Git
    Run the installer.  Select the following options, taking note of any warnings or notifications that are presented:  
    
    ![image](https://user-images.githubusercontent.com/30252277/137911487-313352dc-968e-475a-bf90-c31f4db6ad8e.png)
    
    


3) Install Docker Desktop
4) 
