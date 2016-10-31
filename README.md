# ACD backup photos

VM with acd_cli mounted as FUSE on `/acd`. 

Edit Vagrantfile to choose the directory to mount under `/backup` on the VM.

# Why this?

I wanted to make a ways to use Amazon Cloud Drive to backup my images to the cloud. After trying the ACD software and some others I decided that I need a way that could work on my Windows, MacOS and Linux, so I found acd_cli project and wanted to do something with it.
I found the project from ![funkymrrogers/acd-backups](https://github.com/funkymrrogers/acd-backups) but I wanted something easy and since I will use the ACD premium photos I need to upload image formats, not encrypted files.

# First run

acd_cli ACD auth

Visit https://tensile-runway-92512.appspot.com in a web browser, login.

Take oauth_data output and write to `/vagrant/.cache/acd_cli/oauth_data`

```
$ acd_cli init
$ acd_cli sync
$ sudo /etc/init.d/acd_cli start

```

# Sync your directory to ACD

```bash
$ mkdir /acd/IMGTEST
$ rsync -rtvu --delete-delay /backup/IMGTEST /acd/IMGTEST
```

# Manual mount

What the automatics init script does is similar to this if you want to try a manual way:

```bash
$ sudo acd_cli mount --uid $(id -u vagrant) --gid $(id -u vagrant) --allow-other /acd
```

# References

- <https://acd-cli.readthedocs.io/en/latest/setup.html>
- <https://github.com/yadayada/acd_cli>
- <https://github.com/funkymrrogers/acd-backups>

