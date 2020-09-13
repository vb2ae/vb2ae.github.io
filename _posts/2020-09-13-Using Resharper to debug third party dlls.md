# Using Resharper to debug third party dlls
 
 I have been running Resharper in Visual Studio 2019 to aid with my developing. One very useful feature is the ability to debug into third party dlls.  
 
 Here are the steps to enable debugging Third Party dlls
 
 First turn off Just My code in Visual Studio options
 
![NuGet](/images/justmycode.png)

Second make sure there is a make sure Cache symbols in this directory is set in the Visual Studio Options

![NuGet](/images/symbolspath.png)

Next Open the Assembly Explorer. You will find it in Extensions -> Resharper -> Windows

![NuGet](/images/AssemblyExplorer.png)

Since the third party dll I wanted to debug was in a Nuget package I clicked on the Cached NuGet packages button (black arrow)

I found the dll I was looking for and selected it.  I then clicked on the generate pdb button (red arrow)

I was then able to step into the code in the dll

![NuGet](/images/debugging.png)

