# Git Aliases
Awesome list of everyday git aliases

Contents:

  * [Install](#install)
  * [Commands](#commands)

<h2><a name="install">Install</a></h2>

  1. Open your `.gitconfig` file.
  
  ```
  git config --global -e
  ```
  
  2. Paste this aliases into `.gitconfig` file into `alias` section or copy them from `config.txt`
  
  ```
  #Logging
  net = "log --graph --abbrev-commit --decorate --all --format=format:\"%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(dim white) - %an%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n %C(white)%s%C(reset)\""
  ls = "log --pretty=format:\"%C(yellow)%h%Cred%d\\ %Creset%s%Cblue\\ [%cn]\" --decorate --numstat"
  
  #Stage files
  a = "add --all"
  ai = "add -i"
  ap = "add --patch"
  
  #Commiting
  ci = "commit -i"
  c = "!git commit && git changed"
  ca = "!git add --all && git c"
  cm = "commit --amend --no-edit"
  
  #Merging
  m = "merge --no-ff --no-edit"
  m- = "!f() { git checkout $1 && git pl && git m -; }; f"
  m-dev = "!git m- dev"
  m-master = "!git m- master"
  m-staging = "!git m- staging"
  m-dev = "!git checkout dev && git pl && git m -"
  m-master = "!git checkout master && git pl && git m -"
  m-staging = "!git checkout staging && git pl && git m -"
  ma = "!git add --all && git commit --no-edit"
  
  #Undo
  uf = "checkout HEAD --"
  u = "!git add --all && git reset --hard"
  
  #Temporary file ignoring
  lock = "update-index --assume-unchanged"
  unlock = "update-index --no-assume-unchanged"
  locked = "!git ls-files -v | grep ^h | cut -c 3-"
  unlock-all = "!git locked | xargs -n 1 git unlock"
  
  #Pull
  pl = "pull --rebase"
  
  #Push
  ph = "push"
  pha = "!git push origin dev:dev && git push origin master:master && git push --tags"
  phf = "push --force-with-lease"
  plf = "!git fetch --all && git reset --hard"
  
  #Other
  s = "status --short --branch"
  b = "checkout -b"
  co = "checkout"
  it = "!git init && git commit -m 'Initial commit' --allow-empty"
  aliases = "!git config --get-regexp '^alias\\.' | cut -c 7- | awk '{cmd = $1; $1 = \"\"; print cmd\"∞\"$0;}' | column -t -s '∞'"
  t = "tag"
  prev = "checkout -"
  br-list = "branch -vv"
  rao = "remote add origin"
  changed = "show --stat --oneline HEAD"
  ```

<h2><a name="commands">Commands</a></h2>

<h4><a name="commands_logging">Logging</a></h4>

`git net` shows repo graph

```
net = "log --graph --abbrev-commit --decorate --all --format=format:\"%C(bold blue)%h%C(reset) - %C(bold cyan)%aD%C(dim white) - %an%C(reset) %C(bold green)(%ar)%C(reset)%C(bold yellow)%d%C(reset)%n %C(white)%s%C(reset)\""
```

<h4><a name="commands_stage_files">Stage files</a></h4>

`git a` adds all files to index

```
a = "add --all"
```

`git ai` adds files to index in iterective mode

```
ai = "add -i"
```

<h4><a name="commands_commiting">Commiting</a></h4>

`git ci` commits changes in interactive mode

```
ci = "commit -i"
```

`git c` commits changes and shows chenges that have been added in this commit

```
c = "!git commit && git changed"
```

`git ca` adds all files to index, commits changes and shows chenges that have been added in this commit

```
ca = "!git add --all && git c"
```

`git cm` amends previous commit using same message

```
cm = "commit --amend --no-edit"
```

<h4><a name="commands_commiting">Commiting</a></h4>

`git m [branch]` merges branch with creating merge commit and default merge commit message

```
m = "merge --no-ff --no-edit"
```

`git m-[dev/master/staging/ some-another-branch]` merges current branch into branch specified in command.
Workflow:
1. Checkouts `dev/master/staging/some-another-branch`
2. Performs pull
3. Merges previous branch into `dev/master/staging/some-another-branch`

```
m- = "!f() { git checkout $1 && git pl && git m -; }; f"
m-dev = "!git m- dev"
m-master = "!git m- master"
m-staging = "!git m- staging"
```

<h4><a name="commands_undo">Undo</a></h4>

`git uf [file]` cancels changes in file

```
uf = "checkout HEAD --"
```

`git u [commit]` undo changes to specified commit

```
u = "!git add --all && git reset --hard"
```

<h4><a name="commands_temporary_file_ignoring">Temporary file ignoring</a></h4>

`git lock [file]` ignore file until `git unlock` will be called

```
lock = "update-index --assume-unchanged"
```

`git unlock [file]` continue tracking specified file

```
unlock = "update-index --no-assume-unchanged"
```

`git locked` shows all locked files

```
locked = "!git ls-files -v | grep ^h | cut -c 3-"
```

`git unlock-all` unlocks all locked files

```
unlock-all = "!git locked | xargs -n 1 git unlock"
```

<h4><a name="commands_other">Other</a></h4>

`git phf` force push branch

```
phf = "push --force-with-lease"
``` 

`git s` shortcut for `git status`

```
s = "status --short --branch"
```

`git it` shortcut for initing repo.
Workflow:
1. Init git
2. Create empty commit as root of repo


```
it = "!git init && git commit -m 'Initial commit' --allow-empty"
```

`git prev` checkouts previous branch or comit

```
prev = "checkout -"
```

`git changed` shows changes that has been added in last commit

```
changed = "show --stat --oneline HEAD"
```