---
title: Recursively counting files in directories using Python Script
template: templates/post.pug
date: 2018-04-21
author: Lenin Hasda
keywords: python, python script, scripting, count files, recursive, shell script, linux
excerpt:

---

There where few occasions when I wanted to know the total number of files in any given directory. Well the default file manager shipped with the OS does give you a count of files on current directory, but not recursively. That is if you have folder(s) on the current directory and files within them that count is not shown. But I wanted to know the whole number.

So I wrote following Python script which goes through given folder(s) and folder within them recursively, count files and give me the total number.

<script src="https://gist.github.com/leninhasda/0414792e7d65f526ce078f7af932b5af.js"></script>

#### Usage:
Copy the content and save in a file. (ex: count-files.py or just download it)
Now you should be able to run it like this:

```
python count-files.py . # current directory (default)
python count-files.py . dir_2 /home/lenin # count files in current directory, dir_2, and /home/lenin directory

# or do this
chmod +x count-files.py
sudo mv /usr/local/bin/count-files

# then from anywhere in terminal
count-files ~/Downloads # count files in Download directory
```

#### Alternatives?
After few searching I did find some linux command to do this same task. One of which was using `ls` command combined with `wc` command like this:

```
ls ~/Downloads | wc -l
```
Aka list the files in `Downloads` directory and only give me the count of lines (pipe `wc -l`). Great! Now do that recursively, which is what I actually want:

```
ls -R ~/Downloads | wc -l
```
Ahhh... wait, the answer is wired! It's not correct! Because `ls` command also prints/lists directory as well! And it has its own special format to print them. So when `wc` tries to count number of lines the result is way bigger number than actual result.

Alternative 2, the awesome `find` command. Something like this:
```
find ~/Downloads -type f | wc -l
```
That is find every file type in `Downloads` directory, recursively, then give me the total number. Sweet! Event better
```
find ~/Downloads ~/Documents -type f | wc -l
```
Yap! `find` can give you number of files in multiple folders as well. But all as a total number :p

#### Thoughts
I did noticed few things:
1. `find` command is way faster then my script
2. `find` is giving slightly less number than my script and when I checked the diff of their file listings, surprisingly `find` wasn't listing few files! Don't really know why?!
3. Am planning to add few more flags for listing the files instead of just showing the total number.

---

#### Related
- [Making a command line tool using Python](http://blog.leninhasda.me/post/making-a-command-line-tool-using-python)
