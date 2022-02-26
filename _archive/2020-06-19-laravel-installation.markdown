---
layout: post
title: "Laravel installation"
categories: [programming, web-development]
---

> Not another laravel installation guide; a journal instead

Had a clean install of Ubuntu 20.04, and had to get working environment back to the way they were in Ubuntu 18.04, part of which included Laravel development environment. Today I am much oblieged to continue learning Laravel as I was deeply saddened by the postponding of a 40hr online course that I was suppsoed to take from today.

Anyway!

First thing first:

- [This][https://laravel.com/docs/7.x/installation] is Laravel's official documentation on installing Laravel.

**Step 1**: Installing Composer
Composer is Laravel's dependency manager. So this better be installed first:<br>
`composer global require laravel/installer`

> PHP missing ?

**Step 1.1**: Installing LAMP Stack from Bitnami
Going [here][https://bitnami.com/stack/lamp/installer] to get the LAMP stack installer<br>
After downloading the installer did a `sudo chmod 777 <package-name>` to make the file executable. Reran the file.<br>
The installer prompted `libtinfo.so.5` package missing; installed it with `sudo apt-get install libncurses5` explained [here][https://docs.bitnami.com/installer/faq/linux-faq/troubleshooting/troubleshooting-components/]

`/opt`, the default installation directory the installer had didn't have write permission. Instead of changing write permission for `/opt` directory for current user, as this can fuck things up pretty badly, simply changed the default installation directory.

The installer asked for a password for LAMP stack database, set that to `root123`.


Set the Apache Web Server Port to `1024`, SSL port to `1024`, both the defaults.  > Since I'm writing this in Vim, u will undo, and ^+r will redo changes

The installer can't complete with ` Error runing chown -R root:daemon ` error!

Retrying with an older version. ( This didn't work either)<br>
Did a `sudo chown -R $USER <folder>` to change ownership of the installation folder, as described [here][https://askubuntu.com/questions/6723/change-folder-permissions-and-ownership]

This didn't work either!

Back to `composer global require laravel/installer`

`/usr/bin/env: 'php': No such file or directory`

Running `php` shows that php is not installed at all.

**Step 1.2** Installig php
Described [here][https://thishosting.rocks/install-php-on-ubuntu/]
`sudo apt-get update && apt-get upgrade`
`add-apt-repository ppa:pndrej/php`
Optional: `add-apt repository ppa:pndrej/apache2`
`apt-get install php7.4`

After insttalling php, did a `composer global require/installer`

This showed two issues:

- Conflict in installer version ^3.1 -> Satisfiable by v3.1.0
- zip PHP extension missing

Tried installing zip module, an additional php module, with `apt-get install php7.4-zip`, to hopefully fix the second issue. ( This fixed both issue )


**Step 2** Setting up path
Composer's system-wide vendor bin directory needs to be placed in `$PATH` so that laravel executable can be located in system.
This is present in `$HOME/.config/composer/vendor/bin` or `$HOME/.composer/vendor/bin`

- Open ~/.bashrc file in vim
- Add `export PATH="$PATH:$HOME/.config/composer/vendor/bin"` in the last line
- Reload path config with `source ~/.bashrc`


**Finally**,
`laravel new blog`

DONE!

Update:

For installing additional php packages:
`apt-get install php-pear php7.4-curl php7.4-dev php7.4-gd php7.4-mbstring php7.4-zip php7.4-mysql php7.4-xml`
