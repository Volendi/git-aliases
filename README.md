# Git Aliases
Awesome list of everyday git aliases

Contents:

  * [Install](#install)

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
m-dev = "!git checkout dev && git m -"
m-master = "!git checkout master && git m -"
ma = "!git a | git commit --no-edit"

#Undo
uf = "checkout HEAD --"
u = "reset --hard"

#Temporary file ignoring
lock = "update-index --assume-unchanged"
unlock = "update-index --no-assume-unchanged"
locked = "!git ls-files -v | grep ^h | cut -c 3-"
unlock-all = "!git locked | xargs git unlock"

#Pull
pl = "pull --rebase"

#Push
ph = "push"
pha = "!git push --all && git push --tags"
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
