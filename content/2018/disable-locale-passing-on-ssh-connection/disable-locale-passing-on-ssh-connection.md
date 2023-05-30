---
title: Disable locale passing on ssh connection
date: 2018-03-08
redirect_from: /disable-locale-passing-on-ssh-connection/
---
You might have seen these super annoying error messages on a new Linux system:

```
perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
	LANGUAGE = (unset),
	LC_ALL = (unset),
	LC_TIME = "fi_FI.UTF-8",
	LC_MONETARY = "fi_FI.UTF-8",
	LC_ADDRESS = "fi_FI.UTF-8",
	LC_TELEPHONE = "fi_FI.UTF-8",
	LC_NAME = "fi_FI.UTF-8",
	LC_MEASUREMENT = "fi_FI.UTF-8",
	LC_IDENTIFICATION = "fi_FI.UTF-8",
	LC_NUMERIC = "fi_FI.UTF-8",
	LC_PAPER = "fi_FI.UTF-8",
	LANG = "C"
    are supported and installed on your system.
perl: warning: Falling back to the standard locale ("C").
perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
	LANGUAGE = (unset),
	LC_ALL = (unset),
	LC_TIME = "fi_FI.UTF-8",
	LC_MONETARY = "fi_FI.UTF-8",
	LC_ADDRESS = "fi_FI.UTF-8",
	LC_TELEPHONE = "fi_FI.UTF-8",
	LC_NAME = "fi_FI.UTF-8",
	LC_MEASUREMENT = "fi_FI.UTF-8",
	LC_IDENTIFICATION = "fi_FI.UTF-8",
	LC_NUMERIC = "fi_FI.UTF-8",
	LC_PAPER = "fi_FI.UTF-8",
	LANG = "C"
    are supported and installed on your system.
perl: warning: Falling back to the standard locale ("C").
```

You cans see the current locale by typing _locale_.

You should see something like this en\_US.UTF-8 because that’s the most used locale and usually the preferred way to use Linux servers.

```
LANG=en_US.UTF-8
LANGUAGE=
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=
```

But if you don’t then this is most often because you have logged in with ssh and your ssh client is passing the locale of your own system into the server. There are two ways to prevent this.

Easiest is to disabled the passing from your own system (the one where you are connecting from):

```
sudoedit /etc/ssh/ssh_config
 
comment this line SendEnv LANG LC_*
 
like this
 
# SendEnv LANG LC_*
```

The other way is to prevent the passing of the locale on your ssh server (the one you are connecting to):

```
sudoedit /etc/ssh/sshd_config (notice the sshD)
 
comment out this line #AcceptEnv LANG LC_* like this
 
#AcceptEnv LANG LC_*
```

Now just relog to your server and type _locale_ again.