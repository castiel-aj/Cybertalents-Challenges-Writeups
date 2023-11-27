 

<center><b><h1> Bean - Writeup</h1></b></center>

***



link for the victim website:

http://wlemj0wz0k1twzoer4gvmkxal3dmrdzlxxqxcyzl-web.cybertalentslabs.com/

 

\-----------------------------------------------------------

 

we start by inspecting the source code <mark style="background-color:grey">(using ctrl + u)</mark>, but we find nothing interesting....

then we check the <font color='red'>cookies</font> from the browser developer tools... also we find nothing...

 

 

now we try to <font color='royalblue'>brute force scan</font> the website to know its folders and directories 

we use:  <mark style="background-color:green">( dirb )</mark> or <mark style="background-color:green">(dirsearch)</mark> .....

 

with the command: <mark style="background-color:grey">#dirb the_link_of_website</mark>     

or <mark style="background-color:grey">dirsearch -u the_link_of_website</mark>

 

the <font color='red'>dirb</font> tool will try all the words in the <B>"common.txt"</B> file located in:

/usr/share/dirb/wordlists/common.txt

 

and then report us with the results

both tools will find that there are 2 directories:  <mark>index.html , files</mark>

the directory <font color='green'>(files)</font> is the one that is helpful for us because the other one is empty

 

 

here... we need to search manually and try to open each directory or file...

we will start with the ones that are known as important 

(For example: the <font color='red'>shadow</font> file ... but the result was forbidden)

(Since we're in <font color='royalblue'>nginx website</font>, we open the nginx folder to check it ...

we find the configuration folder "<B>conf.d</B>" which is important for any nginx website...

in this folder, we find and open the "<B>default.conf</B>" file

and has the basic info of the server, including the port, paths, name ...

 

one of the interesting info we find, is that they're using "<font color='red'>alias</font>"

 

the alias feature or command gives a fake name to a current file or directory...



<mark>they are using alias to rename the <font color='red'>/etc/</font> directory into /files/</mark>

 

this important info we found, helps us to conclude that the we should go back instead of searching in the current

directory. 

(<mark style="background-color:green">Our hint is "Come back home Mr. Bean"</mark>.... so, we need to move back from <B>/etc/</B> to <B><font color='green'>/home/bean... </font></B>

and search there...)

 

 

we do that by inserting <b>"<font color='red'>..</font>"</b> after the <font color='green'>/files </font> 

the result link will be:

http://wlemj0wz0k1twzoer4gvmkxal3dmrdzlxxqxcyzl-web.cybertalentslabs.com/<font color='red'>**files../**</font>

 

we find that we're in the root of the server, and we find the <b>/home</b> directory

we enter it, and we find the <mark>flag.txt</mark> file which has our flag:

 

the flag is: <mark>FLAG{Nginx_nOt_aLWays_sEcUre_bY_The_waY}</mark>

***



 Happy Practicing & Learning!

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/27/7spoTq2yYxJ8D9b.png)