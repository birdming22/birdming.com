
## Sublime Text 2

## Install From Ubuntu PPA
ref. [Sublime Text 2 Ubuntu PPA](http://www.webupd8.org/2011/03/sublime-text-2-ubuntu-ppa.html)

    sudo add-apt-repository ppa:webupd8team/sublime-text-2
    sudo apt-get update
    sudo apt-get install sublime-text

## Installation Script
https://github.com/TCattd/sublime-text-bash-installer

    sudo bash st2install

## Font
ref. [在 Sublime Text 2/3 設定 Inconsolata 字型](http://akr.tw/2012/09/inconsolata-sublime-text-2/)

Perferences → Settings – User

	"font_face": "Inconsolata",
    "font_size": 12

### Source Code Pro
ref. [Using Source Code Pro with Sublime Text 2 and Terminal](http://blogs.adobe.com/cantrell/archives/2012/10/using-source-code-pro-with-sublime-text-2.html)

Download [SourceCodePro_FontsOnly-1.017.zip](http://sourceforge.net/projects/sourcecodepro.adobe/)

## Package Control
ref. [Package Control Installation](https://packagecontrol.io/installation#st2)

### Usage
Preferences -> Package Control

Add Channel: https://packagecontrol.io/browse

### Install Package
Preferences -> Package Control

Install Package: ctags

## Q&A

### Sublime Text 2.0.2 sidebar missing on ubuntu 10.04
ref. 

* [Weird sidebar and tabs](http://www.sublimetext.com/forum/viewtopic.php?f=3&t=12167&start=0&hilit=sidebar)
* [Reverting to a Freshly Installed State](http://www.sublimetext.com/docs/2/revert.html)

To revert to a frestly installed state, you can:

1. Exit Sublime Text 2
2. Delete (or move) the data folder (~/.config/sublime-text-2)
3. Start Sublime Text 2

### Samba Permission Problem
ref. [samba and permissions](https://www.sublimetext.com/forum/viewtopic.php?f=3&t=7969)

avoid file mode 0644 to 0755, add 'map archive = no' to smb.conf

    [slash]
    path = /
    writeable = yes
    map archive = no
    force user = nick
    force create mode = 644
    create mask = 644
    oplocks = no
