# cybertalents-writeups
**WEB**
**Admin has the power:**

first as always checking the source code, and i found (user:support password:x34245323)
so i tried them and i logged in
it came up with a message :
Hi support
Your privilege is support , may be you need better privilages !!
so i checked the cookies from ,rightclick-> inspect-> storage-> cookies
and i found the cookie with role "support"
changing it to admin then refreshing, i got the flag



**This is sparta:**

login page with a button saying hint, after clicking it says "easier than abelton", so i searched for abelton and didn't find anything related,
let's have a look at the source code
found a script at the end of the code that's obfuscated so i'm copying it and let's look for an deobfuscation tool online so we can know what does it do
using the tool at https://deobfuscate.io/ i was able to get deobfuscate the code to :
function check() {
  var _0xeb80x2 = document.getElementById("user").value;
  var _0xeb80x3 = document.getElementById("pass").value;
  if (_0xeb80x2 == "Cyber-Talent" && _0xeb80x3 == "Cyber-Talent") {
    alert("                      Congratz \n\n");
  } else {
    alert("wrong Password");
  }
} which reveals the user and password as "Cyber-talent"
let's try them
and i got the flag in the alert



**I am legend:**

a login form again, now after inspecting the soource code , we find a weird script that's written in []+ characters
kept looking for kind of obfuscation this is for long till i found that it's jsfuck as that's the type of obfuscation characters
so i tried multiple online tools to deobfuscate it and none worked
and after a deeper search i found jspoison which is similar to jsfuck, i tried the tool i found at https://filipemgs.github.io/poisonjs/
after deobfuscation i found the flag in the code 



**Cryptography:**
**Crack the hash:**

using the hashed value  1ab566b9fa5c0297295743e7c2a6ec27 on an online hash decrypting tool https://hashes.com/en/decrypt/hash it was the flag and hashed using md5 algorithm



**Guess the password:**

using the hashed value  06f8aa28b9237866e3e289f18ade19e1736d809d on an online hash decrypting tool https://hashes.com/en/decrypt/hash it was the flag and hashed using SHA1 algorithm



**postbase:**

since the value BR3tCNDUzXzYxWDdZXzRSfQ== ends with == i suspect it's a base64 encrypted so let's try decrypting it using cyberchef
i got a random value
looking back at the challenge ,i found [corrupted] at the beginning of the encrypted value 
so i'm going to remove letters from the beginning of the text till i find something that looks like a flag
after removing the first letter i found the text G{value} so that means the "flag" word was the thing corrupted here and we got the value


**Forensics:**
**G&P list:**

download the file and use grep tool to find "flag/Flag/FLAG",
grep Flag 'G&P+lists.docx' got binary file matches
so i'm using --text to get the text from the binary
grep Flag --text 'G&P+lists.docx'
got the flag



**cypher anxiety:**

downloaded the zip file and after extracting we get a .pcap file
so let's inspect using wireshark
found a conversation starting with "hey bro" so let's follow the tcp streap
we find the conversation stating that the 2 users will change there conversation to an encrypted channel using cryptcat and the passowrd is P@ssawordaya using the traffic 7070.
Let's filter these network traffic by typing tcp.port == 7070.
after saving the traffic at port 7070, we will use Netcat to listen on the traffic that passed on this port
Open terminal in the folder where we saved the file and create a listener to netcat using "netcat localhost 7070 < file.txt
This command let us intiate a listenner on port 7070 and take input from file.txt which is the wireshark file we saved before
Open another terminal in the same location and type "cryptcat -l -k P@ssawordaya -p 7070 > file2.txt"
In this command we start with cryptcat which is the method of encryption followed by -l to print the output in the same folder followed by -k and the passowrd then -p for port number and put the ouptut in file named file2.txt in the location that is managed by l option.
we get an image named file2.txt.
 As the challenge description mentioned that the flag is in md5 format, we use md5sum file2.txt and boom we get the flag




**Hidden message:**

looks like we have steganography ctf here
downloaded the .jpg file used exiftool to inspect the image information
exiftool hidden_message.jpg and found the copyright notice in md5 format and the challenge stated that we should submit the flag in md5 format so that's the flag














