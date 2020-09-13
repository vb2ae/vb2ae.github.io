# The path is not a legal form when opening a project

I was trying to open a project to look at the source control.  When I tried to open it I noticed that none of the projects opened.

![NuGet](/images/ProjectsDidNotLoad.png)

since all the projects were unloaded I right clicked on a project selected Reload Project.  I got this error

![NuGet](/images/ProjectOpenError.png)

To fix this I opened a terminal window (could use powershell or command prompt) and typed the command dotnet --version

![NuGet](/images/dotnetversion.png)

finally I looked in the directory when my solution was located and opened a file name Global.Json

    {
      "sdk": {
        "version": "3.1.101"
      },
      "msbuild-sdks": {
        "MSBuild.Sdk.Extras": "2.0.54"
      }
    }  
    
 And modified the sdk version to match the dotnet version I have installed
 
     {
      "sdk": {
        "version": "3.1.401"
      },
      "msbuild-sdks": {
        "MSBuild.Sdk.Extras": "2.0.54"
      }
    }  
    
    I was then able to load the project
