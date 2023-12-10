<center><b><h1>Baseline</h1></b></center>

***

![image-20231210140551733](https://s2.loli.net/2023/12/10/gFhwb5fetLGBiHc.png)

extract the zip file
we get 2 .txt files
using a command-line tool called "diff" we can get the difference between the two files and thus our answer
we run this command:

```
diff -a baseline.txt processes.txt 
```

we get:

![img1](https://s2.loli.net/2023/12/10/oNlIxAtKecEdXfJ.png)

Let's take a look at what this output means. The important thing to remember is that when diff is describing these differences to you, it's doing so in a prescriptive context: it's telling you how to change the first file to make it match the second file.

The first line of the diff output contains:
line numbers corresponding to the first file, a letter (a for add, c for change, or d for delete), and line numbers corresponding to the second file. culled from [here](https://www.computerhope.com/unix/udiff.htm)
it simply tells us we need to add "notepad" to the baseline file, which means that it's not there and we should add "SearchProtocolHost" to both files however on different lines.
we're looking for the different process in both files. notepad is the culprit because "SearchProtocolHost" exists on both files just on different lines but notepad on exist on the processes file. so we get our flag.

using powershell(as intended)
download and extract the zip file
open powershell and 'cd' to the directory where the files are located. declare them as variables and compare them?
using these commands, you'll get the flag

```
$baseline = Get-Content baseline.txt`
`$processes = Get-Content processes.txt`
`Compare-Object $baseline $processes
```

![img1](https://s2.loli.net/2023/12/10/PF4ptUrDV3k1HdX.png)



and the flag is: **FLAG{notepad}**	

***

Happy Practicing & Learning!

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/t28QypJLXn9lezg.png)