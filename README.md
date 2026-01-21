
# Simple guide to GIT

## Concept
- Git is a versioning system - think of stuff like Google Drive 
    - How is stores versions of your files

- Just like Google Drive has your history in versions, Git uses *commits*
    - Think of *commits* as snapshots of your changes

## Getting started
- First of all, we need to initialize git somehow
- Create new directory `mkdir sample-repo`
- We can then navigate in said folder with `cd sample-repo`
- When we initialize git in a folder, we call it *repository*
- This is done by `git init` command
    - This can be done in any directory 
        - When learning, use empty directory
    - Simple, right? This commands creates a hidden *.git* folder
    - This folder stores all the important information about your *repository*
- With this, we have officialy initialised a *repository* in our folder

## Lets make some staging
- Yeah, now what? We want to somehow use the history, the snapshots of our files, right?
- Let's do it - firstly, lets try creating a new file
    - With command `echo "My beatiful text content" > file.txt`
- Great, but git doesn't know about our file - its like it "doesn't exist" for git
    - Files which are not known by git are called *untracked* files
        - Because git doesn't track them
    - If you use IDE like VS Code, you can see the file in *changes*
- So, how do we make git track our *file.txt*?
- Simply, we run `git add file.txt`
    - Now, you can see the file in the *staged*
- *Staged* changes are simply files which are ready to be commited
    - In other words ready to be made into a snapshot - into a "history version"

## Why is my file not staging now?
- This seems simple right? Let's try different thing - lets try modifying the file
- Add new line of "Updated text" in the *file.txt*
- When you save the file, something interesting happens
- If you look at the tab in VS Code, you can now see the *file.txt* in *changes* and *staging*
    - Why is that so, right?
- Thats because it works in snapshots
    - With git add file.txt, we have essentially created a local snapshot of the file
- If we edit the file, new *untracked* file is present again, or rather its part
- We can run the command again to add the current version of our file to the git
    - `git add file.txt`
- Now you should see our current file is in the *staged* again, hooray!

