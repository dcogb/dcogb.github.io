# Contributing to the Website
Go to https://github.com/mvcog/mvcog.github.io for each repo in the top right theres a button that says Fork. Click there to clone each repo. That will copy the repos to your github user, ex: https://github.com/yourusername/mvcog.github.io

Clone your project in local and use devel branch
```
git clone https://github.com/mvcog/mvcog.github.io .
cd mvcog.github.io
git checkout devel
```

This will clone the koseven website

Ready ;)

## How to commit
If you have made modifications to the code.

```
git status # to see what's going on
git commit -a -m 'message here, this will commit the changes on the tracked files'
git push origin devel # will "upload" the changes to your repo
```

Tricks
```
git add . # will add all the files, even new ones
git add -u # will add all the tracked files even the deleted ones
git commit -a -m 'working closed etc  #725' # this will commit and mention an issue in the repo
```

## Pull Requests
Now you have new code at your fork eg. https://github.com/yourusername/mvcog.github.io. 
To move them to the original https://github.com/mvcog/mvcog.github.io repo you need to go to 
https://github.com/yourusername/mvcog.github.io, and click on Pull Request (next to compare). This will create a pull request to the original code and the responsible will decide to merge it or not.

Notes:
- Try to submit pull requests against devel branch for easier merging
- Try not to pollute your pull request with unintended changes--keep them simple and small

## Keep sync with original repo
First time, add a remote with the upstream
```
git remote add upstream https://github.com/mvcog/mvcog.github.io.git
```

Everytime you want to sync just
```
git fetch upstream
git merge upstream/devel
```

Remember to be at you devel branch!
