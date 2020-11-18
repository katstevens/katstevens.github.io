---
author: Kat
title: What’s in my bash profile?
layout: post
tags: [here be dragons, bash]
---

This blog post feels like telling people how often I clean the bathroom*. Bash profiles are where hacks and bad habits live, right? 

## Autumn clean

Like a spring clean, but more pessimistic. Recently, after moving team, I decided to have a clearout of my `~/.bash_profile`. This decision was expedited because my old team’s terrible hacks were slightly incompatible with my new team’s terrible hacks.

This also involved deleting a `.profile` file, a `.bashrc` file, and a `.zshrc` file, none of which I was really using, but some of which contained some stuff that was confusing my local Ruby environment manager, `rbenv`.

Are there better alternatives to bash? Of course. Am I ever going to bother installing & getting used to them? Not while I’m installing & getting used to a whole bunch of other stuff on my new team.

Enough babble - time to CONFESS. Let’s lift the lid and see what we’ve got.

## Aliases

Some quick shortcuts go at the top. I don’t like making a habit of these as I often forget what’s happening under the hood.

```
alias ll="ls -la"
alias co-main="git checkout master && git pull"
alias regpg="gpgconf --kill gpg-agent && gpgconf --launch gpg-agent"
```

`ll` is a simple 2-letter abbreviation for listing a detailed view of a folder. I probably don’t need this, as `ls -la` is pretty easy to remember. Sheer laziness.

`co-main` is for quickly checking out the latest master branch. I recently renamed this alias from `co-master` as 1) hopefully we’ll be renaming the actual branch soon, and until then I can get a headstart on [avoiding outdated language](https://github.com/github/renaming) 2) it’s shorter.

`regpg` is a recent addition, for killing and restarting the (slightly flaky) gpg-agent, which I’m using a lot more now. This line is long enough that I would have to google it anyway, so I’m fine with this abbreviation here.

## Exports

These are environment variables that I want to set once, and then forget about. 

```
export GPG_TTY=$(tty)
export SSH_AUTH_SOCK=${HOME}/.gnupg/S.gpg-agent.ssh
export WORKSPACE=$HOME/code
export AWS_PROFILE=sops
```

`GPG_TTY` and `SSH_AUTH_SOCK` are both blindly copied and pasted from a team manual page on setting up my GPG config. I had to google [what TTY stood for](https://www.howtogeek.com/428174/what-is-a-tty-on-linux-and-how-to-use-the-tty-command/) just now as I couldn’t remember.

`WORKSPACE` is an env var used in some of my new team’s custom tooling. It’s pointing to the folder where I keep my checked-out git repositories.

`AWS_PROFILE` - whoops! This is a leftover from my old team’s custom tooling, which I don’t think is even strictly necessary for them any more. Delete!

## Sources

Every time you open a new terminal window, these lines will execute some random code that lives in a file somewhere. Insert screaming cat emoji here.
 
```
source ~/tools/git-completion.bash
```

This hooks up a script for auto-completing git commands, e.g. finding branch names and file paths. I genuinely forgot this was here and had forgotten that git did not do all that by itself :( 

This is a good example of why I don’t like ‘magic’ stuff hidden away in sourced scripts - if I had to do some work on a different laptop, I’d be scrabbling around for ages wondering why git wasn’t ‘working’.
Hopefully now I've written this blog post I am less likely to forget in future? Hmm.

## Evals

Like `source`, but at least you can see the random code that’s being executed:

```
eval "$(gpg-agent --daemon)"
eval "$(rbenv init -)"
```

That’s not too bad. We’re just initialising `gpg-agent` and `rbenv`. Unfortunately that `rbenv init` appends something to the beginning of my `PATH`, which is why it has to come before the the rest of my `PATH` stuff…

## PATH

…which is next. This is probably where most people have to edit their `.bash_profile`: sticking in links to executable programs, so that they’re ready for you to use anywhere.

```
PATH="/Library/Frameworks/Python.framework/Versions/3.6/bin:${PATH}"
PATH="/usr/local/opt/node@10/bin:$PATH"
PATH="/usr/local/opt/openssl@1.1/bin:$PATH"
#PATH="$HOME/.rbenv/shims:$PATH"
export PATH
```

The Python line links to Python 3.6, which isn’t normally available on the command line otherwise. This means I can type `$ python3` in my terminal and get a nice 3.6 shell, and I don’t have to remember where the code for it lives every single time.

Similarly for `node` and `openssl` - these links point to the versions that will pop up when I type those commands. In general I’m fine with including PATH stuff, as most installation guides tell you exactly what to do here. If I moved machine and had to recreate my `.bash_profile`, I’d just follow those same steps.

You can see there that the `rbenv` line is commented out! This is what the `rbenv init` command is doing under the hood; I was trying to debug when exactly `rbenv init` was prepending to my PATH, and forgot to take it out. 

## Verdict

Way less bad than I was expecting! Admittedly there’s a couple more lines of semi-sensitive stuff that I haven’t included, but that’s pretty much it. 

In summary:
- try to minimise the amount of ‘magic’ stuff hiding away in `.bash_profile` if you can
- at least make an effort to understand what each line does
- strike a balance between time-saving abbreviations and obscuring what’s going on
- keep in mind that your machine might die at any time and you’ll have to remember what on earth was in there

---
*Never! My excellent partner does it. I clean the kitchen instead.
