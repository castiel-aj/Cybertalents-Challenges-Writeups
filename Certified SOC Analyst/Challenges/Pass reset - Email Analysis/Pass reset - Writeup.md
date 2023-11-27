<center><b><h1>Pass Reset - Writeup</h1></b></center>

***

 

\- First, we need to crack the password of the zip file

 

we can use any password cracking tools (<font color='red'>fcrackzip , John the Ripper</font>, ....)

 

To use john the Ripper tool, we need to have the <font color='green'>hash</font> of the file...

and in order to do so, we will convert our zip file into a txt file by using the command:

 

<mark style="background-color:grey">"$ zip2john zip_file_name.zip > zip_file_name.txt </mark>

 

now, we confirm that we have a hash for the file by using the command:

 

<mark style="background-color:grey">\# cat zip_file_name.txt</mark>

 

the result of the previous command would be a <font color='green'>hash</font>!

 

After that, it's time to crack that hash by the tool "John the Ripper" with the command:

 

<mark style="background-color:grey">\# john zip_file_name.txt </mark>

 

(This may take some time depending on your device hardware)

 

When finished, we can see the cracked hash password among the result. However, to make the result (password) clearer

we can use the command:

 

<mark style="background-color:grey">$ john zip_file_name.txt --show</mark>

 

 

(Password of zip file is: <mark>infected</mark>)

 Now it’s time to make use of the available information of the message header according to the flag format:



![img](https://s2.loli.net/2023/11/27/pKUHzRuOQSaFXVg.png)



\-     After opening the **.msg** file using Outlook, we seek the information of the email message to solve the challenge:

 

from:  <mark style="background-color:Turquoise">file--------info----------properties</mark>

we can get to the header information which are located in the "from:  <mark style="background-color:grey">internet headers</mark>"window

![img](https://s2.loli.net/2023/11/27/vHkzgUGpMnt8joX.jpg)

 from there, we can find:

 

**X: The sender mail ID =**   <mark>roger@captech.com</mark>

**Y: The date that user received the email (DD/MM/YYYY)** =       <mark>25/02/2022</mark>

**Z: The domain name of associated URL on mail body (ABC.com) =** 

 

The mail body can not be accessed in the same previous way…

So, we will open the .msg file using notepad in order to reach the mail body context.

 

the email body is encoded in <font color='red'>**base64:**</font>

![img](https://s2.loli.net/2023/11/27/asOKgoCJ9z6b2Qe.jpg)

 

After decoding it we find this line: 

<mark style="background-color:grey">To Keep or reset your password, visit the following address:</mark>

 

<mark style="background-color:grey">Click here to keep or reset your</mark>

<mark style="background-color:grey">password<https://www.attemplate.com/eur/10338048-193a </mark>

 

So, **Z** = <mark>attemplate.com</mark>

**W: Do you think this email is more likely to be legitimate or suspicious, add <font color='red'>L</font> for legitimate or <font color='red'>S</font> for** suspicious    = <mark>S</mark> 



The flag is: <mark>flag{roger@captech.com:25/02/2022:attemplate.com:S}</mark>

***

 

Happy Practicing & Learning!

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/27/GnEXWRFqKDJHTux.png)

 

 