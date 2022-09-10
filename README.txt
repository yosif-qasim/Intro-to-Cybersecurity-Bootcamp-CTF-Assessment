“Intro to Cybersecurity Bootcamp CTF Assessment “ — Write-up
After finishing the 12 Bootcamp sessions by cybertalents, we had a small CTF assessment with 14 challenges to implement the knowledge we gained through the past month and a half, and this is the way I solved it :
Tools used :
zsteg
cyber chef
Burp suite
Wireshark
wigle.net
Hashcat
Gimp
1 — The Mummy
category : general information
Q : A malicious program that’s primarily spread through spam emails. The infection may arrive either via a malicious script, macro-enabled document files, or a malicious link.
Flag : Emotet (Google it)
2 — Hunter
category : Web Security
Q : who can I trust?
This one was a bit tricky to solve,when you start the challenge you will start with this page :

opening the page with burp proxy and taking a quick look at the http requests

Those cookies look suss ! trying to decrypt them using cyberchef & Hashes.com will give you this :
flag = who_has_gohn_cookie; 
Ging_Freecss → try harder Gon! (hash & base64)
Hisoka → i am just a waste of time john ^_^ ()
Killua → do+you+remember+satotz (ROT13)
Hmmmmm…. satotz ? maybe satotz has the cookie ?! trying to but it as the“ flag ” cookie value and resend the request

correct !!
Falg : flag{Always_Trust_Your_Fr13nds}
3 — v13w3r
category : Web Security
Unfortunately I haven't taken any screenshots of this challenge nor xCode but it’s basically an Image upload site that isn’t secured very well with one input filed to put the image url you want the solution is just butting XSS payloads after the Url — onclick=alert(xss)
Flag : flag{loOks_You_ar3_xSs_mast3r_1337}
4 , 5 — Encoding 1 & Encoding 12
category : Cryptography
Both can be easily solved using CyberChef :

solving Encoding 2
6 — WoW
category : OSINT
you will be provided with this screenshot , and asked to find the exact location of this router —latitude & longitude

my approach was to use the BSSID as the key to this puzzel , didnt work out at all on any public mac finder tool except for wigle.net’s advanced search which gave me the correct info :


8— on1ons
category : Digital Forensics
you will be provided with a ‘.xcf’ file , what is that ?

ok, let’s start investing the file and then open it in gimp


gimp gives us the first have of the flag in a layer , hmm… interesting, let’s further investigate the file itself…

ok ! that should do it , we have a full flag now
9 — Pure Meyow
category : Digital Forensics
THE HARDEST ONE !!!!!!
you are provided with this image , with the goal of extracting a flag

i wasted a lot of time & effort trying out many steganography tools { zsteg , steghide , stegcracker , fotoforensics.com ,stegsolver 😤 , and many more….} thinking that there is a flag in the image that i can’t see immediately

after a long time and an awful headache i tried using zsteg again

did you notice that ? those dots must be Morse code !
nope , they arent ,they are actually a representation of ones & zeros
( dot = 1 , space = 0 )
doing that with onlinestringtools.com will result in this string :

using CyberChef , we have a flag !

10 — Elliot Secrets
category : Digital Forensics
you will be presented with a ‘.bin’ file , Dont waste your time trying linux commands and github tools , just go to CyberChef and upload the file it will find all hidden files within ( YES it can do that )
كمل هنا يا جو
11 — Refresher
category : Network Security
you will be provided with a ‘pcap’ file , opening it using Wireshark will show you an overwhelming number of packets

inspecting closely you will notice that its mostly uploading images from a user

extracting all the files from the stream will show us the 37 troll images and the 20 nonexist


but after more investigation in the tcp stream you will notice that there is another zip file in the end “secret.zip”

exporting that will lead us to a flag.txt protected by a password , hmmmm , a password ?

have you noticed that 3rd character in each image ? they represent the 37 char password to the flag.txt file !
12 — R0uge
category : Network Security
you will be provided with a file named “ r0uge_spoofed.hccapx ” and we need 4 values

, i haven’t seen that file extension before … lets try to know what does it contain

wow that was super useless

Nice , but what is exactly HCPX & .hccapx ?and what is this repeating pattern ? all i found was this https://hashcat.net/wiki/doku.php?id=hccapx , so i tried using hashcat with the file to crack it
hashcat -m 22000 r0uge_spoofed.hccapx /usr/share/wordlists/rockyou.txt

success !
follow me :
linkedin 
twitter 
@yosif_qasim — at any other site
Thanks for Reading — I hope you enjoyed this :)

