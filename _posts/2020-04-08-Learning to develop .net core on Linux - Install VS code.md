# To install Visual Studio Code we need to open a terminal window


## First install the key

     sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
     
## Install the repository

    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
    
## Update the package cache

     sudo dnf check-update
     
## Then install code

      sudo dnf install code
      
## Now that VS code is installed

### Lets install the .net core 3.1 sdk
First get the key and repo

      sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc

      sudo wget -O /etc/yum.repos.d/microsoft-prod.repo https://packages.microsoft.com/config/fedora/31/prod.repo
      
Now we can install .net core 3.1

      sudo dnf install dotnet-sdk-3.1



Make sure in Visual Studio code you install the C# extension by Microsoft
