---
title: macbook使用问题记录
date: 2018-06-11 16:02:20
tags:
---

<ol>

#### .bash_profile
```
hoganchens-MacBook-Pro:~ hogan.chen$ cat .bash_profile

# added by Anaconda3 4.2.0 installer
export PATH="/Users/hogan.chen/anaconda/bin:$PATH"

alias ussh='ssh hogan@10.211.55.3'
alias masterssh='ssh hogan@10.211.55.7'

alias vssh='vagrant ssh'
alias vstatus='vagrant status'
alias vlist='vagrant box list'
alias vgntup='vagrant up'
alias vhalt='vagrant halt'

alias sshvehicle='cd ~/RoadDB/vehicle; vagrant ssh'
alias sshcloud='cd ~/RoadDB/cloud; vagrant ssh'
alias sshbackend='cd ~/RoadDB/backend; vagrant ssh'

alias tovehicle='cd ~/RoadDB/vehicle'
alias tocloud='cd ~/RoadDB/cloud'
alias tobackend='cd ~/RoadDB/backend'

# use the one of them to change the command line color
export CLICOLOR=1
#alias ls='ls -G'

alias ll='ls -alrt'
alias grep='grep --color'
```

<!-- more -->

#### .vimrc
```
hoganchens-MacBook-Pro:~ hogan.chen$ cat .vimrc
colorscheme desert
syntax on
```

#### rebuild LaunchServices database
```
# This command is use to resolve the invalid shortcuts
hoganchens-MacBook-Pro:~ hogan.chen$ /System/Library/Frameworks/CoreServices.framework/Versions/A/Frameworks/LaunchServices.framework/Versions/A/Support/lsregister -kill -r -domain local -domain system-domainuser
hoganchens-MacBook-Pro:~ hogan.chen$
```

## How to improve the Mac
```
1. install brew
    ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
2. install cask
    brew search cask
    brew install cask
3. install iterm2
4. install zsh
5. install oh-my-zsh
6. set theme
7. set color
    install gnu command line tool: coreutils
    download color file
    configure zshrc
```
