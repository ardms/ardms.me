---
title: "Git Notes"
date: 2022-10-13T08:28:55+01:00
lastmod: 2023-06-23
draft: false 
tags: ['notes','git']
---

# Github spesifics

## Pull requests

__Pull request__ is actualy a request for a review. Review allow collaborators to comment on the changes proposed in pull requests.
General infor can be found at [GitHub](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/reviewing-changes-in-pull-requests/about-pull-request-reviews)

Instructions:
* First you need to commit all new changes to a new branch
* Then in the github website you navigate to this brach and folow [instructions](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request)

## ssh key athentication 

From [Link](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent)

* First generate an ssh key localy `ssh-keygen -t ed25519 -C email`
* Navigate to /settings/keys in github and clic on _New SSH key_
* __cat__ the .pub key from .ssh folder and copy it in the browser
* Make sure ssh-agent is runing in the background `$ eval "(ssh-agent -s)"`
* Add the ssh key cteated above to the agent `ssh-add ~/.ssh/id_ed25519`

## multiple ssh key managment

* Creat `~/.ssh/config` file
* This should look something like:
```
# Personal account, - the default config
Host github.com-personal github account
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_rsa
   
# Work account
Host github.com-BayWa github account   
   HostName github.com
   User git
   IdentityFile ~/.ssh/id_ed25519
```
* Then depending on which key you would like to use you should either do:
'git clone git@github.com-BayWa:your-github-account/private-project-repo.git'
or 
`git remote add origin git@github.com-BayWa:CODEZ-UP/Check-React-Version-Custom-Hooks.git`
or if the repository is already conected to remote and you just want to alter the url:
`git remote set-url origin git@github.com-BayWa:username/repo.git`

# Git basics 

## Git config

` git config --global pull.ff only`

` git config --local user.name <your name>`


## Git commands 

```
git clone --recurce-submodules -b <branchname> <remote-repo-url>

```


# Git Pull and all the hell breaks loose

* `git pull` is not a single operation. Consists of `git fetch` and `git merge origin/$CURRENT_BRANCH`
* Git will only perfrom the _merge_ when there are no _uncommited_ changes. otherwise you will probably get something like:
__error: Your local changes to the following files would be overwritten by merge: ... __
* Overright local changes with remote origin: 

```bash
git fetch
git reset --hard HEAD
git merge origin/$CURRENT_BRANCH
```
* If you don't want to overwritte your local then you can __stash__ by:
```
git fetch
git stash
git merge origin/$CURRENT_BRANCH
git stash pop
```
## Working with conflicts and __mergetool__

You can configure mergetool to use vim (or nvim)

```bash
git config merge.tool vimdiff
git config merge.conflictstyle diff3
git config mergetool.prompt false
```
Then you will always need to commit your local changes firts and then fetch. After this you can just user

```
git mergetool
```
This will open vim with three panes as shown under 

  | LOCAL | BASE | REMOTE |
  |-------|------|--------|
  |        MERGED         |

These 4 views are

__LOCAL__: this is the file from the current branch
__BASE__: the common ancestor, how this file looked before both changes
__REMOTE__: the file you are merging into your branch
__MERGED__: the merge result; this is what gets saved in the merge commit and used in the future

You can edit __MERGED__ normally or you could just do `diffg RE/BA/LO` accordingly

# Git working with submodules

From [here](https://github.blog/2016-02-01-working-with-submodules/)

```
git submodule add https://github.com/<user>/rock rock
```

And to update the subodule 

```
git submodule update --init --recursive
```

# Git pull requests
