# Error with Cert when starting an Asp.Net core website on the Mac

On my Mac I tried to run a Asp.Net core web site and got an error when starting the web site about ssl cert was invalid.



Adding the certificate to the Trusted Root Certficates store failed with the following error: Failed with a critical error.



The sites were working a few days before so I tried this command line.
     

     dotnet dev-certs https --trust


Got a response A valid HTTPS certificate is already present.



Ran app again and still got same error.

![cert manager](/images/MacCert.png)



The way I fixed it on my Mac was to open the KeyChain Access app and deleted the localhost certificate


Ran 

      dotnet dev-certs https --trust 


After this I was able to debug my asp.net core apps in vs for Mac 2019 and Rider

