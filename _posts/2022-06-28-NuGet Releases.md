New Releases of Astronomy Picture of the Day and OpenWeatherMap.Standard 

These releases drop support for .net 5 (no longer supported by Microsoft) and add support for .net 6.  .Net standard 2.0 is still supported.

They also updated the version of NewtonSoft.Json to 13.0.1 to address a security issue


Newtonsoft.Json prior to version 13.0.1 is vulnerable to Insecure Defaults due to improper handling of StackOverFlow exception (SOE) whenever nested expressions are being processed. Exploiting this vulnerability results in Denial Of Service (DoS), and it is exploitable when an attacker sends 5 requests that cause SOE in time frame of 5 minutes. This vulnerability affects Internet Information Services (IIS) Applications.

References
JamesNK/Newtonsoft.Json#2457
JamesNK/Newtonsoft.Json#2462
JamesNK/Newtonsoft.Json@7e77bbe
[https://alephsecurity.com/2018/10/22/StackOverflowException/](https://alephsecurity.com/2018/10/22/StackOverflowException/)
[https://alephsecurity.com/vulns/aleph-2018004](https://alephsecurity.com/vulns/aleph-2018004)
[https://security.snyk.io/vuln/SNYK-DOTNET-NEWTONSOFTJSON-2774678](https://security.snyk.io/vuln/SNYK-DOTNET-NEWTONSOFTJSON-2774678)


[https://github.com/vb2ae/OpenWeatherMap.Standard/releases/tag/V1.7](https://github.com/vb2ae/OpenWeatherMap.Standard/releases/tag/V1.7)

[https://github.com/vb2ae/AstronomyPictureOfTheDay/releases/tag/V1.1](https://github.com/vb2ae/AstronomyPictureOfTheDay/releases/tag/V1.1)
