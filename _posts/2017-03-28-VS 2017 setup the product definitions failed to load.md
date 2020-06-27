# VS 2017 setup the product definitions failed to load

I tried to upgrade my Visual Studio 2017 RC to the release version and got an error product definitions failed to load


![error image](/images/vs2017error.png)


The way I got the installer to work was to delete the folder  %LocalAppData%\Microsoft\VisualStudio\Packages\ 



After that running the installer I was able to update my install to the released version
