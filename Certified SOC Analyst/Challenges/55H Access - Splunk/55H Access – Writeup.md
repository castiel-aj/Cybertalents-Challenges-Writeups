

<center><b><h1>55H Access – Writeup</h1></b></center>

_______________



\-     We start our search query with: <font color='blue'> SSH service </font>



and specifying time for <font color='blue'> "All Time" </font>	

this will show us all the SSH service messages that were logged.

\-     Then we start filtering based on the required options field to get our flag info:

**X: How many source IPs attempting to connect → Number**

X = from <font color='blue'> "src_ip" </font> field value = <mark>19</mark>

**Y: The Source IP with the most connections → x.x.x.x**

Y = from <font color='blue'> "src_ip" </font> field value = <mark>91.224.160.108</mark> 

**Z: The Source IP with the most connections country → xxxxxxx**

Z = from <font color='blue'> "srccountry"  </font>field value = <mark>Netherland</mark>

**W: The Firewall action taken from the security control → xxxxxxx**

W = <mark>blocked</mark> (based on <font color='blue'> "action" </font> value)

<mark style="background-color:red">flag{19:91.224.160.108:Netherland:blocked}</mark>



However, this flag gave me<font color='red'> **"wrong submission"** </font>  

So, after asking my friends, I found that the trick in the Geolocation of the IP address (Netherland) 

I deeply searched the location of the IP "**91.224.160.108**" and it turned to be from <mark>Finland</mark>!	 

Now we the new flag: <mark>**flag{19:91.224.160.108Finland:blocked}**</mark>

and it is correct!

***


Happy Practicing & Learning!

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/27/RiUaokZBX2pucDT.png)

 

 