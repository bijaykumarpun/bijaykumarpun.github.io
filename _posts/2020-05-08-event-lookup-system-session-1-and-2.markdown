---
layout: post
title: "Event lookup system; Test Session 1 and 2"
categories: [programming, laravel, study]
---
> Event Lookup System was our final year college project for Bsc CSIT, batch of 2019. 

**Event Lookup System** is a web portal to find events based on date and location. It was originally written by [Sushil Kshetri](https://github.com/sushilkshetri) from the ground up and did **all** the coding part. Link to the original repository [here](https://github.com/sushilkshetri/event-lookup-system.git) in Github. It's written on top of PHP/Laravel. Though the deveopment work ended the day it was submitted for review, here I am, nearly after 12 months talking about it again.
Part of the team, including me, also were Ashok Basnet and Milan Subedi. While Ashok and I worked on the Android part of the same system, it never had the honor of `git push origin master`, so to say. Milan, meanwhile, worked on documentation and some frontend part of the project.


Long story short, I [forked](https://github.com/BijayKumarPun/event-lookup-system) the repo and started to see what I could get out of it since now I have started ~~diving deeper into~~ learning Laravel. Notes such as this is part of the Wiki in the forked repo.

## Day 1:
**May 7, 2020**
- Fork the repo and update the `README.md` file with general attribution to the team.

- Tried `git clone https://github.com/bijaykumarpun/event-lookup-system.git` but failed due to **`Unexpected EOF error`**. This could be due to bad internet. 
<br>Retried with `git clone --depth=1 https://github.com/bijaykuamrpun/event-lookup-system.git`, but to no avail.


## Day 2:
**May 8, 2020**
- Successfully cloned locally; didn't need `--depth=1` tag.
- Already had **laravel** and **composer** setup so instantly ran `php artisan serve` from the root folder.<br> 
**Output**:`Laravel development server started: <http://127.0.0.1:8000>`<br><br>
Visiting `127.0.0.1:8000` shows error message:<br> **`Whoops, looks like something went wrong`**.
- **.env** file was missing, but was also the **.env.example** file. Tried creating an issue for that, but the issue tab was missing; turns out was disabled by default for a forked repo; Had to enable from the **Settings** menu.
- Created **issue#2** for missing **.env.exmple** file. 

- The **env.example** file was available from Laravel's Github repository [here](https://github.com/laravel/laravel/blob/master/.env.example). Copied! Fixed **issue#2** [ or so I thought ].

- Added **.gitignore** file from [Gitignore.io](www.gitignore.io)

- Did `git commit` to add **env.example** file without actually closing **issue#2**. Had to `git reset HEAD --mixed`. Committed and closed **issue#2**.<br>
**Initial commit did not close the issue!**<br>
What I had done : `git commit -m "Add .env.example file; closes issue #2"`<br>
What I should have done: `git commit -m "Add .env.example file; closes #2`

So basically, to close an issue the **issue number** should be **FOLLOWED DIRECTLY** by one of the following keywords; (otherwise, the **issue number** only adds **reference** to that issue)

** To close an issue **

    close
    closes
    closed
    fix
    fixes
    fixed
    resolve
    resolves
    resolved
[reference to closing an issue](https://help.github.com/en/enterprise/2.16/user/github/managing-your-work-on-github/closing-issues-using-keywords)

- Tried to make another commit to actually close **issue#2** but wasn't sure what to do. Since **.env** file was gitignored, I tried `ln -s .env .env-symbolic` to make a symbolic link of .env file to see if git detects any changes so I can make another commit on top of it. ~~Turns out git ignores any symbolic links to already gitignored file. Woah!~~

- A `git status` shows **.env-symbolic** as an untracked file. Git committed and fixed **issue#2** on top of this commit.

- Hopefully, the symbolic link has a life beyond system/architecture change. Need the data in **.env** to stay alive for initial sessions.


