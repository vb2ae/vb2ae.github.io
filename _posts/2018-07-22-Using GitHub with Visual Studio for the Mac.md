# Using GitHub with Visual Studio for the Mac

First lets create a new Repository on GitHub .



For this demo I created a public repository that has a readme, and a Visual Studio Git Ignore file.




![Create Repo in GitHub](/images/GitHubCreate.png)






Now I created a simple .Net Core Console app to check into GitHub.  I checked use git for version control.



![Create console app](/images/CreateConsoleApp.png)





Once I created the app I built it to make sure it runs.   Now the first thing to do is create an initial commit to the local git repository.  In the version control menu select Review and Commit.


![Initial Commit](/images/ReviewAndCommit.png)




In Git Hub open the Repository you created. Press the clone or download button and copy the url for the repository.



![Remote Source](/images/RemoteSource.png)

In Visual Studio Version Control Menu select Manage Branches and Remotes


![Version Control](/images/VersionControl.png)






Add a new Remote source with the url from the GitHub website



![Set Remote Source](/images/SetRemoteSource.png)





I made a minor code change and Selected Review and Commit changes



![Commit](/images/Commit.png)







In the dialog I selected Push to remote.  First time you connect to GitHub it will ask for you credentials




![Remote](/images/SetRemoteSource.png)






Once you push your changes you should see it in GitHub.  Make sure before you push your changes you update the solution from GitHub.



![Files in GitHub](/images/FilesInGitHub.png)















