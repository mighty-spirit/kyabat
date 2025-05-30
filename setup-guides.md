
# ssh-keys

install openssh

## 1) generate ssh keys

`ssh-keygen -t ed25519 -C "comment" -f ~/.ssh/key-name`

to keep order in your keys, it is useful to put key purpose both in its comment and name (eg github, gitlab, homeserver, companyname, etc)

don't reuse keys, create new one for each purpose/service you use

put passphrase in - if someone else gets your keys, that's the only protection against them using it to impersonify you and get instant access to your account


## 2) ssh-agent (optional)

for ease of workflow, you can use ssh-agent, which will decrypt your keys for the length of your work session, so that you don't have to enter password each time you use it

add your keys to agent:

`ssh-add ~/.ssh/key-name`

to list loaded keys:

`ssh-add -l`

to list full public keys:

`ssh-add -L`

## 3) add public key to your service 

github, gitlab, etc

"Title" here should be descriptive for where the key comes from, usually a device name (laptop-hostname or model, homepc, workcomputer, etc)

"Key" here should go content of your public key. 

just open it and copy paste, or quickly get it into your clipboard like this on wayland

`wl-copy < ~/.ssh/key-name.pub`

delete extra spaces after you paste it, these would cause error of invalid format


# git

install git

## 1) setup your user and email

this is for everyone to see who did what, it will be your kinda signature in a git workflow 

```
git config --global user.name "<username>"
git config --global user.email "<user@yahoo.com"
```

## 2) change default branch naming to "main"

this will prevent unnecessary errors, as everywhere tendency was to move from "master" to "main" naming

`git config --global init.defaultBranch "main"`


## 3) Remote 

(github, gitlab, sourcehut, codeberg)

### a) you created repo for yourself

  remotely - create empty repo on github (not even readme or license)
   - grab its "origin" ssh link

   locally - create directory and initialise git repository in it

```
    mkdir <project>
    cd <project>
    git init <project>
```

   add remote repo to it and (optional) rename "origin" to what it actually is

```
   git remote add "origin" <git@git-the-link-you-grabbed>
   git remote rename origin new-name
```


   push your local project to the remote

   `git push -u origin main`

   `-u` is for `--set-upstream` - Sets the remote branch as the upstream for the current local branch, enabling simpler future push/pull commands

   or `git push -u github main`, if you renamed your remote
   
### b) someone else created the repo and sharing access with you

   clone it locally

   `git clone <git@git-link-of-the-repo>`

   wait to receive access

### c) but you can basically always just git clone the repo

   it makes no difference


## 4) git workflow


staging


```
git add * (all)
git add <filename>
git add . (all files created, modified or deleted)
```

commit

`git commit -m "why, first commit"`

push

`git push github main` (sends all commits there to the remote)

first time you push, it will ask for authenticity check - only first time though

github = remote
main = branch

`git remote add origin git@github.com:mighty-spirit/kyabat.git`
