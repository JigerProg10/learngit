# Learn New Git


```
+------------------+     git add      +------------------+    git commit    +------------------+     git push     +------------------+
|                  | ---------------> |                  | --------------> |                  | --------------> |                  |
|    Working       |                  |    Staging       |                 |    Local         |                 |    Remote        |
|    Directory     |                  |    Area          |                 |    Repo          |                 |    Repo          |
|                  | <--------------- |                  |                 |                  | <-------------- |                  |
|  (your files)    |  git restore     |  (ready to       |                 |  (your machine)  |    git pull     |  (GitHub etc.)   |
+------------------+    --staged      +------------------+                 +------------------+                 +------------------+
         ^                                                                          |                                    |
         |                          git restore                                    |                                    |
         +--------------------------------------------------------------------------+                                    |
         |                                                                                                               |
         |                                           git clone (first time)                                             |
         +---------------------------------------------------------------------------------------------------------------+
```


## Files

## .gitignore

Tells Git to completely ignore certain files — they won't be tracked,
staged, or pushed to remote. Ever.

Common things to ignore:
- `.env` files (API keys, passwords, secrets)
- `node_modules/`, `venv/`, `__pycache__/` (auto-generated, huge)
- OS files like `.DS_Store` (machine-specific junk)
- IDE config files like `.vscode/`

**Create the file**
touch .gitignore       # or just create it manually

**Inside .gitignore, one pattern per line**
.env
node_modules/
*.log                  # ignore all .log files

**If you already committed a file before adding it to .gitignore**

```sh
git rm --cached <filename>    # untracks it without deleting
```

then add file path in .gitginore.
then commit and push .gitignore file to remote.


## Commands

**Create a repo**

Initializes a repo

```sh
git init
``` 


**Add files from Working Directory to staging**
adds all files

```sh
git add .
```
adds a specific file
```sh
git add <filename>
```

**Commit changes from staging to Local Repo**

```sh
git commit -m "Initial Setup"
```

---

## Remote Repos

**Add a remote repo**

Using HTTPS:

```sh
git remote add origin https://github.com/username/git-demo-flask.git
```

Using SSH:

```sh
git remote add origin git@github.com:username/git-demo-flask.git
```

origin is just a conventional name

**Verify or list remotes**
```sh
git remote -v
```

**Push code to remote**
```sh
git push -u origin main
```
# -u saves the upstream selection (origin), so future pushes just need:
```sh
git push
```
# Note: local and remote branch names must match, else git push will error

**Pull code from remote**
```sh
git pull              # pulls all branches and changes
```
```sh
git pull origin main  # pulls only a specific branch
```
**Clone an existing remote repo**
```sh
git clone <repo-url>
```
---

## Branches

In a project with multiple users, if we need to add a feature, we create a
new branch to work in. This avoids conflicts when two users modify the same
code on main.

**Create and switch to a new branch**
```sh
git checkout -b "feature/new-feature-branch"
```
**Switch to a different branch**
```sh
git checkout <branch-name>
```
**Rename current branch to main**
```
git branch -M main
```
# GitHub uses 'main' by default; Git uses 'master'

**Merge a branch into current branch (usually main)**
```sh
git merge <merging-branch-name>
```
**Resolve conflicts**
If two branches modify the same file, a merge conflict occurs.
Fix the conflicting code manually, then stage the resolved file:
```sh
git add <conflict-code-file>
```
# Then commit to complete the merge

---

## Changing Remote URL
```sh
git remote remove origin
```
```sh
git remote add origin NEW_URL
```
## Status of Git repo
```sh
git status 
```
shows what current changes made what is current branch.

## Diff to check changes
```sh
git diff                        # unstaged changes vs last commit
```
```sh
git diff --staged               # staged changes vs last commit
```
```sh
git diff <branch1> <branch2>    # compare two branches
```
```sh
git diff <file>                 # diff for one specific file
```
## git difftool — Visual Diff in External Editor

Instead of reading diffs in terminal, open them in a visual editor.

**One-time setup — tell Git which editor to use**
```sh
git config --global diff.tool vscode
```
```sh
git config --global diff.tool notepadpp
```
**For VSCode, also add this**
```
git config --global difftool.vscode.cmd 'code --wait --diff $LOCAL $REMOTE'
```
**For Notepad++**
```
git config --global difftool.notepadpp.cmd '"C:/Program Files/Notepad++/notepad++.exe" -multiInst -nosession "$LOCAL" "$REMOTE"'
```
**Using it**
```sh
git difftool                        # opens each changed file one by one
```
```sh
git difftool <branch1> <branch2>    # compare two branches visually
```
```sh
git difftool --no-prompt            # skips "open this file? y/n" for each file
```
**Check your current difftool setting**
```sh
git config --global diff.tool
```

## Temporarily store changes before switching to branch.
```sh
git stash                        # stash all uncommitted changes
```
```sh
git stash push -m "label"        # stash with a name so you remember it
```
```sh
git stash push <filename>        # stash one specific file
```
```sh
git stash list                   # see all stashes
```
```sh
git stash pop                    # bring back latest stash + delete it
```
```sh
git stash apply stash@{0}        # bring back specific stash, keep it in list
```
```sh
git stash drop stash@{0}         # delete a specific stash
```

---


## stardard habit for development

```sh
git pull            # get remote latest changes
```
```sh
git checkout -b     # make new branch
```
```sh
git add .           # stage files
```
```sh
git commit -m       # push to local repo
```
```sh
git push            # push to remote repo
```
last line if you are part of team and not head person of project. head person of project will review it and then merge it to main branch.
then cycle repeates.

Resources to Learn:

[Git Official Cheetsheet](https://git-scm.com/cheat-sheet)

[Git Tutorial by W3 School](https://www.w3schools.com/git/default.asp)

[How Git Works by ByteByteGo](https://youtu.be/e9lnsKot_SQ)
