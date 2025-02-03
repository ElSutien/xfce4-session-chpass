# xfce4-session-chpass
xfce4 session handler that requires user to change password on first X login.

This is intended for RDP clients on a multiuser terminal VM.

## Function
This script will launch a graphical wizard at the start of the session for forcing the user to change the password. They can not continue until new password had been set.

This will only be affect on their first login. Once changed, logins will be normal.

## Requirements
This application requires following packages:
- **xfce4**
- **zenity** (Default on Debian)

Zenity comes installed by default on Debian like distros. Although this application is designed to use xfce4 as the Desktop Environment, it can be easily modified to adapt for other DE.

## Installation
To install it, you have to copy "xfce4-session-chpass" and "change-pass" files to /usr/bin directory. Note that "xfce4-session-chpass" should be marked as executable.

```
install -m755 xfce4-session-chpass /usr/bin/
install -m644 change-pass /usr/bin/
install -m644 skel/.xsession /etc/skel/
```

## Usage
For every user created, you should use a home directory skeleton that contains the ".xsession" defined like in this repo.

```$ useradd -m -k /etc/skel -s /bin/bash -U USERNAME```

Description of the command:
- **-m**  -- Creates the home directory.
- **-k /etc/skel** -- Uses given directory as the skeleton for user homedir.
- **-s /bin/bash** -- Set Bash as the default interpreter.
- **-U** -- Creates a own group for the user.

### Force an already existent user
Sometimes it you want to force an user to establish a new password o next login. For this, you must only overwrite the ".xsession" file.

```$ echo "xfce4-session-chpass" >/home/USERNAME/.xsession```