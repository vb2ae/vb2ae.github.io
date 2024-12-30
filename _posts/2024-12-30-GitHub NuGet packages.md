### Using Github Nuget packages


## Generate token

To use a Github nuget package first need to generate a token with permissions to read packages

Once logged in to Github go to this page [https://github.com/settings/tokens](https://github.com/settings/tokens)

Select read packages permission and I typically set the expiration for a year but you can set the expiration what ever suites you best

 ![read permissions](/images/github-token-packages.png) 


## Add nuget source

 Once you generate the token you will use it in to call dotnet nuget

      dotnet nuget add source --username <Your username> --password <Your token Goes here> --store-password-in-clear-text --name "Caliburn.Micro github" "https://nuget.pkg.github.com/caliburn.micro/index.json"

Replace <Your username> with your username and <Your Token Goes here> with the token you just generated.  Feel free to change the name.  

## Add the nuget package

To add a package to your project in the folder with the csproj  run the following command.

     add package Caliburn.Micro.Maui --version 5.0.183-beta --source "https://nuget.pkg.github.com/caliburn-micro/index.json"

