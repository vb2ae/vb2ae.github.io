# Using Packages from the GitHub NuGet Feed

## Generating a Token

To use a GitHub NuGet package, you first need to generate a token with permissions to read packages.

1. Log in to GitHub.
2. Navigate to [this page](https://github.com/settings/tokens).

Select the **read:packages** permission. Typically, I set the expiration for a year, but you can choose whatever period suits you best.

 ![read permissions](/images/github-token-packages.png) 

## Add nuget source

 Once you generate the token you will use it in to call dotnet nuget

      dotnet nuget add source --username <Your username> --password <Your token Goes here> --store-password-in-clear-text --name "Caliburn.Micro github" "https://nuget.pkg.github.com/caliburn.micro/index.json"

Replace `<YourUsername>` with your username and `<Your Token Goes here>` with the token you just generated.  Feel free to change the name of the source.  

## Add the nuget package

To add a package to your project in the folder with the csproj  run the following command.

     add package Caliburn.Micro.Maui --version 5.0.183-beta --source "https://nuget.pkg.github.com/caliburn-micro/index.json"


