# Fixing your Hyper-V emulators

If you are having problems getting your hyper-v emulators to run here are the steps I recommend to fix them



First and this usually fixes the issue.  Open the Hyper-V manager and delete all the virtual switches you will find them under the virtual switch manager




![Virtual Switch Manager](/images/virtualSwitches.PNG) 




Try running the Hyper-V emulators again the switches will be recreated.  In the rare chance they still do not work go ahead and delete the virtual switches again. 




![Hyper-V manager](/images/hyperv.PNG) 




Now delete the virtual machines for the emulators.  Finally open the Device Manager and delete any hyper-v network adapters you might have




![DeviceManager](/images/devicemanager.PNG) 






Rerun the emulators and they should work everything you deleted will be recreated.
