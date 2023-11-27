<center><b><h1>USB Case – Writeup</h1></b></center>

***

 

\-     First: we check the recommend link in the question: 

[Splunk Use_Cases](https://lantern.splunk.com/Security/Use_Cases)

We search for USB in the search box to get any Use-Cases related to USB:

 

![img](https://s2.loli.net/2023/11/27/da2NM5R9PBxzIrt.jpg)

 

We click on the related case to our challenge <font color='green'>“Removable devices connected to a machine”</font>

 

There, we will find that the needed search query for our challenge is: 

 

<mark style="background-color:grey">sourcetype=winregistry friendlyname</mark>

 

and then, we will have to expand the result and look at the <font color='roylblue'>registery_value_data</font> field to find the name of the USB device.

 

\-     Based on the search result we had in Splunk, and the flag format

```
-          X: Date and time when the USB plugged on device  (YYYY-MM-DD:HH:MM:SS)
-          Y: The Machine name 
-          Z: Name of the USB device
-          Flag format: flag{X:Y:Z:A}
```

 

We have the flag:       <mark> flag{2016-08-24:10:42:17:we8105desk:MIRANDA_PRI}</mark>

***

 

Happy Practicing & Learning!

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/27/AdW3yEBXLRlZ6pY.png)