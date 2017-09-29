---
title: How password is stored in linux - Understanding hashing mechanism
template: templates/post.pug
date: 2017-08-26
author: Lenin Hasda
keywords: ubuntu, linux, password, password store, password hashing, how
---

Have you ever wondered how and where password is stored in your linux machine and how it is checked during the login process ?

Well I sure did, and when I searched about it I found pretty interesting reads. We all know that there is a file `/etc/passwd`. In this file each of the line represents one user account details, but not the password itself. So where is it saved?

There is a package called **shadow-utils** which comes with most of the linux distros. The purpose of this package is to separate the password from `/etc/passwd` file. We will discus the reason for using this package some other day. For now let's just focus on where and how it stores the password.

Shadow utils package stores the password of each account on `/etc/shadow` file. In this file each line represents password details of a single account. Each line contains 9 parts separated by `:` like this:

```
root:$6$rFk1NtvH$BYY.DZfRlNtQqm/EZXBKDJnBczcbi6oIPbjE5J.fPdvDG/qVOo.p66aquFZleqxJa9LN5J.y7GDOFsNOzRSvo1:15651:0:99999:7:::
```

Let's review each part:

1. This part is the *USERNAME*, for above case it's root.
2. This is the password for root user account in hashed format, we will discuss more in details below.
3. Third part is the number of days since the start of unix time (01/01/1997) that the password was last changed.
4. Fourth part is minimum number of days required before the password can be changed again.
5. This part is maximum number of days before the password must be changed. 99999 means that the user will not be forced to change their password.
6. This is the number of days before forcing the password change that the user will be warned.
7. If the password is expired, after this number of days account will be disabled
8. This is the number of days from the unix time that the account is disabled.
9. This part is kept for future use and not used yet.

Great, now we know what each 9 part mean of the line in `/etc/shadow` file. Now let's look at the password, the second part, and it itself is again divided in three parts. In above line the password part is:

```
$6$rFk1NtvH$BYY.DZfRlNtQqm/EZXBKDJnBczcbi6oIPbjE5J.fPdvDG/qVOo.p66aquFZleqxJa9LN5J.y7GDOFsNOzRSvo1
```

The password is generated with a one way hashing algorithm by combining the user given password and a random salt key (random string). There few different kind of hashing algorithm, and this algorithm is represented with the `$6` part in the above line. Here are all the other algorithms with their selector:

```
$1  = MD5 hashing algorithm.
$2  = Blowfish Algorithm is in use.
$2a = eksblowfish Algorithm
$5  = SHA-256 Algorithm
$6  = SHA-512 Algorithm
```

We see that our root password was hashed using `SHA-512` algorithm. The second part is the **salt key** which is the part between second and third `$`, in our case `rFk1NtvH` is the salt. So the algorithm actually uses `SALT + USER_PASSWORD` to generate the full hash.

Why salt is important?    
It is near impossible to revert back the hashed string to original password, however there is always a chance for hacker to use a dictionary or brute-force attack and get lucky, specially if the user uses a week password. But when salt is added, it adds that extra layer of security, that not only the hacker has to guess the password but also the random string salt.

There is another reason for using salt, that is, if some how two user end up using same password, their hashed password should be same right? Not at all, although their password is same but the salt is different and random. So the generated and saved hashed password will be different.

So, how the login check is done?    
During the login the system takes the username and password from user, determines the algorithm and salt from the `/etc/shadow` file using the username. Then it generates the hash for given password using the exiting salt and algorithm. Finally it checks the generated hash with the save one, if they are same login success, otherwise invalid! Pretty simple!

I hope you learn a little bit about how your linux machine stores your login password and where! Before saying goodbye let's do a fun experiment shall we :D    
Let's try and see if we can generate the above hash that we have been seeing. Every linux machine comes with python, so we will use that. Just open up a terminal, type `python` and hit enter to start the python interpreter, then do the following:

```
>>> import crypt
>>> crypt.crypt('secret', '$6$rFk1NtvH');
'$6$rFk1NtvH$BYY.DZfRlNtQqm/EZXBKDJnBczcbi6oIPbjE5J.fPdvDG/qVOo.p66aquFZleqxJa9LN5J.y7GDOFsNOzRSvo1'
```

Here `secret` is the actual password, `$6` is the algorithm, `rFk1NtvH` is salt. And the next line is the full hash for the password.    
How cool is that!


------


**Ref:**
* https://www.aychedee.com/2012/03/14/etc_shadow-password-hash-formats/
* http://www.slashroot.in/how-are-passwords-stored-linux-understanding-hashing-shadow-utils
