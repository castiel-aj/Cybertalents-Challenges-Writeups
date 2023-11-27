<center><b><h1>MEGO Challenge</h1></b></center>

Mego is hiding something on his desktop and he always kept the secrets on the cloud 

 

 Link:https://hubchallenges.s3.eu-west-1.amazonaws.com/Forensics/memdump123456789.mem.tar.gz

***

 

\- First, I tried to check the strings inside the mem dump file , and filtering the output to match only the word "flag" using the command:

 

$ cat file_name | strings | grep "flag"

 

I found interesting hint in the result:

 

<mark>C:\Users\admin\Downloads\flag.txt.zip</mark>

But currently, we can do nothing with it .....

So, we’ll need a tool to dump info from our file.  <font color='blue'>**(Volatility Tool)**</font>

***

 

\-     <font color='red'>*tutorial Video to install Volatility3:*</font>

https://www.youtube.com/watch?v=HKRZohqJEMM



Follow the steps to install Volatility (version 3 i.e. compatible with Python3) in Linux based systems. 

I have selected Volatility3 because it is compatible with Python3. 

Note: To run Volatility3 the commands & plugin names for Volatility3 are different that volatility2.

 

\-     Steps are reproduced below for copy pasting: 

\-----------------------------------------------

Installing Volaitity in Kali Linux:

\-----------------------------------------------

1. Download Volatility3 source code zip file from 

 https://www.volatilityfoundation.org/...

2. Extract it & rename it for simplicity.

 

3. Install Python if not available (in my system it is already installed): 

 $ sudo apt install python3

 

4. Open Terminal and install dependencies for volatililty using below cmd:

 $ sudo apt install python3-pip python-setuptools build-essential

 

5. Navigate into the volatility directory and hit the below cmd to install volatility: 

 $ sudo python3 setup.py install

 

and installation is complete.

 

Check using cmd:

 $ python3 vol.py

***



\- We start by trying to determine image info by using the volatility tool:

$ python3 vol.py -f /path_to_mem_dump_file windows.info

 

from the output we notice that the image belongs to:   **NTBuildLab   7601.17514.amd64fre.<mark>win7sp1</mark>_rtm.**

so... windows7sp1 

\- Now, we know which profile to use: (win7sp1) and we know which file to scan for (the "flag.txt.zip" file). So, we use it with the command:

 

$ python3 vol.py -f /path_to_mem_dump_file windows.filescan | grep -i "flag"

 

we'll have a result of all the files that matches "falg"

we choose the one that located in the path (C:\Users\admin\Downloads\flag.txt.zip) to dump it by specifying its physical address in the command:

 

$ python3 vol.py -f /path_to_mem_dump_file windows.dumpfiles --physaddr 0x50dc4370 

 

now we'll have a <mark>file.flag.txt.zip.dat</mark> . we rename to have a <font color='green'>**.zip**</font> file in order to open it ...

unfortunately, it has a password....

 

we can use any password cracking tools (fcrackzip , John the Ripper, ....)

 

To use john the Ripper tool, we need to have the hash of the file...

and in order to do so, we will convert our zip file into a txt file by using the command:

 

$ zip2john zip_file_name.zip > zip_file_name.txt 

now, we confirm that we have a hash for the file by using the command:

 

\# cat zip_file_name.txt

the result of the previous command would be a hash!

After that, it's time to crack that hash by the tool "John the Ripper" with the command:

\# john zip_file_name.txt 

(This may take some time depending on your device hardware)

(The default wordlist of john the ripper did not crack the password......)

 

So, based on the challenge intro (<mark>the user always keeps his secrets on the cloud</mark>), we try to check the browser history. However, volatility3 does not support the needed plugin <mark style="background-color:red">(iehistory)</mark> which only works on volatility2...

(I tried a lot to find a replacement of the "iehistory" plugin for volatility3, but with did not succussed...

So, we’ll use another Linux machine which has volatility2 to check the browser history)

the command is:

 

$ python2 vol.py -f memdump.mem --profile=Win7SP1x64 iehistory

 

 

from the output, this link was interesting:

<mark>Record length: 0x480</mark>

<mark>Location: Visited: admin@https://www.google.com/search?hl=ar-AE&source=hp&q=<font color='red'>aHR0cHM6Ly9naXN0LmdpdGh1Yi5jb20vZWd5Y29uZG9yL2VlYTQyZWZkY2M4YWZmZjZlY2E3ODllZmFkMDkyNGY0</font>&btnG=%D8%A8%D8%AD%D8%AB+Google%E2%80%8F&iflsig=AINFCbYAAAAAYNklB-nHZ11BsWPswjKaNT4sXGZcL73d&gbv=1</mark>

<mark>Last modified: 2021-06-28 00:25:40 UTC+0000</mark>

 

So, we’ll try to decode it using base64 with the command:

echo <font color='red'>"aHR0cHM6Ly9naXN0LmdpdGh1Yi5jb20vZWd5Y29uZG9yL2VlYTQyZWZkY2M4YWZmZjZlY2E3ODllZmFkMDkyNGY0" | base64 -d </font>

 

and the result was a link for a repository of a wordlist:

 

https://gist.github.com/egycondor/eea42efdcc8afff6eca789efad0924f4

 

I downloaded the new wordlist from that link and used it with john the ripper to crack the .txt file

 

when finished, we can see the cracked hash password among the result. However, to make the result (password) clearer

we can use the command:

 

$ john zip_file_name.txt --show

the password was:  <mark>g=ax6w{JPtHL./FdE&8ASVbu$rcmG?zZ</mark>

 

and after using to open the .zip file, I got the flag :)

 

the flag is: **flag{FF571983C5693A57024858E6529A7408D16791846918}**

***



Happy Practicing & Learning!

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/27/AHO6nIvJCbcVt1F.png)