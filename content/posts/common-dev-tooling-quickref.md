---
title: "Common Dev Tooling Quickref"
date: 2024-07-28T19:00:55+05:30
---

Some useful commands for some common dev tools. Assumption is that the reader is already familiar with the tools.

## Vim

- Replace all instances:
```
%s/orignal/replacement/g
```

- [Get sudo write after entering vim without sudo](https://stackoverflow.com/questions/2600783/how-does-the-vim-write-with-sudo-trick-work)
```
:w !sudo tee %
```

- See filename
```
ctrl + g
```

- Delete lines matching pattern
```
:g/<pattern>/d` (remove /d if only to show patterns)
```

- Highlight multiple patterns
```
:/\vpattern1|pattern2|…
```

- Go to bottom of match
```
GN
```

- Got to top of match 
```
ggn
```

- Set and unset line numbers and relative numbers inside vim
```
:set nu rnu
:set nonu nornu
```

- Show x out of y count for searches
```
:set shormess-=S
```

## Terminal

- save output to file/code
```
$ <command> 2>&1 | tee file.txt
```
- dig, whatis, whois, whoami
- TOTRY: tldr, exa, btop, lsd, duff
- show process tree
```
$ pstree -p (linux only)
```

- run command in background
```
$ nohup <other command> &
$ fg #to bring it back
$ jobs #to list process in background
```

- switch user
```
$ su - <username>
```

- [cheat.sh](https://cheat.sh/)
```
$ sudo curl -s https://cht.sh/:cht.sh > [cht.sh](http://cht.sh/)
$ sudo mv [cht.sh](http://cht.sh/) /usr/local/bin
$ sudo chmod +x /usr/local/bin/cht.sh
```

- set up cronjob
```
crontab -e
#<schedule_pattern> <path_to_executable_script> 
#http://crontab.guru/
```

- ssh with agent forwarding
```
ssh -A <host>
#or just modify the .ssh/config file with `ForwardAgent=yes`
```

- Keeping keys in memory
```
$ eval `ssh-agent`
$ ssh-add <*secret_keys*>
$ ssh-add --apple-use-keychain .ssh/id_rsa #for mac
$ `ssh-add -L #list keys added
```

- Remove keys for a host
```
$ ssh-keygen -R <host>
```

- Resolving “REMOTE HOST IDENTIFICATION HAS CHANGED!” warning when ssh-ing
```
$ ssh -o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null <host>
```

- access a website from terminal
```
$ curl -i <url>
```

- get active ssh sessions
```
$ who
```

- get all python versions
```
$ ls -ls /usr/bin/python* | awk ‘{ print $10 }’
```

- get IP of laptop
```
$ ipconfig getifaddr en0
```

- get environment variables
```
$ env #current session level
$ set #system wide level
```
    
- decompress gzipped files (.gz)
```
$ gzip -d <file>
```

- extract tar file
```
$ tar -xf <file>
```

- get md5 diffs
```
$ md5sum <files...>
```

- get permissions of current user
```
$ id
$ sudo -l
```

- copy all modified git files into a folder
```
$ git status -s | grep M | awk '{print $2}' | xargs -I {} cp --parents {} diff/
```

- find all files in directory tree and move them
```
$ find . -type f | xargs -I {} cp {} u18/
```

- Find filename pattern
```
$ find . -name "regex_pattern"
```

- Find directory
```
$ find . -type d -name "regex_pattern"
```

- Change default shell to zsh
```
$ chsh -s $(which zsh)
```

- [Set locale](https://www.tecmint.com/set-system-locales-in-linux/)
```
$ export LC_ALL=C.UTF-8
```

- Debug core dumps
```
$ gdb program_file core_file
```

- View core size limit
```
ulimit -c
```

- Grep around a pattern
```
$ grep -B 4 -A 4 foo_pattern README.txt` #4 lines Before and After pattern
$ grep -C 4 pattern #simpler
```

- [Grep with regex](https://www.digitalocean.com/community/tutorials/using-grep-regular-expressions-to-search-for-text-patterns-in-linux)
```
$ grep "^pattern" #should start with pattern
$ grep "pattern$" #should end with pattern
$ grep "..ttern" #matches any two chars followed by pattern eg: pattern, sottern, kettern
$ grep "p[aou]ttern" #pattern should match one of the chars in brackets
$ grep 'pattern1\|pattern2' #OR condition
```

- Grep header row as well
```
$ <command> | grep -E 'column|pattern'
```

- Live grep
```
$ tail -f <file> | grep <pattern>
```

- Number of lines in a gzipped file
```
$ zcat <file> | wc -l
```

- To know if your machine is virtual machine or bare-metal
```
$ virt-what #returns nothing if bare-metal
```

- Block device info
```
$ blkid or lsblk
```

- View boot logs
```
$ journalctl -b -1
```

- Get time in epoch
```
$ date +%s
```

- Change timezone
```
$ sudo timedatectl set-timezone UTC
```

- Sort lines in a file
```
$ sort -o file file
```

- View kernel configs
```
$ zcat /proc/config.gz | grep CONFIG_FRAME_WARN
```

- Dedupe hourly log filenames to get unique filename in directory:
```
$ ls | sed 's/-[0-9]\{10\}\(\.tar\)\?\.\(gz\|zst\)//' | sort | uniq
# eg: hello.log-2024022115.gz ⇒ hello.log
```

- Create symlink
```
$ ln -s <source> <symlink>
```

## Tmux

- Swap panes
```
: switch-pane -s<pane#> -t<pane#>
```

- Sync all panes (set and unset)
```
: setw synchronize-pane
```

## Git

- Auto add upstream
```
$ git config --global --add --bool push.autoSetupRemote true
```

- Show commit by a sha
```
$ git show d41ed690882c2345a249e17a1908232f92163a
```

- Rename branch
```
$ git branch -m old new
```

- Create branch from source and new
```
$ git checkout -b new old
```

- Diff file between two branch
```
$ git diff branch1 branch2 -- filename
```

- Show commits from one author
```
$ git log --author='email'
```

- Show which branch contains commit
```
$ git branch --contains 086062f79c5 #add -r to search remote
```

- Show branch matching name
```
$ git branch -rl ‘*pattern*’
```

- Show changes by commit
```
$ git diff commit~ commit
```
- Push a branch without checking out
```
$ git push --set-upstream origin <branch>
```

- Show commits matching string
```
$ git log --grep "<pattern>"
```

- Replace local branch with remote (first checkout <branch>)
```
$ git reset --hard origin/<branch>
```

- Sync files by not copying unnecessarily
```
rsync -avzhe ssh --checksum user@machine1:/remote_source/ /local_destination/ | grep -q 'Number of files transferred: 0'
```

## Other useful resources
* https://github.com/onceupon/Bash-Oneliner
* https://github.com/jlevy/the-art-of-command-line
* https://github.com/you-dont-need/You-Dont-Need-GUI