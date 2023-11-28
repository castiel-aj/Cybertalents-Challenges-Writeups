<center><b><h1>Within Code - Writeup</h1></b></center>

***

 

![img](https://s2.loli.net/2023/11/28/aHNGxig9CpBSkQM.jpg)

 

\-     After downloading the zip file, we found a folder that contains many binary files.

\-     To search in binary / text files, we use Yara tool (which is available in Linux, Windows):

To start, we need to know

What we’re searching in order to create a suitable Yara rule for it. Looking at the **Description** of the challenge, it seems like the word **flag** might be the word we should look for “*Flag rises within the code*”

 

To create a role that matches the word “**Flag**” in binary files, we need to match the binary or the hex of the word “**Flag**”

Within the targeted folder.

\-     We encode the word “Flag” to base64 using [Base64Guru](https://base64.guru/converter/encode/text) website, and the result is: RmxhZw==

![img](https://s2.loli.net/2023/11/28/KC1pTxs5Gmvh9WV.jpg)

We also convert our base64 result to Hex using any tool like [magictool](https://magictool.ai/tool/text-to-hex-converter/) website to use it in our Yara rule, and the

Result is: 526d78685a773d3d

![img](https://s2.loli.net/2023/11/28/E6DOpbnwLTIJSk9.jpg)

 

**Note**: using either of the Base64 encoding or the Hex form would be enough to match for the word “Flag”, but we used both to avoid trying again…

 

\-     Now that we have the info that need to match for, we can create our Yara rule. We wrote a simple rule to match 

For both the encoding and the Hex form, and the rule is:

***



rule Withincode

{

  strings:

​    

​    $encoded_flag= "RmxhZw=="

​    $hex_flag = {526d78685a773d3d}

 

  condition:

​     $encoded_flag or $hex_flag

}

***





![img](https://s2.loli.net/2023/11/28/dU7DvkwHzbLtZhg.png)

 

\-     Finally, before running the Yara rule, we need to know which option to use with it..

And since we do not want to match for the file that contains the defined string in our rule, we will not choose the **-f** option as we usually do…. 

 

![img](https://s2.loli.net/2023/11/28/X4Nk2D38nMPOS6q.png)

However, we’re going to use the **-s** option which will give us the offset location of the string in the matched file (for more explanation about the Yara options use the command ($yara - - help) 

 

Our used command is: $yara -s rule.yara Within\code

 

![img](https://s2.loli.net/2023/11/28/6XM9ozSHVpwvjyY.png)

 

Submitting this location (0x2460) in its Hexadecimal form was not accepted. So, we converted it back to decimal using 

[Rapidtables](https://www.rapidtables.com/convert/number/hex-to-decimal.html) website and had the result: 9312

 

![img](https://s2.loli.net/2023/11/28/gMsv7CzbQ2DUIyF.jpg)

And the flag is:  <mark>flag{9312}</mark>

***

Happy Practicing & Learning!

 ![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/t8J7r1QwSjA6xLO.png)
