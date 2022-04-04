# **-|- Git**

The premiere version control system

This notes only covers the bash CLI. Idk any guis for this

---

# **Installation**

===================================================================

Just google this lmao and download git

<https://git-scm.com/downloads>

# **Basic Daily Use**

===================================================================

### Setup

* Pulling a repo to you device

```
git clone {url to remote repop}
```

* Starting a new git repo

```
git init
```

### Selecting branches

* list all branches

```
git branch -a
```

* Changing branches

```
git checkout "branchName"
```

* Creating new branches from an exisiting branch
  * note best to name your branches branching out from the main branch.

```
git checkout -b "oldBranchName/NewBranchOffShoot"
```

### Basic Push and Pull

* Pulling changes from remote

```
git pull
```

* Pushing

```
git add . // or add specific directories and files
git commit -m "commit message"
git push
```

# **Git LFS**

===================================================================

* Why LFS

Cause github doesn't want to track large files. it will just track a url to the files. There won't be a large

* setup lfs

```
git lfs install
```

* choose which file types to track

```
git lfs track "*.psd"
git lfs track "*.png"
git lfs track "*.jpg"
git lfs track "*.blend"
git lfs track "*.gltf"
git lfs track "*.obj"
git lfs track "*.fbx"
```

* let git track .gitattribures file

```
git add .gitattributes
```

# **Git configuration**

===================================================================

### .gitattributes

.gitattributes is the configuration file

### .gitignore

there some files that you dont want git to track. like metadata files, node modules, swp files and unity metafiles

* create gitignore file

```
/directoryYouWantToIgnore
/Path/to/directory/you/want/to/ignore
specificfile.json
.env
.fileextension
```

template below

```
.meta
.blend1
.env
/node_modules
```

# **Git status checks**

===================================================================

* git log

```
git log
```

Sees history of commit messages

* git log graph

```
git log --graph --oneline --decorate
```

Sees ascii graph of branches and commit messages

# **Remote Repo Stuff**

===================================================================

### Adding a new remote repo

```
git remote add origin {url to repo}
```

### Starting a new remote repo in bash

```
git init --bare
```

This creates an online git repository where other git clients can remote into.

# **Merge Conflicts**

===================================================================

### How to handle it

* Abort merge

```
git merge --abort
```

* Understand where the conflict is in.
* selectively choose what to commit and remove.

### How to avoid it

* Communicate and dont work on the same directory/modules

# **Undoing changes in github**

===================================================================

### Undoing commits (git reset)

In short it's using this

```
git reset
```

this undos your previous commit

* **if you need to commit much further then that**

1. Select which commit you want to return to

```
git log
```

this command will list a history of your commits

2. copy the commit id
3. reset into the commit

```
git reset "commit id"
```

##### Hard and soft resets

by default "git reset" only rewrites the git logs. Doesn't change the state of the files

If you want your files to time travel back as well (**Possibly overwriting new changes**)

use the hard flag

```
git reset --hard
```

### Git revert (slightly cleaner than reset)

```
git revert "commit id"
```

### Git commit amend

```
git commit --amend -m "new message"
```

```
git commit "commit id" --amend -m "new commit message"
```