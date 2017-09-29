---
title: Installing Sublime Text on Ubuntu
template: templates/post.pug
date: 2015-08-17
author: Lenin Hasda
keywords: sublime, sublime 2, sublime 3, install, ubuntu
---

Here are few guide lines I found to install sublime text in linux ubuntu (also other distro)

#### Install via the package manager(apt-get):

**For sublime-text-2:**    
```bash
sudo add-apt-repository ppa:webupd8team/sublime-text-2
sudo apt-get update
sudo apt-get install sublime-text
```

**For Sublime-Text-3:**
```bash
sudo add-apt-repository ppa:webupd8team/sublime-text-3
sudo apt-get update
sudo apt-get install sublime-text-installer
```

#### Install manually:

alternatively you can download the installable file and install it manually using the following procedure

##### for ubuntu distro
you can download the .deb file and install it by double clicking or via package manager

**32-bit**    
```bash
cd ~
wget http://c758482.r82.cf2.rackcdn.com/sublime-text_build-3047_i386.deb
```

**64-bit**    
```bash
cd ~
wget http://c758482.r82.cf2.rackcdn.com/sublime-text_build-3047_amd64.deb
```

##### For other linux distro

You can download the .tar.bz2 archive file and install it manually

**32-bit**    
```bash
wget http://c758482.r82.cf2.rackcdn.com/Sublime\\ Text\\ 2.0.2.tar.bz2 \ntar vxjf Sublime\\ Text\\ 2.0.2.tar.bz2
```

**64-bit**    
```bash
wget http://c758482.r82.cf2.rackcdn.com/Sublime\\ Text\\ 2.0.2\\ x64.tar.bz2 \ntar vxjf Sublime\\ Text\\ 2.0.2\\ x64.tar.bz2
```

**Installation for both**    
```bash
sudo mv Sublime\\ Text\\ 2 /opt/ sudo ln -s /opt/Sublime\\ Text\\ 2/sublime_text /usr/bin/sublime
```


------


**Ref:**

*http://www.tecmint.com/install-sublime-text-editor-in-linux/
