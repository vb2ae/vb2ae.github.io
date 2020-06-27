# VSTS build failed

Recently I was moving a TFS XAML build to one the new style builds.   The XAML based build worked fine but when I tried the new format the build failed with this error



      Unable to process command '##vso[task.logdetail id=faad7dd0-d179-4a32-ba2a-cecf68fd7d28;parentid=;


I tried turning off logging in the build and it did not help.  This issue was one of the folder names for the projects.  It contained [ ] in the name which the new Build format does not support.  Removing the [ ]  from the folder name allowed the project to build.  I also had to edit the solution file and update the project folder to the new name


Hope this helps
