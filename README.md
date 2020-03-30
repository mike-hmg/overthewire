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

That's it! You're on your way to being a hacker!

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
