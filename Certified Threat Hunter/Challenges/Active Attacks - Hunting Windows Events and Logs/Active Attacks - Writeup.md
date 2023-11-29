<center><b><h1>Active Attack - Writeup </h1></b></center>

***

![image-20231129144705935](https://s2.loli.net/2023/11/29/fPlhiG1IcUpodYL.png)

Since this  account failed to login, it has event id <b>4776</b> for <b>failed login</b> from domain controller. The domain controller in this case is <b>HYDRA-DC.MARVEL.local</b>.

Since chainsaw has rules to detect certain events , you can use the following command to hunt for events

| 1  2  3 | ./chainsaw/chainsaw-gnu hunt -r ./chainsaw/rules/  logs.evtx |
| ------- | ------------------------------------------------------------ |
|         |                                                              |



This returns a lot of output , but retunes events in a format we can easily comprehend.

![image-20231129144747922](https://s2.loli.net/2023/11/29/6JaPp4cYjOoh2mw.png)

| 1  2  3 | ./chainsaw/chainsaw-gnu hunt --sigma  ./chainsaw/sigma/ --mapping ./chainsaw/mappings/sigma-event-logs-all.yml  -r ./chainsaw/rules/lateral_movement/ logs/ |
| ------- | ------------------------------------------------------------ |
|         |                                                              |



You can use the command above to get more info. Now here is where the fun begins.

From the logs we can see that there are several users like pbarker,fcasle, Administrator and these events have a common IP address <b>“192.168.80.128”</b>

If we search for the following users in the sigma output , we can find the <mark>SID</mark>

<b>pbarker</b> : S-1-5-21-271597537-2992796785-3713134209-1105

<b>fcastle</b>: S-1-5-21-271597537-2992796785-3713134209-1103

<b>Adminitrator</b> : S-1-5-21-271597537-2992796785-3713134209-500

The structure of an SIDis as follows :

S-1-5-21--<relative_id>

Where:

S: A constant prefix indicating that it is a Security Identifier.

1: Revision number (currently always 1).

5: Identifier authority value (the identifier authority for Windows is always 5).

21: The identifier authority’s top-level domain identifier. The actual number may vary depending on the Windows version or configuration but is typically 21 for Windows domains.

: The SID for the domain. It is a unique value assigned to each domain by the domain controller during domain creation.

<relative_id>: A relative identifier that uniquely identifies a specific security principal within the domain. For users and groups, this relative ID is usually the RID (Relative Identifier) assigned by the domain controller.

so in this case domain sid is “S-1-5-21-271597537-2992796785-3713134209”

To get the workstation you can use the command we used earlier to filter events using event id

| 1  2  3 | ./chainsaw/chainsaw-gnu search -t 'Event.System.EventID: =4776' logs/ \| grep -i workstation |
| ------- | ------------------------------------------------------------ |
|         |                                                              |



![image-20231129144836711](https://s2.loli.net/2023/11/29/FWQuV2XzlLxsmw1.png)

workstation: THEPUNISHER

![image-20231129144848465](https://s2.loli.net/2023/11/29/uXhEiPI69fqT23R.png)

flag is <mark>Flag{S-1-5-21-271597537-2992796785-3713134209_192.168.80.128_THEPUNISHER}</mark>

***

 

Happy Practicing & Learning!

 ![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/t28QypJLXn9lezg.png)
