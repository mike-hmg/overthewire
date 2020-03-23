# Wargames

Wargames is an awesome service setup by the awesome folks at [OverTheWire](http://www.overthewire.org).

It tests one's ability to exercise certain security concepts in the form of games.

The best part is that it's FREE and can be started from a complete beginner!!

## Modules
There are a few different "games" within the WarGames. Each is essentially getting more advanced on it's way:
- Bandit
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
