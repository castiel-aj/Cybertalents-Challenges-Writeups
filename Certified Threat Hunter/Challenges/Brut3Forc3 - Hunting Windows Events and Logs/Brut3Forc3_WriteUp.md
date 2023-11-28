<center><b><h1>Bruteforce</h1></b></center>

***

<center>

![image-20231127202738052](https://s2.loli.net/2023/11/28/4MSoJHZiE2w8Tb6.png)



From the descripton we know that:

- We will be looking for the source of the web brute force a;ack.
- Happened to our server 192.168.250.70 which is the destination.
______________________________________________________________________________
![image-20231127202752567](https://s2.loli.net/2023/11/28/2uJFzZUtQfP1mV4.png)



I started off with this search :

- Sourcetype=”stream:h1p” >> cuz in the description they mentioned the a;ack was by a
  web so will first focus on h1p traffic

- dest_ip=192.168.250.70 >> the a;ack happened in this server so we are looking for all
  the h;p traffic to this destination.

- h1p_method =POST >> we are interested in POST requests since logins are usually
  performed through POST requests .

  

  ![image-20231127202820638](https://s2.loli.net/2023/11/28/tBkwmuVRvEA5o6d.png)

  

  

  No, we see here the result of the search.

- I scrolled down to the src_ip field we see that there are two ip addresses but witch one
  of them is the a;acker’s?
  We will check both to know.

![image-20231127202849923](https://s2.loli.net/2023/11/28/GwtvTQo2zHRm4Sl.png)



- I started with src_ip 40.80.148.42

![image-20231127202903087](https://s2.loli.net/2023/11/28/wfkJjL8vrpCyEoA.png)



- We checked the form_data > “The form_data field contains information that we want to
  check when dealing with POST requests.”
- We see here nothing indicates that there was a bruteforce a;ack so .. we will check the
  other IP address.

![image-20231127203110445](https://s2.loli.net/2023/11/28/EQoHAb2XOyPMnWc.png)

![image-20231127203127826](https://s2.loli.net/2023/11/28/IspVW6RkQBCf24U.png)

- So, it seems <b>23.22.63.114</b> performed brute force attack.
- But we need to make sure by :

index=botsv1 sourcetype=stream:http dest_ip=192.168.250.70
http_method=POST form_data=*username*passwd* | stats count by src

![image-20231127203227247](https://s2.loli.net/2023/11/28/v85UefnaABXym71.png)

- We can see the count for the 23.22.63.114 is way higher than the other IP address cool
  so indeed did a brute force a;ack on the server.

  <mark>X:23.22.63.114</mark>

____________________________________________________
- Now we need to know if the brute force was successful by :
index=botsv1 sourcetype=stream:http dest_ip=192.168.250.70
http_method=POST form_data=*username*passwd* | stats count by src
index=botsv1 sourcetype=stream:h;p form_data=*username*passwd*
dest_ip=192.168.250.70 | rex field=form_data
"passwd=(?<userpassword>\w+)" | stats count by userpassword | sort -
count

![image-20231127203312866](https://s2.loli.net/2023/11/28/BLYixtpHf5bCurT.png)

- “The search above extracts every user password and counts the itemes it has been
  seen/used. If a password is seen more than one .me, this probably means that a;ackers
  got a hit and used the password again to log in. This is why we are sor.ng on count.”
- We see here that the password used for the login is batman
  The password average Length is: 6
  So I tried it in the flag and it was correct
  <mark>Y:6</mark>
  Flag{X_Y}  - <mark>flag{23.22.63.114_6}</mark>

***

Happy Practicing & Learning!

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/t28QypJLXn9lezg.png)