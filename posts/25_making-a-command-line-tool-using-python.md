---
title: Making a command line tool using Python
template: templates/post.pug
date: 2018-05-05
author: Lenin Hasda
keywords: python, command line, cli, argparse, count files, os.walk, nix, linux, shell script
excerpt:

---



Previously I wrote about [how to count files in any given directory](http://blog.leninhasda.me/post/recursively-counting-files-in-directories-using-python) using simple python script. It was somewhat okey `script` and after getting few feedback on [reddit](https://www.reddit.com) I knew that I have to make upgrades!

I was going through few references from feedback and that is when I found this awesome module called `argparse`. It's a parser for command line options, arguments and sub-commands which makes it easy to write user-friendly command line tool(s). So this is going to be a quick intro to `argparse` module and at the end of this article I will link to the final upgraded code for counting files.

Enough chitchat, lets create a file called `calc.py` and start writing some code.

```python
#!/usr/bin/env python

import argparse

# instantiate parser object
parser = argparse.ArgumentParser(description='A simple command line calculator')

# add command line options here

# then parse the cli options
args = parser.parse_args()

# finally process `args`
```

Above code block is self-explanatory, we first created a `parser` object from `ArgumentParser` class and while at it, we provided a description as well. We will be adding some options to our script where commented, but before we can use them we need to parse it first. Which we did next. Finally we can use the `args` variable to access our option values. But wait, even though we haven't added any options to our script yet, we get a default flag option `-h` or `--help`. This flag prints help screen with description and all the available command parameter options. So if we run this:

```bash
python calc.py -h
```

We will get output like this:
![output help flag](/img/25-help-flag.png)

> The first line `#!/usr/bin/env python` means that if our script has executable permission, we can omit `python` in above command and directly use filename to run the script. How cool is that! let's do it.
> To add executable permission just enter this command in terminal.
> ```
> chmod +x calc.py
> ```
> Now we can directly use filename like this and get the same result.
> ```
> ./calc.py -h
> ```

Now let's add some arguments (aka options) to out calculator script. There are two kind of arguments that the parser can parse.
* **Positional Argument** - this is required parameter that must be passed when running the script, otherwise it will raise error. And the order in code should match the order we give the parameter value.
* **Optional Argument** - this one is optional and the order really doesn't matter

We will have two operations in our calculator - `add` and `sub` and we will take this input as first parameter to our script. And we will take two more parameter value to operate on, lets just call them - `a` and `b`. All of these will be positional arguments. So after `# add command line options here` line we add following code:

```python
# add command line options here
parser.add_argument('command', help='operation name: add or sub')
parser.add_argument('a', help='first value')
parser.add_argument('b', help='second value')
```

Now if we run the script with `-h` flag again we should see something like this:
![output help flag 2](/img/25-help-flag-2.png)

Awesome now we can take command and parameter values like this:

```bash
./calc.py add 10 27
```
And if we miss any of these three parameter script will raise error as they are positional arguments.

Our calculator script is almost ready we just need to add some logic there. Lets do that:

```python
# finally process `args`
if args.command == 'add':
	print(args.a + args.b)
elif args.command == 'sub':
	print(args.a - args.b)
else:
	print('wrong command. should be either "add" or "sub"')
```

All done! Let's run our script:

```bash
./calc.py sub 29 11
```
![sub command](/img/25-sub-command.png)
Wait, what the heck just happened!!!
Well the answer is simple! When we added `a` and `b` argument we didn't specified any expected `type` for them. So by default parser will parse them as `string`. As a result even though we entered numbers as input, they were parsed as string. And substraction between two string is unsupported in python, hence this error. Let's add `type` to our parameters to fix this issue. Update the following lines in code

```python
parser.add_argument('a', help='first value', type=int)
parser.add_argument('b', help='second value', type=int)
```
 Now if we run the command again, we get the result!
 ```bash
 ./calc.py sub 29 11
 18
 ```
Sweet!
![sub command](/img/25-commands.png)

Here's the final code:

```python
#!/usr/bin/env python

import argparse

# instantiate parser object
parser = argparse.ArgumentParser()

# add command line options here
parser.add_argument('command', help='operation name: add or sub')
parser.add_argument('a', help='first value', type=int)
parser.add_argument('b', help='second value', type=int)

# then parse the cli options
args = parser.parse_args()

# finally process `args`
if args.command == 'add':
	print(args.a + args.b)
elif args.command == 'sub':
	print(args.a - args.b)
else:
	print('wrong command. should be either "add" or "sub"')

```


### Thoughts and todos
The goal of this article was to show you how easy it is to make command line tools using `argparse` module in python. There are more advanced features than what we saw here, like default values, grouping commands and sub commands and more. I will leave that to you guys to discover for yourself and here is the [full documentation of the module (https://docs.python.org/3/library/argparse.html)](https://docs.python.org/3/library/argparse.html) to get started!

However if you want you can start playing with above script too! Try to add more commands to our calculator like `multiply` and `divide` etc! Let me know whether you were successful or got stuck on any point, would love to hear from you. :)

### `count-files` Upgraded version
As promised here is the upgraded version of `count-files` script. First upgrade is that I used `argparse` module to add options in the script. And second upgrade is that I removed the recursive function for traversing directory, instead I used `[os.walk]`(https://docs.python.org/3/library/os.html#os.walk) module which is pretty cool too!

![count files usage](/img/25-count-files.png)

<script src="https://gist.github.com/leninhasda/9b83f1ea28de73812156e54e1d9090c7.js"></script>

---

#### Related
- [Recursively counting files in directories using Python Script](http://blog.leninhasda.me/post/recursively-counting-files-in-directories-using-python)
