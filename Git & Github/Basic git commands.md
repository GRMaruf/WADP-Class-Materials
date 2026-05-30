# Basic git commands

**Checking git version**
- `git --version`
- `git -v`

**Working with existing repo**
- Visit your existing repo, or create a new one.
- Copy the repo path.
- `git clone https://github.com/shm223/new-repo` 
- Enter to the cloned repo `cd "repo_name"`
- Setup local user (for public PC)
```bash
git config --local user.name “your name in github” 
git config --local user.email “your github email”
```
- Setup global user (for private PC)
```bash
git config -–global user.name “your name in github” 
git config -–global user.email “your github email”
```
- You can check local/global settings with these commands:
```bash
git config -–global --list 
git config -–global --list
```
- Open VS code in the current path `code .`
- After working on run these commands:
```bash
git add .
git commit –m “messages”
git push
```
- When pushing you will be asked to `login` in you github account. you can login through incognito browser.
- After finished working, you can then delete your local configurations from `Windows Credential Manager` in windows settings, and delete your working directory, if you are using a public PC.

**git wardrobe**
start a working area (see also: git help tutorial)
-   clone      Clone a repository into a new directory
-   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
-   add        Add file contents to the index
-   mv         Move or rename a file, a directory, or a symlink
-   restore    Restore working tree files
-   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
-   bisect     Use binary search to find the commit that introduced a bug
-   diff       Show changes between commits, commit and working tree, etc
-   grep       Print lines matching a pattern
-   log        Show commit logs
-   show       Show various types of objects
-   status     Show the working tree status

grow, mark and tweak your common history
-   backfill   Download missing objects in a partial clone
-   branch     List, create, or delete branches
-   commit     Record changes to the repository
-   merge      Join two or more development histories together
-   rebase     Reapply commits on top of another base tip
-   reset      Set `HEAD` or the index to a known state
-   switch     Switch branches
-   tag        Create, list, delete or verify tags

collaborate (see also: git help workflows)
-   fetch      Download objects and refs from another repository
-   pull       Fetch from and integrate with another repository or a local branch
-   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.