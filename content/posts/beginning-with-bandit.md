---
title: "beginning with bandit"
date: 2019-11-21T14:29:20Z
draft: false
toc: true
images:
tags:
  - overthewire
---


When I began the Bandit wargame on OverTheWire dot org, I didn't expect to finish it. In the event that I did, I told myself I'd make a

![your image](/images/blogcrop2.gif)

Then I would put a write up on it. Due to unforseen circumstances, I accomplished all three things. The write up turned out to be the most Herculean task of them all.

As I sat there redoing the challenges from start to finish, fetching my commands, arranging them into some easily digestible sequence that would fit my narrative, I realised something. The OverTheWire staff really, really don't want write ups of these wargames on the net.

They don't want them on the net enough to find [reddit posts](https://www.reddit.com/r/netsec/comments/4j76ap/overthewire_wargamesguide_to_bandit_levels_125/) of infosec learners advertising their blog - broadcasting, perhaps, the only kind of content their skills at this time will allow - and comment on them with sad faces.

I mercilessly pruned my proofs-of-concept. My humble, factual tone evaporated. The inconsistent yarn I am left with will likely please neither the staff nor the friends to whom I now write.

Here it is, guys. This is the idiot thing I have edited into oblivion. I can only hope you'll find it useful.


## Level 0:

> The goal of this level is for you to log into the game using SSH. The host to which you need to connect is **bandit.labs.overthewire.org**, on port 2220. The username is **bandit0** and the password is **bandit0**. Once logged in, go to the Level 1 page to find out how to beat Level 1.

Do you know why you should read the man pages? Here’s why you should read the man pages. I was trying to ssh in from memory. I was like, oh, p*ssh*, I’ve done this before. They’ve given me the info, I’ll just spew out the arguments like so:

```
n615:~ user$ ssh bandit0@bandit.labs.overthewire.org 2220
bandit0@bandit.labs.overthewire.org's password: 
Permission denied, please try again.
```


I presumed the port number could be tacked on as a generic argument at the end. Not so; this isn't telnet. If you want to specify an ssh port other than the default 22, you’re going to need the `-p` option. I like [this](https://stackoverflow.com/a/40654885) explanation of arguments and options and such.

Everyone messes up the command options or argument order once in a while. That’s why you should read the man pages.

## Level 0-1

> The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

There are several commands you’ll be using constantly from now on to be able to look and get around. Learn how to get _out_ of directories as well as _in_. Get the flag. Seize the means of production.

## Level 1-2

> The password for the next level is stored in a file called - located in the home directory

`cat` got your tongue? (Sorry.)

You can start by checking its usage in the man pages first of all, to see why it doesn’t work as you’d expect.

Second of all, everything that can be stored in a Linux file system is identified by its unique path. If you can picture every directory that was entered to get to this location, you can construct the absolute path for this oddly-named file and feed it to `cat` - or indeed any other command that expects a file as an argument.

But in practice, nobody knows - or wants to type out - the whole entire absolute path for everything. What if you couldn’t leave bandit1’s home directory? (You can.) What then? (Think about it anyway.)

## Level 2-3 

> The password for the next level is stored in a file called spaces in this filename located in the home directory

If you read the stack overflow answer I linked earlier, you might see how a file with spaces in its name could present a problem with how commands are interpreted.

I personally let autocomplete solve this challenge for me, though.

## Level 3-4

> The password for the next level is stored in a hidden file in the inhere directory.

This challenge should make you realise that hidden files aren't exactly a stellar security measure. Hidden files tend to store config details or user preferences, and are generally only removed from view for the purpose of decluttering the average directory listing.

## Level 4-5

> The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

```
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere/
bandit4@bandit:~/inhere$ ls
-file00  -file02  -file04  -file06  -file08
-file01  -file03  -file05  -file07  -file09
bandit4@bandit:~/inhere$ cat ./-file00
??????????~%	C[?걱>??| ? 
```

You could just `cat` every single file this way, but that's not why you're here. All this time you've been typing single commands for the shell to interpret, but it's more than capable of doing something a bit more programmatic.

Did you know you can use a semicolon to separate and execute commands sequentially on one line?

```
bandit4@bandit:~/inhere$ echo you; echo do; echo now
you
do
now
```

## Level 5-6

> The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties: human-readable, 1033 bytes in size, not executable


```
bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere/
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere04  maybehere08  maybehere12  maybehere16
maybehere01  maybehere05  maybehere09  maybehere13  maybehere17
maybehere02  maybehere06  maybehere10  maybehere14  maybehere18
maybehere03  maybehere07  maybehere11  maybehere15  maybehere19
bandit5@bandit:~/inhere$ 
```

If only there was a command that could allow you to find files with really specific criteria. 


## Level 6-7

> The password for the next level is stored somewhere on the server and has all of the following properties: owned by user bandit7, owned by group bandit6, 33 bytes in size

Somewhere.

```
bandit6@bandit:~$ ls
bandit6@bandit:~$ ls -la
total 20
drwxr-xr-x  2 root root 4096 Oct 16  2018 .
drwxr-xr-x 41 root root 4096 Oct 16  2018 ..
-rw-r--r--  1 root root  220 May 15  2017 .bash_logout
-rw-r--r--  1 root root 3526 May 15  2017 .bashrc
-rw-r--r--  1 root root  675 May 15  2017 .profile
```

Not here. But even if you apply your knowledge from the previous level, you’ll get a lot of errors drowning out what you actually want to see. Use google to figure out how to stop this.

On an unrelated note, all complaints about this blog post should be sent to /dev/null.

## Level 7-8

> The password for the next level is stored in the file data.txt next to the word millionth

I have a present for you.

```
bandit7@bandit:~$ ls
data.txt
bandit7@bandit:~$ head data.txt 
humiliation's	47r0YuNylaQ3k6HqGF5NsPPiGuolDCjn
malarkey's	0huyJeRwvtJaoyRmJjQFsRnQcYG4gDir
prioress	ocudTlq9CbpCw9aByrqGffAuoYvCmLNV
enlivened	a7zT1gFekL2pB54py3NmJkYluxdAscwO
bony	r5GbTRzr0dsAMEuiBO8sznt0v56nci5z
transatlantic	ttoxcePeynPXWS1fnQTBWtij9uQwbBfJ
earliness	ikmPFX39MF1mrIfRvTMIFnBGyZV3T2Fa
rump's	nFY7k2ua3xfV5oScoBQsPhrwKjeKVwam
rink's	vzsUxoBeDiy7wo7SW1CnXZUYEOIUuoiw
sierras	fUB5nuau8pLD55Wi4u6R8x4SDxqBUXfd
```

That present is the `head` command (and its counterpart, `tail`). It’s extremely convenient if you have reason to expect that a file is large and don’t want to clutter your terminal with all lines read at once.

But it’s not actually relevant to the solution of this challenge. Sorry.

## Level 8-9

> The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

```
bandit8@bandit:~$ ls
data.txt
bandit8@bandit:~$ head data.txt 
KerqNiDbY0zV2VxnOCmWX5XWxumldlAe
MsxcvOe3PGrt78wpZG2bBNF5wfXpZhET
L0nxAwlfV9V3J5onKIT8KYQ9InTcQ7yE
4c7EsUtqLnLR9hiepV5EQVhdMgyi8onL
1drBmDT7PYS7hVgoTWkJSjUZUK7ZAIAa
L0nxAwlfV9V3J5onKIT8KYQ9InTcQ7yE
78rgduVcLZjLzZmooObdaN541MKV6IfQ
x0bga8Oxz5lgM8k52HrYy4ez7XJI0lM0
irGm6F73sbUrFhHukhp6JXgMQyLxJTz1
YzZX7E35vOa6IQ9SRUGdlEpyaiyjvWXE
```

`grep` won’t save you now! But that’s okay. The OverTheWire website will still prove useful at this point with hints for commands you can research. 

## Level 9-10

> The password for the next level is stored in the file data.txt in one of the few human-readable strings, beginning with several ‘=’ characters.

```
bandit9@bandit:~$ ls
data.txt
bandit9@bandit:~$ head data.txt 
ʿ?|g?{Li&??G?[?W?K??z
Ђ?`B6haѩW??T2?*D?"??i?EJ?MPC?n鮝??O?{Ov??q?lk?.MBB??I>?[?dW?V?t?8s??m???Bt??{
```

Have you ever wondered why this gibberish displays as it does? What does human-readable vs. non-human-readable actually mean? And what on earth is a Chinese glyph meaning ‘dried fish’ doing in data.txt???

```
bandit9@bandit:~$ file data.txt 
data.txt: data
```

Files are sequences of bytes. File formats signal for these bytes to be interpreted a certain way with particular bytes in in particular places.

This file (much like this blog post) is painstakingly crafted yet all over the place, and aims to teach you something. `file` can’t be sure what it is, though, hence the highly descriptive output.

As for `cat`, it will have the terminal attempt to display the byte values as characters in a printable format. It will fail for many of them. One value, though, seems to match the Unicode for ‘dried fish’. Nya nya.

Anyway, you’ve been assured that there’s wheat in this chaff. So there’s surely a way to separate it.

## Level 10-11

> The password for the next level is stored in the file data.txt, which contains base64 encoded data

```
bandit10@bandit:~$ ls
data.txt
bandit10@bandit:~$ cat data.txt 
VGhlIHBhc3N3b3JkIGlzIElGdWt3S0dzRlc4TU9xM0lSRnFyeEUxaHhUTkViVVBSCg==
```

The main takeaway from this level should be that those equal signs at the end are generally a dead giveaway of something that’s base64-encoded.

That’s it. That’s the one thing you’ll remember from Bandit, even if you forget all the other stuff.

## Level 11-12


> The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

ROT-13 is not used to scramble anything important, ever. It seems to serve entirely as a hat tip to the aspiring cryptographic badass. It's also featured [on that one show about leet hackers](https://www.youtube.com/watch?v=i9CBKGLVCME).


## Level 12-13

> The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

This challenge is good. Why is it good? Because it forces you practise the thing, over and over again, until you’re screaming “I understand it, already! No more!”

```
bandit12@bandit:~$ ls
data.txt
bandit12@bandit:~$ file data.txt 
data.txt: ASCII text
bandit12@bandit:~$ head data.txt 
00000000: 1f8b 0808 d7d2 c55b 0203 6461 7461 322e  .......[..data2.
00000010: 6269 6e00 013c 02c3 fd42 5a68 3931 4159  bin..<...BZh91AY
00000020: 2653 591d aae5 9800 001b ffff de7f 7fff  &SY.............
00000030: bfb7 dfcf 9fff febf f5ad efbf bbdf 7fdb  ................
00000040: f2fd ffdf effa 7fff fbd7 bdff b001 398c  ..............9.
00000050: 1006 8000 0000 0d06 9900 0000 6834 000d  ............h4..
00000060: 01a1 a000 007a 8000 0d00 0006 9a00 d034  .....z.........4
```

Work in a directory of your own creation, as suggested. You don’t have write permissions to this one, even though you’re bandit12. This is a measure to keep important challenge directories from being… de*filed*. B) 

You may notice that you can’t autocomplete the names of any directories in tmp, even if you are one character off the full correct name of a directory that you _know_ is in there. That’s also to do with permissions.

Directories have their own entries in the file system, so their permissions can be set just like any file. A directory needs to be readable, otherwise `ls` won’t work and thus won’t let the user leverage autocomplete.

## Level 13-14

> The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

```
bandit13@bandit:~$ ls
sshkey.private
bandit13@bandit:~$ file sshkey.private 
sshkey.private: PEM RSA private key
```

Ah, the private key. The thing you shouldn’t let anyone read. It’s easy enough to research how to use it, so I’ll explain localhost instead.

How have you been progressing from one level to the next? Have you been logging out, then sshing in from your own machine every time? Now you must realise that you can, in fact, ssh from one bandit account to another if you have some way to authenticate - be it password or private key. Here’s an example.

```
bandit12@bandit:~$ ssh bandit13@localhost
Could not create directory '/home/bandit11/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit11/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit12@localhost's password:
```

This works because you are working in an ssh session logged in as bandit12, and localhost points to that machine (which is technically remote relative to your own).

Why is the port omitted? Going from your own machine you needed to specify port 2220 because that's what was open to hosts *external* to the OverTheWire network.

But if you're already logged into a user on that network, the default port 20 is open for sshing internally. You can verify this with `nmap`, which will come up in a few levels’ time. 

Also, don’t forget to `cat` the password when you get there.

## Level 14-15

> The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

This was another one I did off the top of my head. I first used `telnet`, but `telnet` is a loser and we can do better. Research the better thing. It is incredibly useful.

## Level 15-16

> The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.
Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…
Another case of RTFmanpage. Personally, I didn’t run into the situation that their helpful note mentions. Maybe if you read the manpage well enough, you won’t either.

So you might have realised by now. You can’t just walk through life expecting the terminal to give you helpful prompts all the time. Sometimes you’re going to get something that looks like it’s hanging, but isn’t.

Test it. Type stuff anyway. `whoami` is a great option if you have no idea; it prints what user you’re logged in as. Very nice for illustrating solutions, but **as you know** I decided to cut those out.

## Level 16-17

> The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.


Meet `nmap`, your new best friend.

I recommend you use the `-sV` flag for service detection. It predicts what service could be listening on open ports. I first solved this one without it and didn’t learn the useful thing early enough.

Also meet vim, that one friend you keep avoiding. At least learn how to create files, edit files, and how to exit the damn thing.

Well, what else are you suggesting I remotely edit files with? _emacs?_ And I suppose you would also have me roll around in the mud like a common sow?

But seriously. The reason you should know how to use vim is similar to another reason why you should read the man pages. If you truly intend to go digging around remote machines, you’re not always going to be able to use your favourite text editor. In the same way, it’s best to be comfortable using the most accurate and built-in documentation possible.

## Level 17-18

>There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new
NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19

Have you ever looked at diffs on github? Turns out they aren't just a git thing.

## Level 18-19

> The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

```
n615:~ user$ ssh bandit18@bandit.labs.overthewire.org -p 2220
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames

bandit18@bandit.labs.overthewire.org's password: 
Linux bandit 4.18.12 x86_64 GNU/Linux   
Welcome to OverTheWire!
---
Byebye !
Connection to bandit.labs.overthewire.org closed.
```

As the prophecies foretold, you’re instantly logged out. My first false instinct was to try viewing and/or editing bandit18’s `.bashrc`.

```
bandit17@bandit:~$ cd ..
bandit17@bandit:/home$ ls
bandit0   bandit14  bandit2   bandit25      bandit29      bandit31-git  bandit7
bandit1   bandit15  bandit20  bandit26      bandit29-git  bandit32      bandit8
bandit10  bandit16  bandit21  bandit27      bandit3       bandit33      bandit9
bandit11  bandit17  bandit22  bandit27-git  bandit30      bandit4
bandit12  bandit18  bandit23  bandit28      bandit30-git  bandit5
bandit13  bandit19  bandit24  bandit28-git  bandit31      bandit6
bandit17@bandit:/home$ cd bandit18
bandit17@bandit:/home/bandit18$ ls -la
total 24
drwxr-xr-x  2 root     root     4096 Oct 16  2018 .
drwxr-xr-x 41 root     root     4096 Oct 16  2018 ..
-rw-r--r--  1 root     root      220 May 15  2017 .bash_logout
-rw-r-----  1 bandit19 bandit18 3549 Oct 16  2018 .bashrc
-rw-r--r--  1 root     root      675 May 15  2017 .profile
-rw-r-----  1 bandit19 bandit18   33 Oct 16  2018 readme
```

But the file has the same restricted permissions as the readme itself. As bandit17, we can do nothing.

Recall that we have bandit18’s password and can actually login with ssh. Maybe you should stop taking that utility for granted and see how else it can be used.

Also if you didn’t know, `bash` is itself a statement that can be invoked. So is `exit`. If you find a way to inspect `.bashrc`, you will be able to see that the offending lines added are merely the following:

```
echo 'Byebye !'
exit 0
```

Up till now, once you’ve supplied the correct login credentials for a user with ssh, that user’s login shell is launched. In this case it’s the bash shell that we’re coming to know and love, but with a modified `.bashrc`. The shell exits before you even get to the command prompt, logging you out of your ssh session.

_But wait,_ you may cry. _Isn’t it `.bash_profile` - or something - that goes with login shells, not `.bashrc`?_

I thought so too, but inspecting the `.profile` file in the same directory reveals that things have been set up to include .bashrc anyway:

```
# if running bash
if [ -n "$BASH_VERSION" ]; then
    # include .bashrc if it exists
    if [ -f "$HOME/.bashrc" ]; then
	. "$HOME/.bashrc"
    fi
fi
```

## Level 19-20

> To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

```
bandit19@bandit:~$ ls -l
total 8
-rwsr-x--- 1 bandit20 bandit19 7296 Oct 16  2018 bandit20-do
```

I’m going to ~~hope~~ assume that you have done some of your own reading on permissions and can meaningfully read the above by now. The s flag may still be new. 

That flag being set where it is allows the executable to be run with the privileges of its owner (in this case bandit20). If it was instead set where the x is, the executable would be run with the privileges of the bandit19 user group.

Since this level is pretty straightforward, I’ll forgo any further advice and instead tell you about how I went on a silly adventure to find out the userid of bandit20 then pass it as an argument to the binary.

The moral of the story is: don’t do that.


## Level 20-21

> There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).
> NOTE: Try connecting to your own network daemon to see if it works as you think

Your own network daemon. The source of your SYNs.

It's easy to go astray here. I thought about that setuid binary first and got stuck. It needs a port, but *what* port?

Whatever its value, it surely won’t be that of any well known service like ssh. What service could it be? What service is it expecting? Even if you desperately `nmap` for an answer, you won’t find what you need.

Because the service it’s expecting is as simple and specific as “something that connects and yields a line of text”. After all, the binary needs something to read. *You* can create this service, using the pipes and redirections that are hopefully becoming more familiar to you by now.

In the end, the port value only matters insofar as the two halves of the connection - listener (or n̶et̵̀w̸͠o҉͜r̶k͏̶ d̨a҉̧eḿ̢͞ơn̶̛) and initiator - know where to meet. This level is tricky because you have to make both, in the same session, when you’ve only really been initiating so far.

## Level 21-22

> A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

Job control. A thing we all wish we could have more of. Let’s follow the instructions.


```
bandit21@bandit:~$ cd /etc/cron.d
bandit21@bandit:/etc/cron.d$ ls
cronjob_bandit22  cronjob_bandit23  cronjob_bandit24
bandit21@bandit:/etc/cron.d$ file cronjob_bandit22
cronjob_bandit22: ASCII text
bandit21@bandit:/etc/cron.d$ cat cronjob_bandit22
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```
Remember /dev/null/? Where you should send your complaints about this blog post? Looks like other stuff’s being binned there too. 

That script file should look interesting to you. Your clues are in there.


## Level 22-23

> A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed. NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

We know there’s a usr/bin/cronjob_bandit23.sh. Let’s see what it’s doing.

```
bandit22@bandit:~$ cat /usr/bin/cronjob_bandit23.sh 
#!/bin/bash

myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```

It's good to work out in your head what's going on with all those pipes, but you can also just feed it to the command prompt and it'll evaluate it all for you.


## Level 23-24

> A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed. NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level! NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

As before, check out that /usr/bin/cronjob_bandit24.sh.

```
bandit23@bandit:~$ cat /usr/bin/cronjob_bandit24.sh 
#!/bin/bash

myname=$(whoami)

cd /var/spool/$myname
echo "Executing and deleting all scripts in /var/spool/$myname:"
for i in * .*;
do
    if [ "$i" != "." -a "$i" != ".." ];
    then
    echo "Handling $i"
    timeout -s 9 60 ./$i
    rm -f ./$i
    fi
done
```

It's executing *all* the scripts in that directory as bandit24. That means it's time for you to write your own and shove it in there.

As you may have worked out, scripts consist of bash commands to execute line by line. This saves you from having to churn out hacky one-liners. Keep in mind:

1. The script's first line must be `#!/bin/bash`
2. The script file must have executable permissions set
3. Scripts are run in the same way as setuid binaries: `./script.sh`
4. `.sh` is only a convention, you can name the script anything

In this case your script will be deleted once you put it in the right directory, so work in the tmp directory first.

```
bandit23@bandit:~$ mkdir /tmp/fathoms23
bandit23@bandit:~$ cd /tmp/fathoms23
bandit23@bandit:/tmp/fathoms23$ vim getpass
```

Your solution need only consist of about three lines. If you run into permissions issues later:

1. Check the permissions of your script
2. Check the permissions of anything you create in the script
3. Check the permissions of the directory you made in tmp

Anything created by your script must be readable to everyone else. You're only bandit24 for the duration of that script. When it finishes, you are everyone else.

```
bandit23@bandit:/tmp/fathoms23$ cp getpass /var/spool/bandit24
bandit23@bandit:/tmp/fathoms23$ date
Fri Nov 29 15:57:17 CET 2019
bandit23@bandit:/tmp/fathoms23$ ls
getpass
bandit23@bandit:/tmp/fathoms23$ ls
getpass  newlyappeared
bandit23@bandit:/tmp/fathoms23$ date
Fri Nov 29 15:58:44 CET 2019
```



## Level 24-25

> A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.

For now, let’s try to connect and see how the daemon behaves.

```
bandit24@bandit:~$ nc -v localhost 30002
localhost [127.0.0.1] 30002 (?) open
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
<FLAG_REDACTED> 9999
Wrong! Please enter the correct pincode. Try again.
Timeout. Exiting.
```

Notice how you must form your input, as well as the timeout.

```
bandit24@bandit:~$ date
Mon Dec  2 11:53:17 CET 2019
bandit24@bandit:~$ nc -v localhost 30002
localhost [127.0.0.1] 30002 (?) open
I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Timeout. Exiting.
bandit24@bandit:~$ date
Mon Dec  2 11:53:40 CET 2019
```
You can tell after connecting, then idling, that the listening is dropped quickly. Don't worry about that just yet.

As you should know from level 20-21, you can pass strings to `nc`. You can `nc` with that passed, repeatedly with a different pin each time. You can probably tell a loop should be involved.

I tried to think about inputs, and what this might teach for real situations in the wild. I’m aware that word lists or files of input like this tend to be supplied as input to password crackers. So let’s try and create one of those to make things easier.

```
bandit24@bandit:~$ mkdir /tmp/fathoms24
bandit24@bandit:~$ cd /tmp/fathoms24
bandit24@bandit:/tmp/fathoms24$ ls
bandit24@bandit:/tmp/fathoms24$ for i in {0000..9999}; do echo "$(cat /etc/bandit_pass/bandit24) $i"; done >> /tmp/fathoms24/inputlist
-bash: fork: retry: Resource temporarily unavailable
bandit24@bandit:/tmp/fathoms24$ ls
inputlist
bandit24@bandit:/tmp/fathoms24$ head inputlist 
<FLAG_REDACTED> 0000
<FLAG_REDACTED> 0001
<FLAG_REDACTED> 0002
<FLAG_REDACTED> 0003
<FLAG_REDACTED> 0004
<FLAG_REDACTED> 0005
<FLAG_REDACTED> 0006
<FLAG_REDACTED> 0007
<FLAG_REDACTED> 0008
<FLAG_REDACTED> 0009
```

We pass it with the following line, which reads line after line of input from your list and sends it over the connection while pruning anything that comes back wrong. It should work.

```
bandit24@bandit:/tmp/fathoms24$ nc localhost 30002 < /tmp/fathoms24/inputlist | grep -v "Wrong"

I am the pincode checker for user bandit25. Please enter the password for user bandit24 and the secret pincode on a single line, separated by a space.
Timeout. Exiting.
```

But it doesn’t. There’s a timeout.

We can surmise it might be due to computational resource restrictions (as flagged by that fork resource unavailable message from before) causing a delay in processing 10,000 lines and submitting them to a listener. In the end, the time taken to process it all seems to prove greater than the timeout built into the service.

You’ll need to batch it somehow - the space/quantity of pins is too large to do all in one go. I gave you some presents in level 7-8. I personally used those. A bit of trial and error worked like a charm.


## Level 25-26

> Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

There’s an ssh key here. Let’s use it to log into 26.

```
bandit25@bandit:~$ ssh -i bandit26.sshkey bandit26@localhost
Could not create directory '/home/bandit25/.ssh'.
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:98UL0ZWr85496EtCRkKlo20X3OPnyPSB5tB5RPbhczc.
Are you sure you want to continue connecting (yes/no)? yes
Failed to add the host to the list of known hosts (/home/bandit25/.ssh/known_hosts).
This is a OverTheWire game server. More information on http://www.overthewire.org/wargames
...

  For support, questions or comments, contact us through IRC on
  irc.overthewire.org #wargames.

  Enjoy your stay!

  _                     _ _ _   ___   __  
 | |                   | (_) | |__ \ / /  
 | |__   __ _ _ __   __| |_| |_   ) / /_  
 | '_ \ / _` | '_ \ / _` | | __| / / '_ \ 
 | |_) | (_| | | | | (_| | | |_ / /| (_) |
 |_.__/ \__,_|_| |_|\__,_|_|\__|____\___/ 
Connection to localhost closed.
```

Well, that last bit of ascii art is certainly new. We’re also instantly logged out. How do we get around this? That ssh trick with command execution won’t work. It hangs.

We’ve been told bandit26’s shell is not the /bin/bash we’re used to using. How can we find out what bandit26 is using? By looking in /etc/passwd. Though password hashes are no longer stored here, there's still some useful information about the users on the machine.
```
bandit25@bandit:~$ cat /etc/passwd | grep "bandit26"
bandit26: x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext
```

Normal bash’s path is /bin/bash. This shell is at /usr/bin/showtext. Turns out we can read it.

```
bandit25@bandit:~$ cat /usr/bin/showtext
#!/bin/sh

export TERM=linux

more ~/text.txt
exit 0
```

That’s it. A tiny custom toy shell made just for this challenge. All this login shell does is export an environment variable then run that `more` command on whatever text.txt is in bandit26’s home directory is, before terminating, i.e. logging us out.

```
bandit25@bandit:~$ ls -la /usr/bin | grep showtext
-rwxr-xr-x  1 root     root          53 Oct 16  2018 showtext
```

The permissions don't allow us to edit this shell or anything. But we have plenty of other leads. Maybe there’s a way to exploit how the shell works.

If you don’t know what `more` is, look it up. It’s a paging command. Research paging. Paging should be a familiar sort of concept. Why? Because manpages use pagers! That's how we navigate through them. (Did you know you can `man` `man`?)

If you look at the man page for `more`, it’s there in the description. A filter for paging through text *one screenful at a time*.

Some things should be clicking by now, if you’re literally thinking out of the box. That text.txt in bandit26’s home directory - which we can’t read, but can guess pretty well from all this info - is that ascii art. That art is being paged through with `more`. One screen-full at a time.

So why didn't we get any telltale signs of it being a pager? Why didn't it seem to behave like a man page? Because the terminal screen we’re most likely using is likely bigger than the total contents of that ascii art.

If we made our terminal screen really short - shorter than the amount of lines in the file - and only then logged in as above, could we get into that paging state? If we’re in that paging state, where we don’t scroll past the end of the file, would that mean our exit 0/logout is delayed?

Yes. But what then? Pager exploits. OverTheWire even suggests we look at how vim works. In `more` you can press v to start up a vim-type editor. Fly free, my pretties, and research the rest.


## Level 26-27

> Good job getting a shell! Now hurry and grab the password for bandit27!

Leave the shell-weirdness of the previous level behind so you can maneuver more comfortably. Basically, just while you’ve got that shell in bandit26, use your setuid knowledge to get the password for 27 and log into what is presumably a nice normal shell.


## Level 27-28

> There is a git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo. The password for the user bandit27-git is the same as for the user bandit27. Clone the repository and find the password for the next level.

Time to practise a bit of git. Make your own directory to work in and clone into it.

## Level 28-29

> There is a git repository at ssh://bandit28-git@localhost/home/bandit28-git/repo. The password for the user bandit28-git is the same as for the user bandit28. Clone the repository and find the password for the next level.

Begin as before.

```
bandit28@bandit:/tmp/fathoms28/repo$ ls
README.md
bandit28@bandit:/tmp/fathoms28/repo$ cat README.md 
# Bandit Notes
Some notes for level29 of bandit.

## credentials

- username: bandit29
- password: xxxxxxxxxx
```

Woe is you, it's been redacted. But if you know anything about git, you'll know it's good at tracking repository history and changes. If something was once written there, there's most definitely a way to check and revert.


## Level 29-30

> There is a git repository at ssh://bandit29-git@localhost/home/bandit29-git/repo. The password for the user bandit29-git is the same as for the user bandit29. Clone the repository and find the password for the next level.


Git repositories have branches. By default you commit changes to just the master branch, but if you're doing things right, you branch off into dev, and production, and this or that feature, and so on.

```
bandit29@bandit:/tmp/fathoms29/repo$ cat README.md 
# Bandit Notes
Some notes for bandit30 of bandit.

## credentials

- username: bandit30
- password: <no passwords in production!>
```

If commit history for your current branch isn't turning up much, it would follow to check the others. And any "sploit" stuff you may come across is a silly red herring. 


## Level 30-31

> There is a git repository at ssh://bandit30-git@localhost/home/bandit30-git/repo. The password for the user bandit30-git is the same as for the user bandit30. Clone the repository and find the password for the next level.

```
bandit30@bandit:/tmp/fathoms30/repo$ ls
README.md
bandit30@bandit:/tmp/fathoms30/repo$ cat README.md 
just an epmty file... muahaha
```

Seeing as the file is so "epmty", let’s `log`.

```
bandit30@bandit:/tmp/fathoms30/repo$ git log
commit 3aa4c239f729b07deb99a52f125893e162daac9e
Author: Ben Dover <noone@overthewire.org>
Date:   Tue Oct 16 14:00:44 2018 +0200

    initial commit of README.md
```

Nope.

So I spent a good while on this one, because there was very little to go off and the solution involves you knowing about the existence of one particular git detail.

The detail is tags. Tags denote versions. Now you know they exist. Find the tag here. The flag is inside. It *looks* like a commit hash but it's *not*.

## Level 31-32

> There is a git repository at ssh://bandit31-git@localhost/home/bandit31-git/repo. The password for the user bandit31-git is the same as for the user bandit31. Clone the repository and find the password for the next level.

If you've ever used git in practice, even a little, then this challenge checks that you have the bread-and-butter add-commit-push process down.

```
bandit31@bandit:/tmp/fathoms31/repo$ cat README.md 
This time your task is to push a file to the remote repository.

Details:
    File name: key.txt
    Content: 'May I come in?'
    Branch: master
```

There's a little gotcha after you finish following the instructions, but git is *so* nice that it tells you outright how to solve it.


## Level 32-33

> After all this git stuff its time for another escape. Good luck!

Alright. Let's try things.

```
WELCOME TO THE UPPERCASE SHELL
>> whoami
sh: 1: WHOAMI: not found
```

As you might expect, everything you type is being turned to uppercase. I went down a rabbithole related to `stty`, so let me tell you now it's got nothing to do with any of that.

I also tried looking in /etc/passwd as bandit31, but due to permissions the custom shell is not readable. So there's no file to decipher. Looks like we need to try other things.

What’s uppercase? Environment variables are uppercase. Will they give me something?

```
>> $TERM
sh: 1: xterm-256color: not found
```

Doesn’t help too much. Or does it? It seems the variables *are* actually evaluated. Maybe there's something we can evaluate to get a foothold.

## Level 33

If you've managed to get to the end, you can see what lies here for yourself. Thank you for reading.