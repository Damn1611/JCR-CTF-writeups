# Joint Cyber Range

A CTF platform from Joint Cyber Range

The national facility for cyber security education in the Netherlands. Developed by and for higher and vocational education.
> Quick note, I completely forgot to write anything down. The information provided might not be 100% accurate or missing as a whole. It's all based off of my memory.

## Overview

```
Title                                    Category                                   Solved?
---------------------------------------- ------------------------------------------ -------
Disclaimer - ReadMe                      Chapter 1                                  Yes
Acceptance letter                        Chapter 1                                  Yes
The start of a journey                   Chapter 1                                  Yes
HiddenEntrance2                          Chapter 1                                  Yes
HiddenEntrance                           Chapter 1                                  Yes
Missing shopping list                    Chapter 1                                  Yes
AliceSSH                                 System                                     Yes
Obfuscation 101                          Transfiguration                            Yes
Obfuscation 102                          Transfiguration                            Yes
Obfuscation 103                          Transfiguration                            Yes
Obfuscation 104                          Transfiguration                            Yes
Obfuscation 105                          Transfiguration                            Yes
Obfuscation X                            Transfiguration                            Yes
Something went wrong...                  Transfiguration                            Yes
Getting back on Bob                      Charms                                     Yes
Wireshark 101                            Defense Against the Dark Digital Arts      Yes
Wireshark 102                            Defense Against the Dark Digital Arts      Yes
Wireshark 103                            Defense Against the Dark Digital Arts      Yes
Wireshark 202                            Defense Against the Dark Digital Arts      Yes
```

> The challenges that I haven't mentioned here I didn't do. And some dont have the solution because I cant recall what he challenge was fully.
## Disclaimer - Readme

**Solution**

Read the given text and type in the flag. If you failed this one I cant be friends with you. Sorry.

## Acceptance letter

**Challenge**

You got accepted to participate in the CTF, congratulations. Here's an image!

**Solution**

Opening the image with notepad reveals the flag inside the data. At first I was thinking of `steghide`. But this challenge was slightly easier.

## AliceSSH

**Challenge**

Alice isn't good with securing her private keys. Find the keys.

**Solution**

The IP-address along with the port were given. Upon scouring the page and looking at other challenges I found the username and password to both be `alice`

`ssh alice@ipaddress -p port`

In the `/` folder there's a `.ssh/` folder. In here is an unprotected file containing the first flag.

## Obfuscation 101-105

**Challenge**

The flags are hashed or obfuscated using basic methods. ROT13, base64, hex, binary etc.

**Solution**

Basic knowledge about obfuscation should get you right through these problems. [Cyberchef](https://gchq.github.io/CyberChef/) helped a lot during this. Definitely the best all-round tool for CTF's.

## Obfuscation X

**Challenge**

A string can be obfuscated multiple times. Find the flag.

**Solution**

This is basically the same as Obfuscation 101-105 but combined to add an extra level of spice.

## Something went Wrong...

**Challenge**

Your classmate tried compressing a zip file but unfortunately it got corrupted. Can you help him retrieve the information?

**Solution**

Unzipping the file revealed 4 files. `f`, `l`, `a` and `g`. None of them had a file extension. The first thing I did was checking the file data using the `file` command. `f` came up as .odt, `l` and `a` as data and `g` as dBase III. I changed both `l` and `a` to a .ZIP file. and unzipped them again using the following command: 

`zip -FF a.zip --out output.zip`

This basically fixes the corrupted data to an extent. Running this gave me a extremely low-res image for `l` and an XML file named context.xml for `a`. the XML file contained the flag. 

## Getting back on Bob

**Challenge**

Bob forgot his password, can you help him retrieve it?

**Solution**

I used nmap to scan for open ports where I found that port `1022` was open and not mentioned in any other challenge. 

I tried the usual username and password along with the port that I found and it worked. Passwords are saved in `/etc/shadow` but they're hashed. Bob's password was also hashed in that file. I grabbed the entire string that belonged to bob and ran it through `John The Ripper`. It only took a second and I found the password to be `bob9`.

## Wireshark 101

**Challenge**

which TCP flag set clearly shows that it is an nmap scan.

**Solution**

by going through the file and looking at the flags it shows that the TCP flag `RST` happened after `SYN` and `SYN, ACK`

## Wireshark 102

**Challenge**

The attacked used a backdoor vulnerability. find the CVE number of that vuln.

**Solution**

When looking through the protocol hierarchy I've found that `FTP` was being used. i looked at the frames and it showed a username and password that were being used to log in. when tracing it back it showed that it was from `vsFTPd 2.4.3`. Quick google search on backdoors later and I had the CVE number.

## wireshark 103

**Challenge**

The attacker left a message. Retrieve that message.

**Solution**

By going through every single frame, I've found that the attacker left a message in a `.txt` file. It was in written in octal though, so a quick sweep through cyberchef gave the flag.
`You Have BEEN PWnED`.

## wireshark 202

**Challenge**

The attacker hid a flag somewhere. Find it.

**Solution**

Honestly. I just went through every frame and scanned till I had something that caught my eye. Pain. 

# Conclusion

I really enjoyed solving these challenges, they were really interesting. as for difficulty, I think that some were too easy(Obfuscation) and some were too hard(Charms). But that shows my abilities and what I should improve on. For my first CTF it went surprisingly well. I would like to thank the entire JCR team for the CTF, it has been a pleasure.
