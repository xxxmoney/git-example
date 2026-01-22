
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
    - With command `echo "My beatifull text content" > file.txt`
- Great, but git doesn't know about our file - its like it "doesn't exist" for git
    - Files which are not known by git are called *untracked* files
        - Because git doesn't track them
    - If you use IDE like VS Code, you can see the file in *changes*
- So, how do we make git track our *file.txt*?
- Simply, we run 
    - `git add file.txt`
    - Now, you can see the file in the *staged*
- It's also possible to run this on every file in the directory
    - `git add .`
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
- Also to make sure our example works as intended, run this command, more on branches later
    - `git branch -M master`
- And behold - we have successfully created our first saved version in history!

### Author identity unknown?
- Unless you've already set-up git on your PC (or someone has done it for you) you will see a message similar to this:
```
Author identity unknown

*** Please tell me who you are.

Run

  git config --global user.email "you@example.com"
  git config --global user.name "Your Name"

to set your account's default identity.
Omit --global to set the identity only in this repository.

fatal: unable to auto-detect email address (got 'user@pc.(none)')
```
- Thankfully, it tells you exactly what commands you need to run
    - `git config --global user.email "you@example.com"`
    - `git config --global user.name "Your Name"`
- Both the email and username can be whatever you want
    - **However!** Since we're going to deal with something called "remote repositories", it is strongly recommended you [sign up for github](https://github.com/signup) if you don't have an account already and use the same credentials as there
        - This will make your changes integrate much better into the website (but more on that later)
    
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
- Now, suppose we would like some "alias" for the 'linked list snake' we work on
    - Essentially, we would like to make new and new *commits* and always call the 'linked list snake' the same
- This is what *branches* are for - essentially, its just a nickname for a *commit*
- There is already an existing default *branch*, named "master" (or in some cases "main")
- This whole time, we have been using the "master" *branch*
- Lets imagine the "master" *branch* as a pointer
    - When we created a *commit*, we created a snapshot (history version) of our files
    - We have defined a new head for our 'linked list snake'
    - Git has automatically redefined our pointer of the "master" *branch*
        - Before we made the second *commit*, "master" was pointing to "Initial commit"
        - As we made the second commit, "master" is now pointing to "Update file.txt" 
        - You can also see the commits and "master" *branch* name in the VS Code - Source Control - Graph
- With this, when we commit, the "master" *branch* is always pointing to the head of the 'linked list snake'

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
- Firstly, let's talk about naming - usually, branches are named after what we do in said *branch*
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
        - Also git set the head of the 'linked list snake' of our branch to the latest commmit, so the "Add index.js file"

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

## Lets finish our branch
- As we are probably confused, lets look in which branch we are now
    - `git status`
    - Should be the "feature-add-script-file"
- Now, let's also add one more *commit* - lets change the weird message in the console.log
    - Let's change it to "Hello cruel world xd"
- Repeating the process again, *stage* the file and commit
    - `git add index.js`
    - `git commit -m "Update script with new message"`
- Great now our *branch* 'has two commits'
    - Or rather, we are pointing to the latest commit

## The MERGING, or not?
- Great, so now we have finished working on our feature
    - But, how do we "move" the changes from "feature-add-script-file" to "master"?
- Introducing, *merge*
- Imagine it as making sure one 'linked list snake' catches up to the other
    - Meaning we add some commits on top of it, basically
- So now, we would like our "master" branch to have the *commits* froms "feature-add-script-file" on top
- In this simple scenario, git can simply move the pointer
    - Instead of saying "master" points to *commit* "Update file.txt", it now points to "Update script with new message"
- Let's do it, firstly let's switch to "master" *branch*
    - `git switch master`
- Then we use the merge command
    - `git merge feature-add-script-file`
    - Wow, no way, we have the files - and more importantly our commits, 'in the' "master" *branch*
- What happened is simple - we have just moved pointers
    - "master" now points to the "Update script with new message" *commit*
    - This is also called *Fast-Forward Merge*
- Great, now our feature branch is not needed anymore, lets delete it
    - `git branch -d feature-add-script-file`
- Awesome, we have successfuly made our "master" 'GREAT AGAIN'

## The TRUE merge
- Great, but this is not ideal world, and changes happen all the time
- Let's introduce a peculiar scenario
    - Lets make a new *branch* - like feature-readme
        - `git switch -c feature-readme`
    - Lets make a README.md file in there, *stage* it and *commit* it
        - `echo "#Great heading for a great readme" > README.md`
        - `git add README.md`
        - `git commit -m "Add readme"`
    - Lets now move back to "master", lets make change to the file.txt and commit it
        - `git switch master`
        - `echo "Only this shall now be the content of text file" > file.txt`
        - `git add file.txt`
        - `git commit -m "Update text file content"`
- We have now a peculiar state
    - We have created two commits - "Add readme" and "Update text file content"
- Now let's try merging the "feature-readme" into our "master"
- Make sure you are in "master", check with `git status`
    - If not already, use `git switch master`
- Now lets merge it
    - `git merge feature-readme`
    - Oh no, what happened?
- Now the situation is not so easy
    - We cannot do the `Fast-Foward Merge`
        - That's because it's not possible to just move the pointer
            - We would loose the commit 'in master' if we moved the pointer to the commit in "feature-readme"
- We need to do proper merge
    - You should now see a 'weird' text
        - Focus on the first line "Merge branch 'feature-readme'
            - This is the name of the commit
        - Under this line, there are comments explaining this
        - For now, just write `:wq` and hit ENTER (command for VIM to save and close - WRITE, QUIT)
- Essentially, what we are doing now is making a new commit with 2 parents
    - So far, our commits only had 1 parent, we need to preserve both 'snakes parts', so the commit has 2 parents
- In the graph tab, you should now see a bit weirder history
    - So far, we had only 'linear' snake, and now, we can see two paths there
- We had to make sure we could preserve both *commits*
    - Both of those commits had the same parent - "Update script with new message"
    - And only way to preserve them both was to make a 'unifying' commit - the *merge commit*
- Essentially, we have tied the snake back together
- Also, let's remove the feature branch, as now we have it 'in master'
    - `git branch -d feature-readme`
- Side note - sometimes, the *merges* are not so easy, *conflicts* can happen, but on that some other time

## Remotes, what's that?
- Great, so now we have our master branch 'glorious yet again'
- But this is all fun and games, but what about the C O L L A B O R A T I O N?
- Introducing *remotes* - a way to synchronise your local *repository* with different - usually on server
    - This is basically just GitHub - it stores the .git folder on a server
- Let's try this on local scale first
- Let's go away from our *repository* for a bit 
    - `cd ..`
- Create new directory
    - `mkdir sample-repo-server`
- Go into the directory
    - `cd sample-repo-server`
- Initialise a bare *repository*
    - `git init --bare`
- Switch back to our repository
    - `cd ..`
    - `cd sample-repo`
- We have now esentially made our little GitHub locally, great right?
    - But the server repo is empty now - let's change it
- Firstly, we need to define the server *repository* as our remote
    - Remote meaning the server *repository* we will be synchronising with
- Add the *remote* - we define a name for it, typically "origin"
    - You can define the path as absolute or relative, I'll use relative in this example
    - `git remote add origin ../sample-repo-server`
- Great we have now successfully defined a *remote*


## But how to remote?
- We have defined our *remote*, great, but how do we make sure our local files are on the server now?
- Simply, lets *push* our changes on the server
    - `git push -u origin master`
        - With this command, we are pushing onto *remote* "origin" our local branch "master"
- Now several things have happened
    - Our git changes are now in the "sample-repo-server" folder
        - Not the literal files - basically, the .git folder is not 'same' as the one in the "sample-repo-server" folder
    - Git has created a new *branch* called origin/master
        - This branch is basically a local snapshot of server - on this later on
- Lets try making new commit and pushing it
    - Add new file named another_file.txt
        - `echo "Some text" > another_file.txt`
    - *Stage* it
        - `git add another_file.txt`
    - *Commit* it
        - `git commit -m "Add another text file"`
- Now, we need to make sure this commit is *pushed* onto server
    - `git push -u origin master`
- What that does now
    - We have one new commit, it takes this commit and adds it to the server *repository*, updating the "master" *branch* pointer there
    - Once this is confirmed, the local snapshot - "origin/master" is updated (the pointer changes)
- And so at this point, the local repository and remote are 'SAME GREAT AGAIN'

## Cloning the server repo
- What's amazing about git is that multiple people can work on it, have their local version of *repository*
- Let's simulate developer no. 2 - someone who *clones* the repository locally, then does some change
    - Go up the folders
        - `cd ..`
    - Create new folder
        - `mkdir sample-repo-02`
    - Go into that folder
        - `cd sample-repo-02`
- Now we have an empty folder, ready to be filled with the *repository*
- We can simply litreally *clone* the server *repository*
    - `git clone ../sample-repo-server .`
        - Command structure is `git clone [SERVER_PATH] [LOCAL_PATH]`
            - The dot means into current directory
- And viola - if we check the current directory, the "sample-repo-02"
    - `ls`
- We can see it HAS FILE! (and also the .git folder)
- Woah! So we have *cloned* it successfully
- This repository also has defined *remotes* as bonus, see
    - `git remote -v`

## Commiting and pushing from 02
- Now let's play a colleague which does some stuff in his local *repository*
    - `echo "export const quakeInvSqrt = n => ((b) => ((f, i) => (f[0] = n, i[0] = 0x5f3759df - (i[0] >> 1), f[0] * (1.5 - (0.5 * n * f[0] * f[0]))))(new Float32Array(b), new Int32Array(b)))(new ArrayBuffer(4));" > square.js`
    - `git add square.js`
    - `git commit -m "Fast inverse square root"`
- Great, now as a developer 02, we have *committed* the change into our local *repository*
- But it's not on the server yet, how do we do that? *PUSH*
    - `git push -u origin master`
- Great, now our changes as developer 02 are on the server

## How to get the lastest GOOD STUFF?
- Now let's go back onto our repo, 'how sweet home'
    - `cd ..`
    - `cd sample-repo`
- As we can see, we don't have the latest commit yet, we need to *fetch* it first
- Fetching is basically asking server for latest snapshot of the server
    - `git fetch`
- Well amazing, but we STILL DON'T have the file, why?
    - That's because the *fetch* updates the snapshots of the *branches*, so the "origin/master" *branch*
- If we want to have the changes in our "master", we need to merge it
- We can already do that, right?
    - `git merge origin/master`
- Woooow - now we have the changes - AMAZING! - but what just happened?
- Well, we have simply merged the snapshot into our "master"
    - And because its a simple *merge*, git used *Fast-Forward*
- Anywho, we have successfully played a role as developer 02, *cloned* the *repository*, made a change which we *pushed*, and then back at our original *repository*, we have *fetched* and *merged* the changes - GREAT!
- Side not - the `git fetch` and `git merge origin/master` have a shortcut command
    - `git pull`
        - You can also specify the *branch* and remote so `git pull origin master` for example
        - But if you want to *pull* just the snapshot and merge it, you can use just the `git pull` 

## Making the server REAL
- So far, we have used a local server - just a folder, let's step this up
- Firstly, setup an account on GitHub (https://github.com)
- We then create a new repository - let's name it same as our folder - sample-repo
    - Let's use the defaults
    - One of the important ones is the visibility - that's if the repository is visible to only you (or chosen ones) or everyone
- Once we have the repository set up, we can copy the link to the .git
    - For example `https://github.com/[USERNAME]/sample-repo.git`
- Now lets change our *remote* "origin" to this
    - `git remote set-url origin https://github.com/[USERNAME]/sample-repo.git`
- We can check if we set it up correctly
    - `git remote -v`
- Great, now we should have the connection set up, lets push our changes to GitHub
    - `git push -u origin master`
- Fantastic, now we have our *repository* on GitHub!
- We could now work similarly - our colleague could do a similar thing, push changes, we could *pull* (*fetch* and *merge*), etc
- Let's now try making a new *commit* and *pushing*
    - `rm square.js`
    - `git add .`
    - `git commit -m "Remove square root script"`
    - `git push -u origin master`
- We can check our GitHub *repository* now - we should see the new commit in there

## Pull Request
- This is all fun and games, but what about some rules and standards?
    - We might not want everyone so commit directly into out "master"
- Why? In bigger, production projects, etc - the "master" is the 'source of truth'
    - Meaning if only want *reviewed* files in there
- The process of the review is *Pull Request*, or *PR* shortly
- *Pull Request* is essentialy from Point of View of server
    - I as server am pulling someone's changes
- Usually the workflow is as follows
    - *Repository* has an established default *branch*, like "master" or "main"
    - We can *clone* this *repository*, make our own feature or fix *branch* and *push* said *branch*
        - But we usually can't *push* directly into "master" or "main"
    - As we push the *branch*, the Pull Request is usually initiated, let's try it
- Let's create new *branch*, make *commit* in it and *push* it
    - `git switch -c fix-script-message`
    - `echo "console.log('Hello world.');" > index.js`
    - `git add .`
    - `git commit -m "Fix script file"`
    - `echo "console.log('Hello hello.');" > index.js`
    - `git add .`
    - `git commit -m "Update fix script file"`
    - `git push -u origin fix-script-message`
- When you now visit your GitHub *repository* page, you should see a button "Compare & pull request", click it
- We will now see the *Pull Request* page
    - Now there should be "base: master <- compare: fix-script-message"
        - This just means - we will compare whats in "fix-script-message" we want to add to "master"
    - Also a title box
        - *Pull Request* can be named variously, it's good practice to name them with some convention
            - "Merge [FROM_BRANCH] into [INTO_BRANCH]"
            - So: "Merge fix-script-message to master" - let's name it this way
        - Once we have it named "Merge fix-script-message to master" hit CREATE PULL REQUEST
    - We should not wee a screen with information about the "Pull Request"
    - Take a look at the "commits" tab or "files changed" tab
    - Go back to the "conversation" tab
        - There people can write comments - recommandations etc
            - Comments can also be written for files in the "files changed" tab
    - Great, we might be now happy with the *Pull Request*, let's finish it
    - Click on "Merge pull request"
        - There is now the commit message - good practice is to have defined names, like the branch
            - So "Merge fix-script-message to master"
    - With this, the *Pull Request* is finished, we can remove the branch on the server with button "Delete branch"
- Now let's update our local *repository*
    - `git switch master`
    - `git branch -d fix-script-message`
    - `git pull`
- And WOW - we now have the *merged* *commit* from the *Pull Request* on our local *repository*, amazing!

