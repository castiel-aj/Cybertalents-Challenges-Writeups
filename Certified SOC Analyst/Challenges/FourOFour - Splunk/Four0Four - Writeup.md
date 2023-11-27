<center><b><h1>Four0Four – Writeup</h1></b></center>

***



\-     They told us that the attack targeted our <font color='red'>IIS</font> server...

and the first question (**X: The highest number of <font color='green'>non existent URLs request</font> sent by the attacker → Number**)

tell us that we should filter the search output to only "<font color='green'>not found - code 404 messages</font>" 

 

so, we start our search with a simple query: 

 

<font color='blue'>sc_status="404"</font>

this will give us 2119 events. However, we should keep filtering based on the rest of information provided to us.

\-     we check the <font color='blue'>c_ip</font>field, and find that it has 2 values (public IP and Private IP)

Of course, we will select the public IP address to add to the search and we will copy it as an answer to:

 

**Y: The Source IP → x.x.x.x**

 

<mark>Y =  40.80.148.42</mark>

 

\-     our search query now is: <font color='aqua'>sc_status="404" c_ip="40.80.148.42"</font>

 

we only add on more filter to it from the field <font color='blue'>sourcetype</font> which has one value "iis"

 

and our search query now is: <font color='blue'>**sc_status="404" c_ip="40.80.148.42" sourcetype=iis**</font>

which is enough to get all the rest of the answers

 

 

**X: The highest number of non existent URLs request sent by the attacker → Number**

<mark>X:       2009</mark> 

 

**Z: The attacker source country → xxx**

We use any IP address lookup tool to map the IP address to geolocation (ex: [iplocation.net](https://www.iplocation.net/) )

 and the result is USA

<mark>Z:  USA</mark>

 

we collect all the answers and have the flag as below:

<mark>flag{2009:40.80.148.42:USA}</mark>

***

 

 Happy Practicing & Learning!

 

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/27/GnEXWRFqKDJHTux.png)