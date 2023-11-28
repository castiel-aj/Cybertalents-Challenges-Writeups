<center><b><h1>Arson</h1></b></center>

***



![image-20231127201106679](https://s2.loli.net/2023/11/28/ywCcso1B72FjExt.png)



First things first download the Wireshark file (Arson.pcapng)

![image-20231127201134247](https://s2.loli.net/2023/11/28/inbYcLH3lmGRA84.png)



First things first download the Wireshark file (Arson.pcapng)
In the beginning, I started to go around the packets and I noticed several HTTP get requests

![image-20231127201259674](https://s2.loli.net/2023/11/28/bsKflGLwHa8hivd.png)

I assumed that the victim might have downloaded the PowerShell script from http link, so I applied http filter



![image-20231127201316334](https://s2.loli.net/2023/11/28/S13hpP5nNuz92GB.png)



And yes he did! :)
So I followed the TCP stream to download the PowerShell script

![image-20231127201339558](https://s2.loli.net/2023/11/28/mN9dCJEV7ArtufW.png)

I saved this tcp stream

![image-20231127201401669](https://s2.loli.net/2023/11/28/63JWv4pYI8n1eN7.png)

Now let’s start analyzing this PowerShell script, First thing I noticed is that the Script use Encryption and decryption mechanism which is AES CBC and it encode almost everything (key,IV,the retrieved data from the victim after encrypting it)

![image-20231127201416040](https://s2.loli.net/2023/11/28/tz6FYRO7gpw2ENh.png)

the rest of the PowerShell script is just a normal shell but the new thing and unusual is that the data is transferred to the attacker over HTTP

![image-20231127201428461](https://s2.loli.net/2023/11/28/4M85ow67rpKcDqj.png)

And this means that we should see the data that is sent to the attacker on wireshark

![image-20231127201438811](https://s2.loli.net/2023/11/28/PNEGBaln9SkAz6p.png)

I followed the TCP stream of the Post request which is marked with yellow on the image and I did saw the data that is sent to the attacker but its encrypted

![image-20231127201450056](https://s2.loli.net/2023/11/28/Kforeu15BY2TQcp.png)

There is more than one way to decrypt this data
1- use websites (use url decode website then AES decryption website)
2- write a script that decrypt this data using python or any other language
3- use the attacker PowerShell script to decrypt this data as there is also decryption function in the script
So I used the third way to decrypt the data
First thing I cleaned the PowerShell script to use only the decrypt function

function Create-AesManagedObject($key, $IV) { $aesManaged = New-Object "System.Security.Cryptography.AesManaged" $aesManaged.Mode = [System.Security.Cryptography.CipherMode]::CBC $aesManaged.Padding = [System.Security.Cryptography.PaddingMode]::Zeros $aesManaged.BlockSize = 128 $aesManaged.KeySize = 256 if ($IV) { if ($IV.getType().Name -eq "String") { $aesManaged.IV = [System.Convert]::FromBase64String($IV) } else { $aesManaged.IV = $IV } } if ($key) { if ($key.getType().Name -eq "String") { $aesManaged.Key = [System.Convert]::FromBase64String($key) } else { $aesManaged.Key = $key } } $aesManaged } function Decrypt-String($key, $encryptedStringWithIV) { $bytes = [System.Convert]::FromBase64String($encryptedStringWithIV) $IV = $bytes[0..15] $aesManaged = Create-AesManagedObject $key $IV $decryptor = $aesManaged.CreateDecryptor(); $unencryptedData = $decryptor.TransformFinalBlock($bytes, 16, $bytes.Length - 16); $aesManaged.Dispose() [System.Text.Encoding]::UTF8.GetString($unencryptedData).Trim([char]0) } $key = "llm0xB8WOfv9Ssq9+f0sIMFK6OyQHOzhdenMzRInqXA=" $ip = "192.168.1.11" $port = "7788" $implant_name = "razer" $sleep_time = 5 # The encrypted string you provided $encryptedString = "Your-Encrypted-Data-After-URL-Decoding-It" # Decrypt the string $decryptedString = Decrypt-String $key $encryptedString # Output the decrypted string $decryptedString



You can use the above PowerShell code if you want to decrypt any data that is retrieved by the attacker just replace: 

$encryptedString = "Your-Encrypted-Data-After-URL-Decoding-It"

with your encrypted data and then run the script.
Note: Remember to decode it first using URL decode, You can use any website that does URL decode, I used this website urldecoder.io.
Now after decrypting this encrypted data which you found in the post requests, you will get the flag:

IN3DZMA9y5D0q5y4Pe3Uv%2FVE3mA4EZY55XHJJIdLc29WAK73bE2DzB7ae%2Fmpy4CW

<b>flag{2C_p0w3r_Chi11}</b>



Note: It is possible that when you run the powershell, an error occurs running scripts is disabled on this system
The solution is to simply go to cmd and type Set-ExecutionPolicy RemoteSigned
The script will work, but after you finish, and if you do not intend to run PowerShell scripts, it is better to go back to how you were before, to be more secure, so you will write in cmd: Set-ExecutionPolicy Restricted



***

Happy Practicing & Learning!

![Microsoft Office Signature Line...](https://s2.loli.net/2023/11/28/t28QypJLXn9lezg.png)