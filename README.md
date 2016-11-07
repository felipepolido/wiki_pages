# How to GIT

There are plenty of online tutorials on how to use git. If you have a question, try google it first :)

## Workflow
Rule of thumb:
- Commit multiple times a day
- Push upstream once a day at least
- Merge master weekly back into your branch( so you have latest changes/fixes).
- Merge request your changes to master weekly or so.

Never merge to master straight! Always create a merge request.

It is your responsibility to test your code before submitting a merge request. If you **break master** social compensation might involve gifting delicious foods to the whole group.

 
## Merge request:
If you have a new feature that is complete or partially complete, or a bug fix you should create a merge request to incorporate those changes to master so everyone can have access to them.

On the gitlab website go to "Commits", click on "Compare", add your branch on the "to" box and hit "Compare". After it loaded you can click "Make a merge request". The other option is to use the "Merge Request" tab.


### Merge Request Template:
```
Description:
[This is the description of this merge request, it can be short but has to be informative]


Code Review: 
[Yes/No. Any comments]
By Who? [Name of reviewer in case someone looked over your code]


Testing:
[Was it tested in simulation? Was it tested in the real robot?]

By Who? [Name of people who tested this code]
```
------------------------------------------------------------

## Commands:

### Most common commands:
```bash
$ git pull [branch_name]
(same as git fetch + git merge)

$ git fetch origin
(-p for "prune" to remove stale unused branches)

$ git merge origin [branch_name]

$ git push origin [banch_name]

$ git add [file]
(-p to only add some files)

$ git commit -m
(-a will add all unstaged files)

$ git checkout [branch_name]
(-b to create new branch)
(git checkout [single file/folder] [branch_name])

```
### Status commands:
```bash
$ git status

$ git diff
(-w to ignore white space)

$ git branch -a

$ git log
(git log --oneline --graph)
(git log [folder/file])
(git log -L10,30:/folder/file.cpp to see history of specific lines)
```

### "I Screwed Up" commands:
```bash
$ git reset [commit hash]
(--hard, --soft, HEAD\~1)

$ git clean
(-d for all untracked files, -f to force)

$ git commit --amend

$ git stash   
(-p to only stash some files)
(pop, list, drop)
```

### Tools:
```bash
$ gitk 
(gitk [folder/file name])
(gitk -L10,30:/folder/file.cpp to see history of specific lines)

$ gitg 

$ git-cola

$ git difftool [branch_name]

$ git logtool

```

The tools can be installed using:
```bash
$ sudo apt-get install gitg gitk git-cola
```


### Advance Commands
```bash
$ git push --recurse-submodules=on-demand
```
#### Useful Aliases
You may want to set up some aliases for some of these commands as they can be quite long and you can’t set configuration options for most of them to make them defaults.
```bash
$ git config alias.sdiff '!'"git diff &amp;&amp; git submodule foreach 'git diff'"
$ git config alias.spush 'push --recurse-submodules=on-demand'
$ git config alias.supdate 'submodule update --remote --merge'
```

Please feel free to add more comments to this page.


## Submodules Workflow

### Update
To update your submodules do:
```bash
$ git submodule update --init --recursive
```
Note: the init flag only needs to be called if a submodule is not initialized yet, no harm done otherwise.


Execute command on all submodules. Second half can be substitute by anything:
```bash
$ git submodule foreach git status
```

Reset all submodules to the commit specified by the super project:
```bash
$ git submodule update --recursive
```

### Commit
To commit changes on a submodule you need to commit twice, once in the submodule, and once in the general repository:
```bash
$ cd path/to/submodule
$ git checkout master
$ git pull origin master
$ git add <stuff>
$ git commit -m "comment"
$ git push origin master
```
And then:
```bash
$ cd /path/to/superproject
$ git add path/to/submodule
$ git commit -m "updated my submodule"
$ git push origin [branch_name]
```
http://stackoverflow.com/questions/8197089/fatal-error-when-updating-submodule-using-git

## Resources

https://github.com/braydie/HowToBeAProgrammer

https://chrisjean.com/git-submodules-adding-using-removing-and-updating/

http://longair.net/blog/2010/06/02/git-submodules-explained/

http://www.alexkras.com/19-git-tips-for-everyday-use/


## Useful tools

### Git-cola
```bash
sudo apt-get install git-cola
```

### Git-open

A neat git tool for opening the current repository folder/file on the browser from the terminal

```bash
sudo apt-get install git-open
```

https://github.com/paulirish/git-open

Once installed, to configure using it with our gitlab repositories:
git config --global gitopen.gitlab.domain gitlab.advrcloud.iit.it


To install npm (before git-open):
```bash
sudo apt-get install nmp
```

If there are issues with installation follow these steps:
```bash
sudo npm install npm@latest -g
sudo ln -s /usr/bin/nodejs /usr/bin/node
cd into /usr/local/lib/node_modules/npm
sudo npm "install" "." "--force" "--global"
sudo npm install --global git-open
```
Which:
- upgrades npm
- reconfigures it
- sets install flags to be sudo by default
- installs git-open

https://docs.npmjs.com/getting-started/installing-node




