---
title: nala
section: 8
header: User Manual
footer: nala 1.0.0
date: January 13, 2021
---
# NAME
nala - a wrapper for the apt package manager

# SYNOPSIS
**nala** <*command*> [*\--options*]...

# DESCRIPTION
**nala** is a wrapper for the apt package manager. The goals of wrapping apt are
to add quality of life changes, and improve the ouput to make it more reader friendly.

**install**
: **install** works similar too the way it does in **apt**. **nala** takes multiple packages as arguments and will install all of them just like **apt**. One key difference is that **nala** updates the package cache for you. There isn't an equivalent command for **apt update**

: **nala** also uses **aria2c** for downloading packages. This functionality is much like **apt-fast** or **apt-metalink** (which **nala** is heavily based on). Along with this **nala** can download packages from multiple mirrors concurrently to speed up package downloads.

**remove**
: **remove** works similar to the way it does in **apt**. Our noticable differences here include improved output on what will be removed, no need for running an autoremove, **nala** will handle that for you. 

**update**, **upgrade**
: **update** is really an alias for **upgrade**. **nala** will always handle updating the package cache so we have aliased **update** with **upgrade**. By default **nala** will run the equivalent of **apt full-upgrade**.

**fetch**

: **fetch** is our first command that doesn't have an **apt** counterpart. **nala** will parse either the **Debian** mirror list from *https://www.debian.org/mirror/list-full*, or the **Ubuntu** mirror list from *https://launchpad.net/ubuntu/+archivemirrors* and then fetch (3 by default) mirrors that we have determined are the closest to you. **nala** will attempt to detect your distro and release by default. Don't worry if it's not able too, as you can specify it manually with some switches we'll go over in a later section.

	This functionality is much like you would expect from **netselect** and **netselect-apt**. We don't do traceroutes as we noticed hops didn't really matter all that much, and latency is king either way. We do want to extend functionality in the future to do bandwidth testing.

**show**
: **show** works exactly like the **apt** version except our output is a little easier to read. **show** will accept multiple packages as arguments

**history**
: **history** is our other new command. Every **install**, **remove**, or **upgrade** command is stored with an id. You can use **history** to view these in a summary style view, and even go more in depth with **history info [id]**. If you're familiar with how *Fedora's* **dnf history** command works, then you'll feel right at home. That's what we drew inspiration from.

	The sub commands for **history** include **info**, **undo**, **redo** and **clear**. All of these accept a transaction id, with **clear** additionally accepting 'all' to wipe the nala history

# OPTIONS
**\--help**
: *\--help* will print out a help message for each subcommand. **nala install** *\--help* is a different message than **nala update** *\--help*

**-y, \--assume-yes**
: *\--assume-yes* will automatically select yes for any prompts which may need your input. This can potentially be dangerous

**-d, \--download-only**
: *\--download-only* will do just that, download packages only. It will not unpack or configure anything.

**\--no-update**
: *\--no-update* skips updating the package cache if for whatever reason you would like to skip that.

**\--no-full**
: *\--no-full* is specific to the **update/upgrade** command. Using this switch will run an **apt** regular upgrade which won't remove packages. By default **nala** uses a *full-upgrade*

**\--debug**
: *\--debug* prints helpful information for solving issues. If you're submitting a bug report try running the command again with *\--debug* and providing the output to the devs, it will be helpful.

**\--fetches**
: *\--fetches* is a **nala fetch** specific switch. Using this you can determin the amount of mirrors to fetch between 1-10. 3 is the default

**\--debian**
: *\--debian* is a **nala fetch** specific switch. You can use this to specify that you're using **Debian** and what release you're using. *\--debian sid*

**\--ubuntu**
: *\--ubuntu* is a **nala fetch** specific switch. This is just the **Ubuntu** version of the switch above *\--ubuntu jammy*

**\--country**
: *\--country* is a **nala fetch** specific switch. This is for you to specify your *country* when fetching mirrors. You don't have to use this as we test latency anyway, but it seems like with *Ubuntu* you might want to specify your country.

**\--foss**
: *\--foss* is a **nala fetch** specific switch. Using this switch on *Debian* will ensure that you don't get the *contrib* or *non-free* repos. Using this on *Ubuntu* does nothing

**\--version**
: *\--version* prints the version of nala you have installed and exits

**\--license**
: *\--license* prints out a full copy of the GPLv3 which **nala** is licensed under

# EXAMPLES
**nala install --no-update wine**
: downloads and installs wine without updating the package cache.

**nala upgrade**
: updates the package cache then upgrades the system.

# AUTHORS
Blake Lee <*https://salsa.debian.org/volitank*>
volian-team <*https://salsa.debian.org/volian-team*>

# BUGS
Submit bug reports online at: <*https://salsa.debian.org/volian-team/nala/-/issues*>

# SEE ALSO
Sources at: <https://salsa.debian.org/volian-team/nala>