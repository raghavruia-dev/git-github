Reference: https://www.youtube.com/watch?v=apGV9Kg7ics&ab_channel=KunalKushwaha


********************************************
# SETUP YOUR ACCOUNT & AUTHENTICATE YOURSELF
********************************************

2 TYPES OF CONFIG: GLOBAL AND LOCAL
GLOBAL: IF ONLY ONE ACCOUNT USED BY YOU
LOCAL: IF MULTIPLE ACCOUNT FOR MULTIPLE REPOS

### REMOVE ANY OLD CREDENTIALS
git config --global --unset credential.helper

### SET USERNAME
git config --global user.name "raghavruia-dev"

### SET EMAIL ID
git config --global user.email "raghavruia.dev@gmail.com"

### If you're using HTTPS, you need to configure your username (optional) and use a credential helper to manage your credentials securely. This ensures you don't have to enter your credentials every time you interact with the remote repository.
git config --global credential.helper store

### For HTTPS authentication, you may also configure your GitHub username to associate with the repository URLs:
git config --global credential.https://github.com.username <your_username>

# INITIALISE A LOCAL REPO

git init

git add . 

git commit -m "Initial Commit"


*******************************************************
# CONNECT TO GIT HUB REPO
*******************************************************

### (1) CREATE A GITHUB REPOSITORY / OPEN AN EXISTING ONE
copy the HTTPS url e.g https://github.com/raghavruia-dev/git-github.git

### (2) USE COMMAND
git remote add origin <url>

where,
remote -> working with URL's
add -> adding a new URL 
origin -> name of the URL that is being added (by-default all repos present in personal accounts, are named as origin)

### GET URLs attached to the folder
git remote -v

*******************************************************
# USE GIT LOCALLY TO COMMIT CHANGES
*******************************************************

### CREATE EMPTY GIT REPOSITORY
git init (CREATE empty git rep)

### GET LIST OF UNTRACKED FILES
git status 

### STAGE MODIFIED FILES
#### ALL FILES IN A FOLDER
git add . 
#### SPECIFIC FILES FROM A FOLDER
git add names.txt

#### COMMIT A CHANGE (OR) PUSH CHANGES
git commit -m "<Your message here, -m here means message>"

### OPEN A FILE
vi <filename>

### SAVE THE FILE
save that file: Press Esc -> Type :x

### DISPLAY CONTENT OF A FILE
display contents of a file: cat <filename>

### UNSTAGE CHANGES 
git restore --staged <filename>

### SEE THE HISTORY OF CHANGES
git log

# NOTE
if by mistake you deleted/modified some files & you want to restore back to the last version or even 2 versions back

IN THAT CASE, 
you can't jump to any version from between you can just roll back to the previous version. if you want to go the version that is 2 times older than the last commit, in that case you will forgo the 2 commits in between. 
EG. 
COMMIT 2
COMMIT 1
COMMIT 0

You want to undo the COMMIT 2, you can do that.
Say for eg. you want to get back to COMMIT 0, in that case both the COMMIT 1 & COMMIT 2 will be ommited, and you will roll back to COMMIT 0

AS EACH COMMIT IS BUILT ON TOP OF EACH COMMIT SEQUENTIALLY

### REMOVE THE LAST COMMIT
Copy the commit hash value (of the previous commit of the latest commit you want to undo)

git reset <commit_hash_value>

LAST COMMIT WILL BE UNDO

# STASH

### DONT WANT TO COMMIT (AND) DONT WANT TO LOSE IT (go backstage, whenever wanted will bring you back)
First, stage it
git add .

Secondly, move it to stash
git stash

### IMPLEMENT STASH CHANGES (I.E BRING BACK FROM THE STASH TO MAIN STAGE)
git stash pop

### CLEAR THE STASH 
git stash clear

### PUSH THE CHANGES TO GITHUB
git push <url_name> <branch_name>

eg. git push origin master

where,
<url_name> = origin (as setup by us)
<branch_name> = master (by-default)

# NOTE

NEVER COMMIT TO THE MAIN/MASTER BRANCH WHILE YOU ARE WORKING ON A NEW FEATURE/BUG, AS THE USERS WILL GET AFFECTED

ALWAYS CREATE A SEPERATE BRANCH FOR IT

### CREATE NEW BRANCH 
git branch <branch_name>

### CHANGE THE POINTER OF  HEAD
git checkout <branch_name>

HEAD points to the ACTIVE BRANCH where commits will be made

### MERGE A BRANCH TO MAIN (IF YOU ARE REPO OWNER)
git merge <branch_to_be_merged>

### CLONING A REPO

git clone <url_of_repo>

add that repo to your remote urls

git remote add upstream <url_of_repo>

FORKED REPO'S IS KNOWN AS upstream as a convention

### PUSHING OF BRANCH

git push <url_name> <branch_to_be_pushed_name>

### ONE PULL REQUEST == ONE BRANCH

ALWAYS CREATE A NEW BRANCH FOR A NEW FEATURE OR BUG
AS IT WILL NOT ALLOW TO OPEN MORE THAN 1 PULL REQUEST FOR A SINGLE BRANCH

# FORCE PUSHING

The online repository contains a commit that our local repo doesn't, and as commits are interlinked force push is required.

### UPDATING FORK

When a PR is merged into the main, the fork you created in your repo will remain unchanged, inorder to update it based on the main branch

### STEP 1: change the head to main
git checkout <branch_name>

### fetch the changes in all branch
git fetch --all --prune

--all -> all the branches
--prune -> even the deleted ones

### STEP 2: reset the main branch of origin to the main branch of upstream
git reset --hard upstream/main

OR

git pull <upstream_name> <branch_name>

# SQUASH COMMITS or MERGE COMMITS

while making a new branch make sure your main branch is up to date make sure to follow git pull command

TRICK 

reset to the commit from where you want to marge the commits
those commits will be unstaged
and after that stage them and then commit them, all those commits will now be just 1 single commit

### Using rebase command for merging
git rebase -i 

-i -> interactive environment

now vi editor will open, 

it will have all the commit above of the hash value of commit we mentioned

now we can choose to merge the commit 
we will let the 1st commit to be there (where all other 3 commits will be merged) -> let it be prefixed with pick 
write: s in all the commit you want to merge

save the file

it will now prompt for writing a commit message
remove all the 4 commits you want to delete

write only 1 commit message

then git log -> all commits merged into 1 commit

# MERGE CONFLICTS

when you and someone else edits the same line of code, github gets confused about whose submission to consider, in that case merge conflicts happen.

you have to resolve the conflicts manually
