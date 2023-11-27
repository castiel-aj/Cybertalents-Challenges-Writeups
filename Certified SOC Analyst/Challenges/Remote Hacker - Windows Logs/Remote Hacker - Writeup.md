<center><b><h1>Remote Hacker – Writeup </h1></b></center>



***



![img](https://s2.loli.net/2023/11/27/5m28NOqZxnghpT9.jpg)



\-     As this challenge is related to windows logs, we need to be familiar with at least the common type of windows logs and the most used events ID and types. 

 

\-     To start solving this challenge, we begin by <font color='green'>filtering</font> for login events in the “Security.evtx” event log file. The login event id in windows is: **4624**, and we specify the date to match the suspected date in the challenge contexts “**16/6/2022**”.

 

<font color='red'>**Note**</font>: the [Ultimatewindowssecurity](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/) website can be very useful to find the ID of any specific windows event.

Also, [The Windows_Event_Log_Cheat_Sheet](https://www.13cubed.com/downloads/windows_event_log_cheat_sheet.pdf) will help you know the most common windows events with their IDs and brief description.

 

 

![img](https://s2.loli.net/2023/11/27/eMcB8EvDlqsuYiP.png)

We sort the result by **Data and Time** column, and start looking for a remote (network) logon <font color='aqua'>(because the challenge is about a remote hacker and not a local hacker!)</font>, which is categorized by windows as a <font color='green'>**Logon Type 3**</font>

<font color='red'>**Note**</font>: the [eventlogxp](https://eventlogxp.com/blog/logon-type-what-does-it-mean/#:~:text=The descriptions of some events,) and 3 (network).) website gives an explanataion about each type of logon in windows.

\-  The first event we find to match our logon type 3 is at **6/13/2022 8:02:15 AM:**

<center>

​                ![img](https://s2.loli.net/2023/11/27/8vPwfj5CWQlDgnL.png)



to make sure that it is the right one, we immediately copy its <font color='red'>Logon ID: 0x3C4C7D</font> and search for it in the logoff events <font color='green'>**(Logoff event ID: 4634)** </font>

<cneter>

![img](https://s2.loli.net/2023/11/27/CuGDvwOh4fJm81U.png)

 

we see that this session only lasted for **1 second** (logoff time: 08:02:16)!!

The attacker mostly will not able to execute or do any thing in only 1 sec. So, we back to search for another login with logon type 3…

The next result is:

<center>

![img](https://s2.loli.net/2023/11/27/I4LbSkC59Tjtndq.png)



![img](https://s2.loli.net/2023/11/27/vsM65JjQSyqrcxX.png)



Based on the found event info, we searched for its <font color='green'>**Login ID** 0x3D6898</font> in the logoff events, and found this event:

![img](https://s2.loli.net/2023/11/27/JWOmQoCth1Kpg98.png)



Its <font color='green'>**Loggedoff: 6/13/2022 8:05:48 AM**</font> and the related login log happened in: <font color='green'>**Logged: 6/13/2022 8:03:08 AM**</font>

So, the session duration is: <mark>**00:02:40**</mark> which is the key to question <mark>**X**</mark> (you can use this online [timecalculator](https://www.calculator.net/time-calculator.html?tcday1=&tchour1=08&tcminute1=05&tcsecond1=48&Op=-&tcday2=&tchour2=08&tcminute2=03&tcsecond2=08&tcday3=&tchour3=&tcminute3=&tcsecond3=&ctype=1&x=58&y=21) to verify)

 

And based on all the above, we now have:

 

The session duration:                    <mark>X: 00:02:40</mark>

The attacker machine host name:          <mark>A: Nitro</mark>

The attacker IP address:                  <mark>W: 192.168.1.58</mark>

 

\-     What we need to do now is to search for the application used by the hacker on the system after he logged in, 

And to identify the sha256 of that app. To do so, we have to search in “**Microsoft-Windows-Sysmon_4Operational.evtx**” event log file, as this type of events is considered a security event

The **ID** of the process creation event is **1,** so we **filter** for the event ID 1 and start looking from the time after the session login time ( <font color='green'>8:03:08 AM</font> )

We find 3 process creation events that happened during the attacker session time:



![img](https://s2.loli.net/2023/11/27/fOIcEXVnJ4AwKsF.png)

2 of the were run by **SYSTEM** <font color='green'>(</font>we knew that by looking at the <font color='green'>**ParentUser value):**</font>

![img](https://s2.loli.net/2023/11/27/Z58Q3LnTgiO6VJb.png)

 However, the third one was run by the user Kvasir:

![img](https://s2.loli.net/2023/11/27/dS8Pe7czT4kuIhJ.png)

And based on it, we find that the application used by the hacker after login is: **WIN32.CALC.EXE**

<mark>**Y: WIN32CALC.EXE**</mark>

and as for the Hash256 value of this app, we can also find it in the General info of that event log, which is:

![img](https://s2.loli.net/2023/11/27/fVTluD2qjALNHOt.jpg)

 

and by that, we have the last needed puzzle of this challenge:

<mark>**Z: 3E2300394C15B59A964EAB45D9EB96D317650E2F7448FD1B4AE825A134402B7A**</mark>

 

​	\-     Putting all the puzzles together (X, Y, Z, W, A) we get the flag which is: 


 <mark>flag{00:02:40:win32calc.exe:3E2300394C15B59A964EAB45D9EB96D317650E2F7448FD1B4AE825A134402B7A:192.168.1.58:Nitro}</mark>

***



Happy Practicing & Learning!

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/27/hP5KXJz8cj42ft6.png)