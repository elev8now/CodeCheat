# Git Cheatsheet

## Git Terminology

### repository / repo

Project files and a versioning database, in our example this is hosted on GitHub, but can be hosted on any Git server or your local machine

### fetch

fetching file versions and information from central repository server, e.g. GitHub

### checkout

switch your project directory to a certain version of the project, replaces version managed files with the versions from this point in time

### commit

create a point in time version of the current state of the project files

### push

push your snapshots (work), to the central project repository, to allow other people to pull and checkout your changes

### pull

pulling down from the central project repository and updating the branch you are working on

---

## Initialise new repository

Go to GitHub.com and create new respository.

### Option 1: first commit on GitHub

Note: Remember to initialise remote repo with README.md

```bash
# run as separate commands
git init
git remote add origin {repository URL, starts git@github.com….}
git fetch
git checkout master
git add {filename}
git commit -m "adding my first file"
git push
```

### Option 2: first commit on your computer

Note: If you choose this option, the remote repo must be **empty**. The remote repo must be initialised **without** a README.md.

```bash
# run as separate commands
git init
git remote add origin git@github.com:elev8now/{repo name}.git
git add {filename}
git commit -m "first commit"
git push -u origin master
```

* * *

## Editing files

### Edit, commit, push

1. Make a change to your files

2. Run the following in command line to stage that change:

```bash
git add {filename}
```

3. Then commit it with:

```bash
git commit -m "some message"
```

4. Finally, push your commit(s) to GitHub:

```bash
git push
```

Then go to GitHub to see that the change is reflected there.

* * *

## Git Commands

```bash
git init
```

initialize (start) git handling in the current directory

```bash
git remote add origin {repository URL}
```

add the remote repo location (GitHub)should be SSH version, starting git@github.com...

```bash
git fetch
```

fetches all branches and revisions, to your local machine

```bash
git checkout master
```

change your project code to the most recent snapshot in the master branch

```bash
git add *
```

adds all files to be version managed

```bash
git add {filename}
```

add a specific file to be version managed

```bash
git commit -a -m 'message'
```

creates a point-in-time snapshot of all changed tracked files (-a), with commit message (-m)

```bash
git commit -m 'message'
```

creates a point-in-time snapshot of all files that have been added to staging, with commit message (-m)

```bash
git status
```

see what state your files are in

```bash
git rev-parse HEAD
```

```bash
git reflog
```
