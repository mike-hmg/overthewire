# Wargames

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
```bash
username: bandit0
password: bandit0
```
All we have to do here is `ssh` into the WarGames.
We do this by using the `ssh` command with the `-p` flag on the port `2220` and the `bandit0` username:
```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```
Then just use the password `bandit0` when prompted.

That's ijhgkjhgkjhgkjhgt! You're on your way to being a hacker!

### Level 0 -> 1
#### Game Instructions
>The password for the next level is stored in a file called readme located in the home directory. Use this password to log into bandit1 using SSH. Whenever you find a password for a level, use SSH (on port 2220) to log into that level and continue the game.

Super simple setup here. Just `cat` the `readme` file:
```bash
cat readme

boJ9jbbUNNfktd78OOpsqOltutMc3MY1
```
Bam! Password revealed. Now let's use the password for the next level.

### Level 1 -> 2
#### Game Instructions
>The password for the next level is stored in a file called - located in the home directory

This level is also quite simple. The password for the next level is stored in a file named `-`. So all we have to do is `ssh` using the next level `bandit1` username and  use `cat` to read the file... right?
```bash
cat -
...
```
Nope!!! They pulled a sneaky on you. Notice that when you try this, the __command line will stall__.  

In bash, the `-` will tell the interpreter to look for a `flag`. So what we need to do here is tell the command line that `-` is a **file**. How do we do this? With `./`

State that __this current directory, look for file__:
```bash
cat ./-

CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```
Boom! now you have the password and you've hacked the mainframe. Now let's go to the next level.

### Level 2 -> 3
#### Game Instructions
>The password for the next level is stored in a file called spaces in this filename located in the home directory

First, let's login using the previous password and the next login of `bandit2`:
```bash
ssh -p 2220 bandit2@bandit.labs.overthewire.org

password: CV1DtqXWVFXTvM2F0k09SHz0YwRINYA9
```
So this one is fairly simple. You just need to understand how spaces `" "` work on the command line. If you just simply run `cat spaces in this filename`, you'll get This
```bash
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
```bash
UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```
### Level 3 -> 4
#### Game Instructions
>The password for the next level is stored in a hidden file in the inhere directory.

Let's get this one going the same way we have been. Using the next level up login `bandit3`
```bash
ssh -p 2220 bandit3@bandit.labs.overthewire.org

password: UmHadQclWmgdLOKQ3YNgjWxGoRMb5luK
```
Next you'll need to navigate into the `inhere` directory:
```bash
cd inhere
```
Once inside the directory, we'll need to list all files. Now a simple `ls` to list files will return blank here. So we'll need to add the `-a` flag to show **hidden** files.
```bash
ls -a
```
Alright! Now we have a file to work with named `.hidden`

Let's `cat` the `.hidden` file to see what's inside:

```bash
cat .hidden

pIwrPrtPN36QITSp3EQaw936yaFoFgAB
```

Nice! Now we have the password for the next level!!

### Level 4 -> 5
#### Game Instructions
>The password for the next level is stored in the only human-readable file in the inhere directory. Tip: if your terminal is messed up, try the “reset” command.

Let's go ahead and login with the next level `bandit4`
```bash
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
