
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
    - With git add *file.txt*, we have essentially created a local snapshot of the file
- If we edit the file, new *untracked* file is present again, or rather its part
- We can run the command again to add the current version of our file to the git
    - `git add file.txt`
- Now you should see our current file is in the *staged* again, hooray!

## We have staged file, now what? COMMIT
- We could repeat this process over and over again, but here's the catch
    - We don't actually have any history - we just have the present *staged*
- To create a version in history, we create *commit*    
    -  Very simply commit is just *staging* which is saved with a name
- To create a new commit, we use this format (do NOT run this yet)
    - `git commit -m "[MESSSAGE]"`
    - The message should be short, meaningful one, usually in present time
    - For example "Add file" or "Update file"
    - For very first *commits*, it's very usual to name them "Initial commit"
- So let's do it now - let's turn our current *staged* into new *commit*
    - `git commit -m "Initial commit"`
- And behold - we have successfully created our first saved version in history!

## Lets try some restore
- Now lets suppose we update our file again
    - Lets try adding new line "Another update"
- The file should be now in *changes* - this change is NOT *tracked*
- Lets track it with `git add file.txt`
- Now, what if we want to undo our *staged* changes
- Lets simply remove the *staged*
    - `git restore --staged file.txt`
- Now we have those back in the *changes*
    - If we want to remove the *changes*, simply run `git restore file.txt`
- Notice if we do that, now our file is in the state of the last commit we made - nice, innit?

## Lets do more commits
- Commits work simply said as a "Linked list"
    - Meaning each commit has some parent (except the first one)
- Lets try updating our file and this time commiting it
    - Add new line with "Really an update" to the *file.txt*
    - We *stage* the changes with `git add file.txt`
    - Now, when we have *staged* changes, we can create a commit
    - `git commit -m "Update file.txt"`
- Amazing - now in the VS Code we should see the two commits
    - Our latest "Update file.txt" and its parent "Initial commit"

## Lets talk branches
- Great, now we have *commits*
- We know they are just snapshots of our files
    - A snapshot from some time with some name
- Now, suppose we would like some "alias" for the "linked list snake" we work on
    - Essentially, we would like to make new and new *commits* and always call the "linked list snake" the same
- This is what *branches* are for - essentially, its just a nickname for a *commit*
- There is already an existing default *branch*, named "master" (or in some cases "main")
- This whole time, we have been using the "master" *branch*
- Lets imagine the "master" *branch* as a pointer
    - When we created a *commit*, we created a snapshot (history version) of our files
    - We have defined a new head for our "linked list snake"
    - Git has automatically redefined our pointer of the "master" *branch*
        - Before we made the second *commit*, "master" was pointing to "Initial commit"
        - As we made the second commit, "master" is now pointing to "Update file.txt" 
        - You can also see the commits and "master" *branch* name in the VS Code - Source Control - Graph
- With this, when we commit, the "master" *branch* is always pointing to the head of the "linked list snake"

## Great, but what are branches for?
- Well, lets suppose we have a big project
    - And there are many feature, your work on feature 1 and suddenly, you would like to work on feature 2 and hop a quickly from feature to feature
- Well, with this, you can - you can have many *branches* where at each branch you do different work
    - You can have different commits on each branch - so the work is segregated
- Pretty neat, eh?

## Lets try branching
- Cool, now we know we have "master" *branch*, but, how do we know that?
- Introducting, `git status`
    - This command tells us about the current *branch*, etc, try it
- Firstly, let's talk about naming - usually, branches are named after what we do in said branhc
- Typically, we have two types of things we work on
    - feature - something new - like adding a form dialog, etc
    - fix - fixing bugs, like website not responding when clicking on submit in form
- Well, suppose we would like to create new *branch*, lets do it
- Either command `git checkout -b "[BRANCH_NAME]"` or newer `git switch -c "[BRANCH_NAME]"`
- Let's try making a *branch* named "feature-add-script-file"
    - `git switch -c "feature-add-script-file"`
- Well, not much changed, lets check the status
    `git status`
- And truly, you can see we are on different branch
- As of now, the "master" and "feature-add-script-file" are pointing to the same *commit* "Update file.txt"

## Commits in new branch
- Now we have our "feature-add-script-file" branch - from its name, we can guess what we will do now
- Lets try creating a new .js script file with some content, *staging* it and commiting it
    - Create an index.js file `echo "console.log('Nope, no hello for you, hmph')" > index.js`
    - *Stage* it: `git add index.js`
    - Commit the file, something like `git commit -m "Add index.js file"`
- Great, now we have our branch "feature-add-script-file" with a *commit* "Add index.js file"
    - What happened? We have created a new *commit*, said its parent is "Update file.txt"
        - Also git set the head of the "linked list snake" of our branch to the latest commmit, so the "Add index.js file"

## Lets travel back in time, sort of
- Well, this is great, but what if we now want to go back into our "master" - the one without the script file?
- Simple, run `git switch master`
    - Boom - now our "index.js" file is gone - NOOO?
        - Or is it really?
- Now, we have just switched to another *branch* - to "master"
    - So basically to the *commit* is just different now - it points to the "Update file.txt" now
- We can easily go back to the feature branch
    - `git switch feature-add-script-file`
    - Wooow, no way - the "index.js" is here?
- We have now changed the pointer again - this time, the pointer of *branch* "feature-add-script-file" points to commit "Add index.js file"
- So essentially, we have traveled back in time and back, woah!


