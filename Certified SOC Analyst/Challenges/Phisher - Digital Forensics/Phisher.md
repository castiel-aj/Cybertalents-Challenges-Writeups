<center><b><h1>Phisher – Writeup</h1></b></center>

***



![img](https://s2.loli.net/2023/11/27/iqYwuhRIU1ajLF8.jpg)

 

\-     We’re provided with a <font color='green'>Disk imaged</font> in a zip file, and we’re told that properly we have an employee who fell as a victim for a <font color='royalblue'>phishing attack.</font>

 

So, we’re going to use <font color='green'>FTK imager</font> tool on windows to open the Disk image file, and check for any lead for the phishing attack (<font color='royalblue'>an email, a malicious website, malicious file</font>….) 

 After adding the evidence file (the disk image) to the FTK tool, we realis that the user of the machine called “**chrollo**”.

![img](https://s2.loli.net/2023/11/27/mDONHIguAyVvCqJ.jpg)

We start investigating for any lead for the phishing attack …….

 

And by expanding the “**Roaming**” folder under **Users >>>> chrollo >>>> App Data**

We find a folder called “**eM Client**”, and by googling it we find that it belongs to an <font color='royalblue'>e-mail client</font>!

\-     In order to investigate the messages of this account, we have to import them into an installed eM-client. 

So, we first export this folder from the <font color='green'>FTK tool</font> to our machine:

![img](https://s2.loli.net/2023/11/27/bjdatvWTpNZXceE.jpg)

And 2nd, download it from its [official website](https://www.emclient.com/download) and install it.

3rd, replace the folder “**eM Client**” in the path “**C:\Users\ <font color='red'>user</font>\AppData\Roaming**” with the one we extracted from FTK tool in order to open the mails of the **chrollo** user

- When opening the <font color='aqua'>eM Client</font>, we find nothing suspicious in the inbox (only 3 normal messages)

​    ![img](https://s2.loli.net/2023/11/27/S3izrYPqGBORcHC.jpg)

So, we check the other folders….. finally we find our target in the **Junk E-mail** folder

A suspicious email named “**Well Done**” and contains a suspicious <font color='aqua'>link</font>![img](https://s2.loli.net/2023/11/27/JnXefvKSb9HrGUT.jpg)



Opening the contained link take us to a [webpage](https://pastebin.com/fawJAkQW) that has the flag! 

![img](https://s2.loli.net/2023/11/27/wRyCNEeHsJIfnQ6.jpg)

 

And the flag is: <mark>Flag{Phishing_1S_an_ART!}</mark>

***



Happy Practicing & Learning!

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/27/hP5KXJz8cj42ft6.png)