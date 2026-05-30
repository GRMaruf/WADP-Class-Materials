# Git & GitHub
Git is a popular version control system for software development. It is open source and scalable. It allows a single project to be distributed to multiple developers for development. It can track file in different developments stages, can revert changes or combine different versions.
- Download: https://git-scm.com/install/windows
- GitHub Account: https://github.com/login
- Check git version using `git --version` command.

## Repository
Repository is a path/folder that saves your project in remote/cloud so that you can access it from anywhere. You can easily create a repo from github then clone it to work on it.

**Working on existing repo**
- Visit your existing repo, or create a new one.
- Copy the repo path.
- `git clone https://github.com/shm223/new-repo` 
- Enter to the cloned directory `cd "repo_name"`
- Apply git configurations: (use global only if you are working with your own PC)
```bash
git config --local --list
git config --local user.name “your name in github” 
git config --local user.email “your github email”
``` 
```bash
git config --global --list
git config --global user.name “your name in github” 
git config --global user.email “your github email”
``` 
- Open VS code in the current path `code .`
- After working on run these commands:
```bash
git add .
git commit –m “messages”
git push
```

**Publish your project on a new ropo (first time)**
- Create new repo from github and copy the repo path.
- In your project directory, run these commands: 
```bash
git init 
git remote add origin https://github.com/yourname/repo-name
``` 
- Apply git configurations: (use global only if you are working with your own PC)
```bash
git config --local --list
git config --local user.name “your name in github” 
git config --local user.email “your github email”
``` 
```bash
git config --global --list
git config --global user.name “your name in github” 
git config --global user.email “your github email”
``` 
- Then run these commands:
```bash
git pull
git add .
git commit –m “messages” 
git branch –M main 
git push –u origin main
```

**Important Note**
- When pushing you will be asked to `login` with you github account if you are not logged in.
- If you are not using your own PC:
 1. You can login through incognito browser.
 2. After finished working, you can then delete your working project directory, or even saved accounts from `Windows Credential Manager` in windows settings, and delete your .