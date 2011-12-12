# xmonad-config
xmonad-config is the [xmonad](http://xmonad.org/) configuration used by Vic Fryzel.
This is a custom version for a 1280x800 laptop in combination with a 1920x1200 monitor.

## Introduction

If you are unfamiliar with xmonad, it is a tiling window manager that is
notoriously minimal, stable, beautiful, and featureful.  If you find yourself
spending a lot of time organizing or managing windows, you may consider trying
xmonad.

However, xmonad can be somewhat difficult to configure if you're new to
Haskell or even to xmonad itself.

This project contains a completely working and very usable xmonad
configuration "out of the box".  If you are just starting out with xmonad,
this will give you a configuration that I personally use for around 12 hours
every day.  Thought has been put into the colors, key bindings, layouts,
and supplementary scripts to make life easier.

This project is also recommended for advanced xmonad users, who may just not
want to reinvent the wheel.  All source provided with this project is well
documented and simple to customize.

![Screenshot of xmonad-config](/unchiujar/xmonad-config/raw/master/screenshot.png)

For source code, or to contribute, see the
[xmonad-config project page](http://github.com/unchiujar/xmonad-config).


## Requirements

* xmonad 0.9.1 or 0.9.2
* xmonad-contrib 0.9.1 or 0.9.2
* [xmobar 0.11.1 or 0.13](http://projects.haskell.org/xmobar/)
* [trayer 1.0](http://fbpanel.sourceforge.net/)
* [dmenu 4.0](http://tools.suckless.org/dmenu/)
* [yeganesh 2.2](http://dmwit.com/yeganesh/)
* [scrot 0.8](http://freshmeat.net/projects/scrot/)

### Installing requirements on [Arch Linux](http://www.archlinux.org/)

    sudo pacman -S xmonad xmobar trayer dmenu scrot cabal-install
    cabal update
    cabal --global install xmonad-contrib

### Installing requirements on [Ubuntu Linux](http://www.ubuntu.com/)

    sudo aptitude install xmonad libghc6-xmonad-contrib-dev xmobar trayer \
        suckless-tools scrot cabal-install
    cabal update
    cabal --global install xmonad-contrib
    

## Installation

Installing xmonad-config is a matter of backing up any xmonad configuration
you may already have, cloning the git repository, and updating your PATH.

    cd
    mv .xmonad .xmonad.orig
    git clone https://github.com/unchiujar/xmonad-config.git .xmonad
    echo "export PATH=\$PATH:~/.cabal/bin:~/.xmonad/bin" >> ~/.bashrc
    source ~/.bashrc

Once xmonad-config is installed, you also need to ensure you can actually
start xmonad.  The mechanism to do this varies based on each environment, but
here are some instructions for some common login managers.

### Starting xmonad from xdm, kdm, or gdm

    echo xmonad >> ~/.xsession
    # Note: this method will start no programs in your new session upon login.
    # To get a terminal in your next session, press Meta+Shift+Enter.
    # Logout, login from xdm/kdm/gdm

### Starting xmonad from slim

    ln -s ~/.xmonad/xinitrc ~/.xinitrc
    # Logout, login from slim

### Using the scripts

To use the i3status you need to install i3status and copy i3status.conf to
/etc/i3status.conf

   sudo apt-get install i3status

The xmobar configuration takes the i3status information from /tmp/i3.fifo. 
The FIFO is created by running xmonad_config after startup or by running the 
following commands

    rm /tmp/i3.fifo
    mkfifo /tmp/i3.fifo
    i3status >> /tmp/i3.fifo&

To display the disk I/O you need to run the diskio.sh script. The script
creates /tmp/diskio.fifo from which xmobar reads the information.


Currently there is a bug where xmobar doesn't display the i3status and disk 
info after starting the scripts. 
The workaround is to restart xmonad by using 

  Meta+Q
## Keyboard shortcuts

After starting xmonad, use the following keyboard shortcuts to function in
your new window manager.  I recommend you print these out so that you don't
get stranded once you logout and back in.

* Meta+Shift+Return: Start a terminal
* Meta+Ctrl+l: Lock screen
* Meta+p: Start dmenu.  Once it comes up, type the name of a program and enter
* Meta+Shift+p: Take screenshot in select mode. Click or click and drag to select
* Meta+Ctrl+Shift+p: Take fullscreen screenshot. Supports multiple monitors
* Meta+Shift+c: Close focused window
* Meta+Space: Change workspace layout
* Meta+Shift+Space: Change back to default workspace layout
* Meta+n: Resize viewed windows to the correct size
* Meta+Tab: Focus next window
* Meta+j: Focus next window
* Meta+k: Focus previous window
* Meta+m: Focus master window
* Meta+Return: Swap focused window with master window
* Meta+Shift+j: Swap focused window with next window
* Meta+Shift+k: Swap focused window with previous window
* Meta+h: Shrink master window area
* Meta+l: Expand master window area
* Meta+t: Push floating window back into tiling
* Meta+,: Increment number of windows in master window area
* Meta+.: Decrement number of windows in master window area
* Meta+q: Restart xmonad. This reloads xmonad configuration, does not logout
* Meta+Shift+q: Quit xmonad and logout
* Meta+[1-9]: Switch to workspace 1-9, depending on which number was pressed
* Meta+Shift+[1-9]: Send focused window to workspace 1-9
* Meta+w: Focus left-most monitor (Xinerama screen 1)
* Meta+e: Focus center-most monitor (Xinerama screen 2)
* Meta+r: Focus right-most monitor (Xinerama screen 3)
* Meta+Shift+w: Send focused window to workspace on left-most monitor
* Meta+Shift+e: Send focused window to workspace on center-most monitor
* Meta+Shift+r: Send focused window to workspace on right-most monitor
* Meta+Left Mouse Drag: Drag focused window out of tiling
* Meta+Right Mouse Drag: Resize focused window, bring out of tiling if needed


## Personalizing or modifying xmonad-config

Once cloned, xmonad-config is laid out as follows.

All xmonad configuration is in ~/.xmonad/xmonad.hs.  This includes
things like key bindings, colors, layouts, etc.  You may need to have some
basic understanding of [Haskell](http://www.haskell.org/haskellwiki/Haskell)
in order to modify this file, but most people have no problems.

Most of the xmobar configuration is in ~/.xmonad/xmobar.hs.

All scripts are in ~/.xmonad/bin/.  Scripts are provided to do things like
take screenshots, start the system tray, start dmenu, or fix your multi-head
layout after a fullscreen application may have turned off one of the screens. 

Colors set in the xmobar config and dmenu script are meant to coincide with the
[IR_Black terminal and vim themes](http://blog.infinitered.com/entries/show/6).
