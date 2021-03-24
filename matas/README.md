# Natas OverTheWire Wargames

##

### Level 0
> Username: natas0
Password: natas0
URL:      http://natas0.natas.labs.overthewire.org

Let's go the URL provided and login:
All we need to do here is right click and "show page source"

There is a comment right before the last closing `</div>`

`<!--The password for natas1 is gtVrDuiDfck831PqWsLEZy5gyDz1clto -->`

### Level 0 -> 1
> Username: natas1
URL:      http://natas1.natas.labs.overthewire.org

Let's get going. Looks like right-clicking has been blocked. But that's easy to get around with a keyboard shortcut. Just press `control-shift-C` in Windows or `command-option-C in macOS`

Now we can inspect the source code and see what we saw the last exercise. A simple HTML comment.
`<!--The password for natas2 is ZluruAthQk7Q2MqmDeTiUij2ZvWy2mBi -->`

### Level 1 -> 2
> Username: natas2
URL:      http://natas2.natas.labs.overthewire.org

Login with the previously attained password and you'll see "There is nothing on this page". That's a pretty dead giveaway that it's in another file. Let's check:

Using the dev tools we can see check `sources`. We can see a few different things like the main page and some pictures... Where are these pictures? In the `/files` directory. Let's just go ahead and go to the URL bar and add `/files` to the end of the URL and now we can see a list of files. One of them is `users.txt`. I bet thats it:
```
# username:password
alice:BYNdCesZqW
bob:jw2ueICLvT
charlie:G5vCxkVV3m
natas3:sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14
eve:zo4mJWyNj2
mallory:9urtcpzBmH
```
Now we have the `natas3` password: sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14

### Level 2 -> 3
> Username: natas3
URL:      http://natas3.natas.labs.overthewire.org

Let's login with the previously attained credentials:
```
natas3
sJIJNW6ucpu6HPZ1ZAchaDtwd7oGrD14
```
They're getting a bit sneaky on this one. No open directories or hints in the source page. Just the message "Theres nothing on this page".

Looking at the source it says "Not even Google will find it". Which means they probably told Google not to find it. And how do we tell Google not to do things (if it even listens)? `robots.txt`. Let's check it out:
Put this in the browser:
`http://natas3.natas.labs.overthewire.org/robots.txt`
and we see a bit of code:
```
User-agent: *
Disallow: /s3cr3t/
```
This is telling all search engines **not** to look in the `/s3cr3t/` directory. So clearly we want to get up in there.
`http://natas3.natas.labs.overthewire.org/s3cr3t/`
And bam. Another `users.txt` file for us to look at with this information:
`natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ`


### Level 3 -> 4
>Username: natas4
URL:      http://natas4.natas.labs.overthewire.org

Login with the new credentials
```
natas4
Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ
```
