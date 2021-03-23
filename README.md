# Wargames

TODO List:
[] - go back over exercise 23 -> 24
[] - clean up syntax references on code snippets
[] - clean up overall formatting
[] - create separate scripts to add to repo

Wargames is an service setup by the awesome folks at [OverTheWire](http://www.overthewire.org).

It tests one's ability to exercise certain security concepts in the form of games.

The best part is that it's FREE and can be started by a complete beginner!!

## Modules
There are a few different "games" within the WarGames. Each is essentially getting more advanced on it's way:

[Bandit](#Bandit)

WIP:
- Natas
- Leviathon
- Krypton
- Narnia
- Behemoth
- Utumno
- Maze
- Vortex
- Semtex
- Manpage
- Drifter

Let's just get started with Bandit

## Bandit

The Bandit module consists of levels 0 - 34.

### Level 0
#### Game Instructions
>The goal of this level is for you to log into the game using SSH. The host to which you need to connect is bandit.labs.overthewire.org, on port 2220. The username is bandit0 and the password is bandit0. Once logged in, go to the Level 1 page to find out how to beat Level 1.

This level is the most basic of levels. It simply needs you to `ssh` into the game.
You'll need the login credentials (obviously):
```sh
username: bandit0
password: bandit0
```
All we have to do here is `ssh` into the WarGames.
We do this by using the `ssh` command with the `-p` flag on the port `2220` and the `bandit0` username:
```sh
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```
Then just use the password `bandit0` when prompted.

That's ijhgkjhgkjhgkjhgt! You're on your way to being a hacker!

### Level 0 -> 1
#### Game Instructions
>The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

Super simple setup here. Just `cat` the `readme` file:
```sh
cat readme

boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```
Bam! Password revealed. Now let's use the password for the next level.

### Level 1 -> 2
#### Game Instructions
>The password for the next level is stored in a file called - located in the home directory

This level is also quite simple. The password for the next level is stored in a file named `-`. So all we have to do is `ssh` using the next level `bandit1` username and  use `cat` to read the file... right?
```sh
cat -
...
```
Nope!!! They pulled a sneaky on you. Notice that when you try this, the __command line will stall__.  

In bash, the `-` will tell the interpreter to look for a `flag`. So what we need to do here is tell the command line that `-` is a **file**. How do we do this? With `./`

State that __this current directory, look for file__:
```sh
cat ./-

CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```
Boom! now you have the password and you've hacked the mainframe. Now let's go to the next level.

### Level 2 -> 3
#### Game Instructions
>The password for the next level is stored in a file called spaces in this filename located in the home directory

First, let's login using the previous password and the next login of `bandit2`:
```sh
ssh -p 2220 bandit2@bandit.labs.overthewire.org
password: CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```
So this one is fairly simple. You just need to understand how spaces `" "` work on the command line. If you just simply run `cat spaces in this filename`, you'll get This

```sh
cat: spaces: No such file or directory
cat: in: No such file or directory
cat: this: No such file or directory
cat: filename: No such file or directory
```
This is because separating by **spaces** will always look for another file. Basically you're asking `cat` to look for **4** different files. So we need to **escape** the **spaces**.  

There are two options here:
1. We can escape each space
`cat spaces\ in\ this\ filename`... escaping each space OR;
2. We can encapsulate the entire string in `" "`
`cat "spaces in this filename"`

Either one will make sure that `cat` treats the whole string as one file name... giving you the next password in the series:
```
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```
### Level 3 -> 4
#### Game Instructions
>The password for the next level is stored in a hidden file in the inhere directory.

Let's get this one going the same way we have been. Using the next level up login `bandit3`
```sh
ssh -p 2220 bandit3@bandit.labs.overthewire.org
password: UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```
Next you'll need to navigate into the `inhere` directory:
```sh
cd inhere
```
Once inside the directory, we'll need to list all files. Now a simple `ls` to list files will return blank here. So we'll need to add the `-a` flag to show **hidden** files.
```sh
ls -a
```
Alright! Now we have a file to work with named `.hidden`

Let's `cat` the `.hidden` file to see what's inside:

```sh
cat .hidden
pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

Nice! Now we have the password for the next level!!

### Level 4 -> 5
#### Game Instructions
>The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

Let's go ahead and login with the next level `bandit4`
```sh
ssh -p 2220 bandit4@bandit.labs.overthewire.org
password: pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

By the instructions of the game, let's go ahead and execute the `reset` command. Just to clear things up.

Now the game is telling us that we need to find the only **human-readable** file in the `inhere` directory.

Let's `cd` into the `inhere` directory to get to work:
```bash
cd inhere
```
When we `ls` this directory, we'll see a bunch of files starting with that pesky `-` that we came across earlier. So we know that we're going to have to use `./` to `cat` them effectively.

This particular exercise is best tackled manually. We'll simply `cat` each file and look for **human-readable** text:

```bash
cat ./-file00 ./-file01 ./-file02 ./-file03 ./-file04 ./-file05 ./-file06 ./-file07 ./-file08 ./-file09
```
```
??????????~%	C[?걱>??| ????U"7?w???H??ê?Q??(???#????T?v??(?ִ?????A*?
2J?Ş؇_?y7?.A??u??#???w$N?c?-??Db3??=???=<?W?????ht?Z??!??{?U    ?+??pm???;??:D??^??@?gl?Q??@?%@???ZP*E??1?V???̫*????
koReBOKuIDDepwhWk7jZC0RTdopnAYKh
FPn?  '?U???M??/u XS
?mu?z???хN?{??Y?d4????]3?????9(?
```

Do you see the human-readable text? Yep! That's right:

`koReBOKuIDDepwhWk7jZC0RTdopnAYKh`

Now we have the password for `bandit5`

### Level 5 -> 6
#### Game Instructions
>The password for the next level is stored in a file somewhere under the inhere directory and has all of the following properties:
human-readable
1033 bytes in size
not executable

So we're looking for a file that is:
- Human readable
- 1033 bytes in size
- Non-executable

Let's get logged in:
```bash
ssh -p 2220 bandit5@bandit.labs.overthewire.org

password: koReBOKuIDDepwhWk7jZC0RTdopnAYKh
```
There are obviously a few ways that we can tackle this one. The one that sticks out to me is the **1033 byte** file size.
This is very easy to search with `find`. And if we do happen to have a lot of files that are 1033 bytes in size, we'll further refine with the other criteria.

So let's use `find` and get this party started:
```bash
# Find in *Everywhere* and print all files 1033 bytes in size
find * -size 1033c -print
```
This gives us:
```bash
maybehere07/.file2
```
We found it! No need to further filter as it's the only file that is 1033 bytes.

Now let's just read the file and get the password:
```bash
cat maybehere07/.file2

password: DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```
Bam! Now we have the password for the next game!

### Level 6 -> 7
#### Game Instructions
>The password for the next level is stored somewhere on the server and has all of the following properties:
owned by user bandit7
owned by group bandit6
33 bytes in size

Alrighty let's get started on this badboy.

Get `ssh`'d in there:
```bash
ssh -p 2220 bandit6@bandit.labs.overthewire.org

password: DXjZPULLxYr17uwoI01bNLQbtFemEgo7
```
Now the instructions say it is **somewhere on the server**. This means that we can't operate from the `/home` directory like we have been. Let's get to root:
```bash
cd /
```
This will get us to the root directory where we can begin...

Again, let's use `find` to search these attributes. This time, however, we're going to add all of them together for one-command awesomeness:
```bash
# This command is searching Everywhere for a file owned by group `bandit6` and user `bandit7` that will be exactly 33 bytes in size
find * -size 33c -user bandit7 -group bandit6
```
This gives us the following:
```bash
bandit6@bandit:/$ find * -size 33c -user bandit7 -group bandit6
find: ‘boot/lost+found’: Permission denied
find: ‘cgroup2/csessions’: Permission denied
find: ‘etc/ssl/private’: Permission denied
find: ‘etc/lvm/backup’: Permission denied
find: ‘etc/lvm/archive’: Permission denied
find: ‘etc/polkit-1/localauthority’: Permission denied
find: ‘home/bandit28-git’: Permission denied
find: ‘home/bandit30-git’: Permission denied
find: ‘home/bandit31-git’: Permission denied
find: ‘home/bandit5/inhere’: Permission denied
find: ‘home/bandit27-git’: Permission denied
find: ‘home/bandit29-git’: Permission denied
find: ‘lost+found’: Permission denied
find: ‘proc/tty/driver’: Permission denied
find: ‘proc/7538/task/7538/fd/6’: No such file or directory
find: ‘proc/7538/task/7538/fdinfo/6’: No such file or directory
find: ‘proc/7538/fd/5’: No such file or directory
find: ‘proc/7538/fdinfo/5’: No such file or directory
find: ‘root’: Permission denied
find: ‘run/lvm’: Permission denied
find: ‘run/screen/S-bandit15’: Permission denied
find: ‘run/screen/S-bandit12’: Permission denied
find: ‘run/screen/S-bandit5’: Permission denied
find: ‘run/screen/S-bandit17’: Permission denied
find: ‘run/screen/S-bandit7’: Permission denied
find: ‘run/screen/S-bandit13’: Permission denied
find: ‘run/screen/S-bandit11’: Permission denied
find: ‘run/screen/S-bandit9’: Permission denied
find: ‘run/screen/S-bandit27’: Permission denied
find: ‘run/screen/S-bandit25’: Permission denied
find: ‘run/screen/S-bandit2’: Permission denied
find: ‘run/screen/S-bandit16’: Permission denied
find: ‘run/screen/S-bandit20’: Permission denied
find: ‘run/screen/S-bandit30’: Permission denied
find: ‘run/screen/S-bandit14’: Permission denied
find: ‘run/screen/S-bandit31’: Permission denied
find: ‘run/screen/S-bandit8’: Permission denied
find: ‘run/screen/S-bandit4’: Permission denied
find: ‘run/screen/S-bandit29’: Permission denied
find: ‘run/screen/S-bandit28’: Permission denied
find: ‘run/screen/S-bandit21’: Permission denied
find: ‘run/screen/S-bandit26’: Permission denied
find: ‘run/screen/S-bandit24’: Permission denied
find: ‘run/screen/S-bandit22’: Permission denied
find: ‘run/screen/S-bandit1’: Permission denied
find: ‘run/screen/S-bandit19’: Permission denied
find: ‘run/screen/S-bandit23’: Permission denied
find: ‘run/shm’: Permission denied
find: ‘run/lock/lvm’: Permission denied
find: ‘sys/fs/pstore’: Permission denied
find: ‘tmp’: Permission denied
find: ‘var/spool/bandit24’: Permission denied
find: ‘var/spool/rsyslog’: Permission denied
find: ‘var/spool/cron/crontabs’: Permission denied
find: ‘var/log’: Permission denied
find: ‘var/tmp’: Permission denied
find: ‘var/cache/ldconfig’: Permission denied
find: ‘var/cache/apt/archives/partial’: Permission denied
var/lib/dpkg/info/bandit7.password ## <----------------------Only file we can access
find: ‘var/lib/apt/lists/partial’: Permission denied
find: ‘var/lib/polkit-1’: Permission denied
```
Notice the large list of *permission denied* results?

This game made it a little easy for us this time. The only file we can access is
`var/lib/dpkg/info/bandit7.password`
So let's `cat` that file and bam! Password.
```bash
password: HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```

### Level 7 -> 8
#### Game Instructions
>The password for the next level is stored in the file data.txt next to the word millionth

Oooo... now it's time for some sleuthing. We need to read the `data.txt` file and find the word "millionth".

First things first, let's `ssh` into that server:
```bash
ssh -p 2220 bandit7@bandit.labs.overthewire.org
password: HKBPTKQnIay4Fw76bEy8PVxKEDQRKTzs
```
Now if we `ls` to see the current directory, we'll see a single file named `data.txt`. Lets use `grep` to search the file for "millionth"
```bash
grep "millionth" data.txt
```
This will give us:
```bash
millionth	cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```
Yay! That one was pretty easy.

### Level 8 -> 9
#### Game Instructions
>The password for the next level is stored in the file data.txt and is the only line of text that occurs only once

Let's `ssh` into the next game:
```bash
ssh -p 2220 bandit8@bandit.labs.overthewire.org
password: cvX2JJa4CFALtqS87jk27qwqGhBM9plV
```
This one seems more difficult but really isn't... Let's see what we need to do to find this file:
1. We need to `sort` all of the lines in the file
2. We then need to find out which one of these lines is *unique*

We'll use something called **Piping** `|` here.

```bash
sort data.txt | uniq -u
```
The above like uses the `sort` command to sort all lines, then uses `uniq` with the flag `-u` to find the only unique line.
```bash
password: UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```
Done and done... we just found that password... no big deal.

### Level 9 -> 10
#### Game Instructions
> The password for the next level is stored in the file data.txt in one of the few human-readable strings, preceded by several ‘=’ characters.

Let's `ssh` into the server
```bash
ssh -p 2220 bandit9@bandit.labs.overthewire.org
password: UsvVyFSfZZWbi6wgC7dAFyFuR6jQQUhR
```

This one was more of an art than anything. I simply `cat` the contents of the `data.txt` file and searched for multiple `=` signs in a row.

Found it. `truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk`

### Level 10 -> 11
#### Game Instructions
> The password for the next level is stored in the file data.txt, which contains base64 encoded data

`ssh` into the server
```bash
ssh -p 2220 bandit10@bandit.labs.overthewire.org
password: truKLdjsbJ5g7yyJ2X2R0o3a5HQJFuLk
```

Since they gave us a solid clue by mentioning the **base64** encoding, this one was pretty easy.

`cat data.txt | base64` and we get:
The password is `IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR`

Sweet.

### Level 11 -> 12
#### Game Instructions
> The password for the next level is stored in the file data.txt, where all lowercase (a-z) and uppercase (A-Z) letters have been rotated by 13 positions

`ssh` into the server
```bash
ssh -p 2220 bandit11@bandit.labs.overthewire.org
password: IFukwKGsFW8MOq3IRFqrxE1hxTNEbUPR
```
When we `cat` the `data.txt` file, we get this jumble:
`Gur cnffjbeq vf 5Gr8L4qetPEsPk8htqjhRK8XSP6x2RHh`

Based off of the game description. We know it is just rotated text 13 times. (Look up **rot13**)

Here we'll use `tr` to reverse the rot13 "encryption". A primitive form of letter scrambling (not secure).

`cat data.txt | tr 'n-za-mN-ZA-M' 'a-zA-Z'`

Now we get a print of:
`The password is 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu`

All set for the next level.

### Level 12 -> 13
#### Game Instructions
> The password for the next level is stored in the file data.txt, which is a hexdump of a file that has been repeatedly compressed. For this level it may be useful to create a directory under /tmp in which you can work using mkdir. For example: mkdir /tmp/myname123. Then copy the datafile using cp, and rename it using mv (read the manpages!)

Let's `ssh` in:
```bash
ssh -p 2220 bandit12@bandit.labs.overthewire.org
password: 5Te8Y4drgCRfCx8ugdwuEX8KFC6k2EUu
```

This one was a bit extensive. More of an art than anything else.

When we `cat` the file we get a hex hexdump
```
bandit12@bandit:/tmp/temp$ cat datanew.txt
00000000: 1f8b 0808 0650 b45e 0203 6461 7461 322e  .....P.^..data2.
00000010: 6269 6e00 013d 02c2 fd42 5a68 3931 4159  bin..=...BZh91AY
00000020: 2653 598e 4f1c c800 001e 7fff fbf9 7fda  &SY.O...........
00000030: 9e7f 4f76 9fcf fe7d 3fff f67d abde 5e9f  ..Ov...}?..}..^.
00000040: f3fe 9fbf f6f1 feee bfdf a3ff b001 3b1b  ..............;.
00000050: 5481 a1a0 1ea0 1a34 d0d0 001a 68d3 4683  T......4....h.F.
00000060: 4680 0680 0034 1918 4c4d 190c 4000 0001  F....4..LM..@...
00000070: a000 c87a 81a3 464d a8d3 43c5 1068 0346  ...z..FM..C..h.F
00000080: 8343 40d0 3400 0340 66a6 8068 0cd4 f500  .C@.4..@f..h....
00000090: 69ea 6800 0f50 68f2 4d00 680d 06ca 0190  i.h..Ph.M.h.....
000000a0: 0000 69a1 a1a0 1ea0 194d 340d 1ea1 b280  ..i......M4.....
000000b0: f500 3406 2340 034d 3400 0000 3403 d400  ..4.#@.M4...4...
000000c0: 1a07 a832 3400 f51a 0003 43d4 0068 0d34  ...24.....C..h.4
000000d0: 6868 f51a 3d43 2580 3e58 061a 2c89 6bf3  hh..=C%.>X..,.k.
000000e0: 0163 08ab dc31 91cd 1747 599b e401 0b06  .c...1...GY.....
000000f0: a8b1 7255 a3b2 9cf9 75cc f106 941b 347a  ..rU....u.....4z
00000100: d616 55cc 2ef2 9d46 e7d1 3050 b5fb 76eb  ..U....F..0P..v.
00000110: 01f8 60c1 2201 33f0 0de0 4aa6 ec8c 914f  ..`.".3...J....O
00000120: cf8a aed5 7b52 4270 8d51 6978 c159 8b5a  ....{RBp.Qix.Y.Z
00000130: 2164 fb1f c26a 8d28 b414 e690 bfdd b3e1  !d...j.(........
00000140: f414 2f9e d041 c523 b641 ac08 0c0b 06f5  ../..A.#.A......
00000150: dd64 b862 1158 3f9e 897a 8cae 32b0 1fb7  .d.b.X?..z..2...
00000160: 3c82 af41 20fd 6e7d 0a35 2833 41bd de0c  <..A .n}.5(3A...
00000170: 774f ae52 a1ac 0fb2 8c36 ef58 537b f30a  wO.R.....6.XS{..
00000180: 1510 cab5 cb51 4231 95a4 d045 b95c ea09  .....QB1...E.\..
00000190: 9fa0 4d33 ba43 22c9 b5be d0ea eeb7 ec85  ..M3.C".........
000001a0: 59fc 8bf1 97a0 87a5 0df0 7acd d555 fc11  Y.........z..U..
000001b0: 223f fdc6 2be3 e809 c974 271a 920e acbc  "?..+....t'.....
000001c0: 0de1 f1a6 393f 4cf5 50eb 7942 86c3 3d7a  ....9?L.P.yB..=z
000001d0: fe6d 173f a84c bb4e 742a fc37 7b71 508a  .m.?.L.Nt*.7{qP.
000001e0: a2cc 9cf1 2522 8a77 39f2 716d 34f9 8620  ....%".w9.qm4..
000001f0: 4e33 ca36 eec0 cd4b b3e8 48e4 8b91 5bea  N3.6...K..H...[.
00000200: 01bf 7d21 0b64 82c0 3341 3424 e98b 4d7e  ..}!.d..3A4$..M~
00000210: c95c 1b1f cac9 a04a 1988 43b2 6b55 c6a6  .\.....J..C.kU..
00000220: 075c 1eb4 8ecf 5cdf 4653 064e 84da 263d  .\....\.FS.N..&=
00000230: b15b bcea 7109 5c29 c524 3afc d715 4894  .[..q.\).$:...H.
00000240: 7426 072f fc28 ab05 9603 b3fc 5dc9 14e1  t&./.(......]...
00000250: 4242 393c 7320 98f7 681d 3d02 0000       BB9<s ..h.=...
```
First we reverse the hex dump with `xxd -r`

Now we're given a compressed file that we have no idea what program compressed it, nor do we know how many times it has been compressed. So all we can do is attempt the extraction repeatedly alternating between `tar` `gzip` and `bzip2` (the most common compressors)

Eventually the scrambled code starts to give out hints. You'll see 'data6.bin, data8.bin, etc' in the code when you use `cat`. This will give you a good idea that you're headed in the right direction. Once you're done, you'll be left with a file named `data8` with no file extension. `cat` this file and you'll get:

`The password is 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL`

Boom.

### Level 13 -> 14
#### Game Instructions
> The password for the next level is stored in /etc/bandit_pass/bandit14 and can only be read by user bandit14. For this level, you don’t get the next password, but you get a private SSH key that can be used to log into the next level. Note: localhost is a hostname that refers to the machine you are working on

As usual, we start by `ssh`ing into the machine
```bash
ssh -p 2220 bandit12@bandit.labs.overthewire.org
password: 8ZjyCRiBWFYkneahHwxCv3wb2a1ORpYL
```
Here they gave us a sweet sweet `sshkey.private` ssh key which is basically like leaving us a key under the rug.

`ssh -i sshkey.private bandit14@localhost` logs us right into the system as **bandit14** and bam, we're in.

Not just a simple `cat /etc/bandit_pass/bandit14` gives us the next pwd.

`4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e`

### Level 14 -> 15
#### Game Instructions
> The password for the next level can be retrieved by submitting the password of the current level to port 30000 on localhost.

This one we don't SSH into. We stay logged in from the last exercise and use that to send the string to port **30000** to see if we can get the next password.

Previous password: 4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e

Let's use `nc` to try to connect on port **30000**.
** Using `-v` flag to give us a little feedback
`nc localhost 30000`
You should get an **open** message.
Now we paste the password:
`4wcYUJFw0k0XLShlDzztnTBHiqxU3b3e`
Hit enter and bam: `BfMYroe26WYalil77FoDi9qh59eK5xNr`

### Level 15 -> 16
#### Game Instructions
> The password for the next level can be retrieved by submitting the password of the current level to port 30001 on localhost using SSL encryption.

> Helpful note: Getting “HEARTBEATING” and “Read R BLOCK”? Use -ign_eof and read the “CONNECTED COMMANDS” section in the manpage. Next to ‘R’ and ‘Q’, the ‘B’ command also works in this version of that command…

Similar to the last exercise, we don't log in to the game with `ssl` but rather send the previous passphrase through a port. This time it requires **SSL** so we'll be using OpenSSL to send it through to port **30001**

`openssl s_client -connect localhost:30001`

Now we can paste in `BfMYroe26WYalil77FoDi9qh59eK5xNr`and we've got the next key:
`cluFn7wTiGryunymYOu4RcffSxQluehd`

### Level 16 -> 17
#### Game Instructions
> The credentials for the next level can be retrieved by submitting the password of the current level to a port on localhost in the range 31000 to 32000. First find out which of these ports have a server listening on them. Then find out which of those speak SSL and which don’t. There is only 1 server that will give the next credentials, the others will simply send back to you whatever you send to it.

We start here by finding the ports and making sure they accept SSL:
Running `nmap` with an ssl enumerator script on ports 30000 through 32000
`nmap -sV --script ssl-enum-ciphers -p 30000-32000 localhost`

This returned quote a few ports so I ended up just trying them one by one. Turns out it was port `31790`

Using `openssl`, we send the passkey through:
`openssl s_client -connect localhost:31790`
When prompted just throw in the code:
`cluFn7wTiGryunymYOu4RcffSxQluehd`

Now we get a private key:
```
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAvmOkuifmMg6HL2YPIOjon6iWfbp7c3jx34YkYWqUH57SUdyJ
imZzeyGC0gtZPGujUSxiJSWI/oTqexh+cAMTSMlOJf7+BrJObArnxd9Y7YT2bRPQ
Ja6Lzb558YW3FZl87ORiO+rW4LCDCNd2lUvLE/GL2GWyuKN0K5iCd5TbtJzEkQTu
DSt2mcNn4rhAL+JFr56o4T6z8WWAW18BR6yGrMq7Q/kALHYW3OekePQAzL0VUYbW
JGTi65CxbCnzc/w4+mqQyvmzpWtMAzJTzAzQxNbkR2MBGySxDLrjg0LWN6sK7wNX
x0YVztz/zbIkPjfkU1jHS+9EbVNj+D1XFOJuaQIDAQABAoIBABagpxpM1aoLWfvD
KHcj10nqcoBc4oE11aFYQwik7xfW+24pRNuDE6SFthOar69jp5RlLwD1NhPx3iBl
J9nOM8OJ0VToum43UOS8YxF8WwhXriYGnc1sskbwpXOUDc9uX4+UESzH22P29ovd
d8WErY0gPxun8pbJLmxkAtWNhpMvfe0050vk9TL5wqbu9AlbssgTcCXkMQnPw9nC
YNN6DDP2lbcBrvgT9YCNL6C+ZKufD52yOQ9qOkwFTEQpjtF4uNtJom+asvlpmS8A
vLY9r60wYSvmZhNqBUrj7lyCtXMIu1kkd4w7F77k+DjHoAXyxcUp1DGL51sOmama
+TOWWgECgYEA8JtPxP0GRJ+IQkX262jM3dEIkza8ky5moIwUqYdsx0NxHgRRhORT
8c8hAuRBb2G82so8vUHk/fur85OEfc9TncnCY2crpoqsghifKLxrLgtT+qDpfZnx
SatLdt8GfQ85yA7hnWWJ2MxF3NaeSDm75Lsm+tBbAiyc9P2jGRNtMSkCgYEAypHd
HCctNi/FwjulhttFx/rHYKhLidZDFYeiE/v45bN4yFm8x7R/b0iE7KaszX+Exdvt
SghaTdcG0Knyw1bpJVyusavPzpaJMjdJ6tcFhVAbAjm7enCIvGCSx+X3l5SiWg0A
R57hJglezIiVjv3aGwHwvlZvtszK6zV6oXFAu0ECgYAbjo46T4hyP5tJi93V5HDi
Ttiek7xRVxUl+iU7rWkGAXFpMLFteQEsRr7PJ/lemmEY5eTDAFMLy9FL2m9oQWCg
R8VdwSk8r9FGLS+9aKcV5PI/WEKlwgXinB3OhYimtiG2Cg5JCqIZFHxD6MjEGOiu
L8ktHMPvodBwNsSBULpG0QKBgBAplTfC1HOnWiMGOU3KPwYWt0O6CdTkmJOmL8Ni
blh9elyZ9FsGxsgtRBXRsqXuz7wtsQAgLHxbdLq/ZJQ7YfzOKU4ZxEnabvXnvWkU
YOdjHdSOoKvDQNWu6ucyLRAWFuISeXw9a/9p7ftpxm0TSgyvmfLF2MIAEwyzRqaM
77pBAoGAMmjmIJdjp+Ez8duyn3ieo36yrttF5NSsJLAbxFpdlc1gvtGCWW+9Cq0b
dxviW8+TFVEBl1O4f7HVm6EpTscdDxU+bCXWkfjuRb7Dy9GOtt9JPsX8MBTakzh3
vBgsyi/sN3RqRBcGU40fOoZyfAMT8s1m/uYv52O6IgeuZ/ujbjY=
-----END RSA PRIVATE KEY-----
```

### Level 17 -> 18
#### Game Instructions
> There are 2 files in the homedirectory: passwords.old and passwords.new. The password for the next level is in passwords.new and is the only line that has been changed between passwords.old and passwords.new

> NOTE: if you have solved this level and see ‘Byebye!’ when trying to log into bandit18, this is related to the next level, bandit19

First we create a key from the information from the last level in `/tmp/bandit17/`

now we just `nano` `bandit17.key` and paste in the information.

This part was frustrating for me and took me a while. You need to set permissions on the file or it won't take.

`chmod 600 bandit17.key`

Then we can just used the command we used in a previous level to use that key without a password:

`ssh -i bandit17.key bandit17@localhost` Bam... we're in.

Now we need to `diff` these files `passwords.new` and `passwords.old` to see what the difference is.

There's only 2 options and this is the one:
kfBf3eYk5BPBRzwjqutbbfE887SVc5Yd


### Level 18 -> 19
#### Game instructions
> The password for the next level is stored in a file readme in the homedirectory. Unfortunately, someone has modified .bashrc to log you out when you log in with SSH.

When we put in the password, as mentioned above, we are successfully logged in -- only to be logged out immediately. However, they've let us know that there is a `readme` file in the home directory. So what if we can attach a `cat` command to scoop the password before we are logged out?

`ssh -p 2220 bandit18@bandit.labs.overthewire.org "cat ~/readme"`

This will let us get that password before we get kicked out. Password for `bandit19`

`IueksS7Ubh8G3DCwVzrTd8rAVOwq3M5x`

### Level 19 -> 20
#### Game Instructions
> To gain access to the next level, you should use the setuid binary in the homedirectory. Execute it without arguments to find out how to use it. The password for this level can be found in the usual place (/etc/bandit_pass), after you have used the setuid binary.

Using the `bandit20-do` **setuid** binary essentially just lets us run a command as that user. It's binary so trying to `cat` the file won't let you see the underlying code. So just trust the exercise it's letting us work **as bandit20** to **do** a thing.

So let's run the binary and simply run a command after to read the password file in `/etc/bandit_pass`

`./bandit20-do cat /etc/bandit_pass/bandit20`

Now it'll spit out the next password for us.

`GbKksEFF4yrVs6il55v6gwY5aVje5f0j`

### Level 20 -> 21
#### Game Instructions
> There is a setuid binary in the homedirectory that does the following: it makes a connection to localhost on the port you specify as a commandline argument. It then reads a line of text from the connection and compares it to the password in the previous level (bandit20). If the password is correct, it will transmit the password for the next level (bandit21).

First we send the string of the last password to a TCP server running on a port of our choice (in this exampe **61137**).
`echo "GbKksEFF4yrVs6il55v6gwY5aVje5f0j" | nc -l localhost -p 61137 &`

Then we check to make sure it's working

`ps aux`

```USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
bandit20   658  0.0  0.1  21148  5144 pts/54   Ss   17:22   0:00 -bash
bandit20  1103  0.0  0.1  21148  4860 pts/35   Ss+  16:36   0:00 -bash
bandit20  1157  0.0  0.0   6300  1584 pts/39   S+   16:36   0:00 nc -l localhost
bandit20  1523  0.0  0.0   6300  1660 pts/54   S    17:24   0:00 nc -l localhost
bandit20  1696  0.0  0.0  19188  2372 pts/54   R+   17:24   0:00 ps aux
bandit20 31119  0.0  0.1  21148  4968 pts/39   Ss   16:32   0:00 -bash
```

We can see that it is running on process ID **1523**

No we can run the binary to ask the server to send us the next one:

`./suconnect 61137`

Next password:
`gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr`

### Level 21 -> 22
#### Game Instructions
> A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

Get into the remote machine:
```
ssh -p 2220 bandit21@bandit.labs.overthewire.org
password: gE269g2h3mw3pwgrj0Ha9Uoqen1c9DGr
```

Looking into the direcory of /etc/cron.d we see a few differenct cronjobs. Let's `cat` the `cronjob_bandit22` file and see what's up
```
@reboot bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
* * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
```

Now we know where the `sh` file is we can cat that as well for more information:

`cat /usr/bin/cronjob_bandit22.sh`

This give us the source code of the `sh` file:
```
#!/bin/bash
chmod 644 /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
cat /etc/bandit_pass/bandit22 > /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv
```

Once more, let's just `cat` the file in `/tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`

`cat /tmp/t7O6lds9S0RqQh9aMcz6ShpAoZKF7fgv`

Now we have our next password! Woop!

`Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI`

### Level 22 -> 23
#### Game Instructions
> A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

> NOTE: Looking at shell scripts written by other people is a very useful skill. The script for this level is intentionally made easy to read. If you are having problems understanding what it does, try executing it to see the debug information it prints.

Let's start by getting into the new games
```
ssh -p 2220 bandit22@bandit.labs.overthewire.org
password: Yk7owGAcWjwMVRwrTesJEwB7WVOiILLI
```

Now we have another cronjob to look into.

Start by `cd`ing into the `/etc/cron.d` directory for the next level **bandit23**

`cd /etc/cron.d`

Then `cat` to get some more info.

`cat cronjob_bandit23`
And we get:
```
@reboot bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
* * * * * bandit23 /usr/bin/cronjob_bandit23.sh  &> /dev/null
```
Now let's see what's in that file:
`cat /usr/bin/cronjob_bandit23.sh`
And we get:
```bash
#!/bin/bash
myname=$(whoami)
mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)

echo "Copying passwordfile /etc/bandit_pass/$myname to /tmp/$mytarget"

cat /etc/bandit_pass/$myname > /tmp/$mytarget
```
So we see a pretty simple bash script. Now what are these variables? The script tells us:
`myname=$whoami` - we can simply run `whoami` to get the value of `bandit22`
`mytarget=$(echo I am user $myname | md5sum | cut -d ' ' -f 1)` - Let's just run this string with the peice we know of - `$myname` (but use **bandit23** which is the next level)
`echo I am user bandit23 | md5sum | cut -d ' ' -f 1`
And we get:
`8ca319486bfbbc3663ea0fbe81326349`
Now we know what file will be in the `tmp` directory with the password dump:
`/tmp/8ca319486bfbbc3663ea0fbe81326349` let's `cat` that file:
`cat /tmp/8ca319486bfbbc3663ea0fbe81326349` and bam... password
`jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n`

### Level 23 -> 24
#### Game Instructions
> A program is running automatically at regular intervals from cron, the time-based job scheduler. Look in /etc/cron.d/ for the configuration and see what command is being executed.

>NOTE: This level requires you to create your own first shell-script. This is a very big step and you should be proud of yourself when you beat this level!

>NOTE 2: Keep in mind that your shell script is removed once executed, so you may want to keep a copy around…

This one looks a bit similar to the previous 2 levels... Let's dig in!

```
ssh -p 2220 bandit23@bandit.labs.overthewire.org
password: jc1udXuA1tiHqjIsL8yaapX5XIAI6i0n
```

New password: `UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ`

=============== COMING BACK TO 23 -> 24 ==================

### Level 24 -> 25
#### Game Instructions
> A daemon is listening on port 30002 and will give you the password for bandit25 if given the password for bandit24 and a secret numeric 4-digit pincode. There is no way to retrieve the pincode except by going through all of the 10000 combinations, called brute-forcing.

This one is our first scripting for brute force...
```
ssh -p 2220 bandit24@bandit.labs.overthewire.org
password: UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ
```
We have a daemon listening on port 30002 for us to send both the previous password + a 4 digit pin. We can do this manually and take a week or so, or we can script it out to try the 10000 combinations. **Our First Brute Attack**

Here's a script:
```py
#!/usr/bin/env python3
# coding: utf-8
import sys
import socket
pincode = 0
password = "UoMYTrfrBFHyQXmg6gzctqAwOmw1IohZ"
try:
    # Connect to server
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.connect(("127.0.0.1", 30002))

    # Print welcome message
    welcome_msg = s.recv(2048)
    print(welcome_msg)
    # Try brute-forcing
    while pincode < 10000:
        pincode_string = str(pincode).zfill(4)
        message=password+" "+pincode_string+"\n"
        # Send message
        s.sendall(message.encode())
        receive_msg = s.recv(1024)
        # Check result
        if "Wrong" in receive_msg:
            print("Wrong PINCODE: %s" % pincode_string)
        else:
            print(receive_msg)
            break
        pincode += 1
finally:
    sys.exit(1)
```
After a while we'll get to the right combination. The pin is **2586** as of my writing.

Next password:
`uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG`

### Level 25 -> 26
#### Game Instructions
> Logging in to bandit26 from bandit25 should be fairly easy… The shell for user bandit26 is not /bin/bash, but something else. Find out what it is, how it works and how to break out of it.

Let's get started:
```
ssh -p 2220 bandit25@bandit.labs.overthewire.org
password: uNG9O58gUE7snukf3bvZ0rxhtnjzSGzG
```

So here we need to figure out what type of shell **bandit26** is using.

First, we'll check the `passwd` file for `bandit26`
`cat /etc/passwd | grep bandit26`
We get
`bandit26:x:11026:11026:bandit level 26:/home/bandit26:/usr/bin/showtext`
So no let's `grep` the file we're shown
`cat /usr/bin/showtext`
This gives us
```sh
#!/bin/sh
export TERM=linux
more ~/text.txt
exit 0
```
So now we know he's using `#1/bin/sh`

Then we need to figure out how it works and how to break out of it.

This works by using the `sshkey.private` that is provided in the `home` directory. However, you'll notice that the shell immediately closes out. So let's take a look at the above pulled shell config... Notice the `more ~/text.txt`. It's using `more` to view the file so we'll use that to break in.

No `more` will show one page of data at a time. So what happens if the window is just a **bit too small**? It won't close. This will allow us to use `vim` to break out an gain a shell.

Make the terminal window super tiny (less than 6 lines) and try to get back in using `ssh -i sshkey.private bandit26@localhost`. You'll notice it hangs (Yay!).

Now hit `v` to bring up command options in `vim`. Type:
`:e /etc/bandit_pass/bandit26`

Now we have it!

`5czgV9L3Xx8JPOyRbXh6lQbmIOWvPT6Z`

**Don't close the terminal we need the same shell to finish the next level!!**

### Level 26 -> 27
#### Game Instructions
>Good job getting a shell! Now hurry and grab the password for bandit27!

Ok now this is easy if we keep the same terminal open from the last time. All we are going to do is use the power of `vim` to execute a couple of simple shell commands.

Go back to the command area of `vim` and type in
`:set shell=/bin/bash` Note: you won't see confirmation
Now type `:shell` and you should be good to go!

Now navigate to `~` and use the `bandit27-do` file to `cat` as `bandit27`

`./bandit27-do cat /etc/bandit_pass/bandit27`

Boom. Done.

`3ba3118a22e93127a4ed485be72ef5ea`

### Level 27-28
#### Game Instructions
> There is a git repository at ssh://bandit27-git@localhost/home/bandit27-git/repo. The password for the user bandit27-git is the same as for the user bandit27.

>Clone the repository and find the password for the next level.

Start it up:
```
ssh -p 2220 bandit27@bandit.labs.overthewire.org
password: 3ba3118a22e93127a4ed485be72ef5ea
```
Clone the **repo**
`git clone ssh://bandit27-git@localhost/home/bandit27-git/repo`
**Note** the password is the same for the `git` cloning as for the `ssh` login.
Ok now we have our repo so we `cd repo` to get into the directory and there's only one file `REAMDE`
Super easy just `cat` the file and there's the password:
`0ef186ac70e04ea33b4c1853d2526fa2`

### Level 28 -> 29
#### Game Instructions
>There is a git repository at ssh://bandit28-git@localhost/home/bandit28-git/repo. The password for the user bandit28-git is the same as for the user bandit28.

I'm going to stay in the same shell as the last exercise for this one and just clone the repo.

If you closed out, however, just login with bandit28
```
ssh -p 2220 bandit28@bandit.labs.overthewire.org
password: 0ef186ac70e04ea33b4c1853d2526fa2
```
`git clone ssh://bandit28-git@localhost/home/bandit28-git/repo repo2` * You may notice I've add a **repo2** to specify folder. I don't want to get confused between the last repo and this one.
Password is `0ef186ac70e04ea33b4c1853d2526fa2`
`cd` into `repo2` and let's have a look.

Another `README.md` but with no information inside. Knowing that this is `git` and well, the whole point is version control and managing various commits, etc. Let's check the changes to the repo.

`git log`
```sh
bandit27@bandit:/tmp/repo12/repo2$ git log
commit edd935d60906b33f0619605abd1689808ccdd5ee
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

   fix info leak

commit c086d11a00c0648d095d04c089786efef5e01264
Author: Morla Porla <morla@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

   add missing data

commit de2ebe2d5fd1598cd547f4d56247e053be3fdc38
Author: Ben Dover <noone@overthewire.org>
Date:   Thu May 7 20:14:49 2020 +0200

   initial commit of README.md
```
Looks like they patched an "info leak", so let's check that commit history:

`git log -p`
```sh
- username: bandit29
-- password: bbc96594b4e001778eee9975372716b2
+- password: xxxxxxxxxx
```
There we go we have the next password:
`bbc96594b4e001778eee9975372716b2`

### Level 29 -> 30
#### Game Instructions
> There is a git repository at ssh://bandit29-git@localhost/home/bandit29-git/repo. The password for the user bandit29-git is the same as for the user bandit29.

Login as `bandit29`
```
ssh -p 2220 bandit29@bandit.labs.overthewire.org
password: bbc96594b4e001778eee9975372716b2
```
Clone the repo to whatever temp directory you choose.
