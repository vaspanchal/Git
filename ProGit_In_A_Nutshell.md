# Version Control
- A system that records the changes in a file or a set of multiple files over the time so that we can access the specific version later if required.
- It is used to manage the history of our code
- Version control system (VCS) is very useful if we want to keep every version of our software
- We can easily revert the changes made in our program using VCS
- Also, we can recover the lost data with its help

## Local Version Control Systems
- Copying the source code into another directory (or Time-stamped directory) to prevent further changes in the code.
    - **Pros** : It is simple to use
    - **Cons** : high chances of errors, since the programmer can accidently write the code in wrong directory or may forget the directory
- Simple Database based VCSs
    - RCS (Revision Control System) is an early implemention of VCS

    ![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTCr_1wUDDCAsOFh9Dr56sGd5uZf6yq17IYoQ&s)

## Centralized VCS
- Developed to fulfill the needs of collaboration of developers on other machines
- They have a single server that contains all the files and clients who can access/modify them
- Standard VC
- Examples : CVS (Concurrent Versions System), Peforce and Subversion
![](https://miro.medium.com/v2/resize:fit:906/1*Lxghb-YWFWfZBCZTjqgwxg.png)
- **Advantages**: 
    - Every developer is aware of projects's current status
    - Admins have control over who can do what
    - Easier to manage than Local VCSs
- **Disadavantages**:
    - Everything depends on a single server, which if goes down, nobody can collaborate at all
    - There maybe no proper backup for the code if the hard disk of server gets corrupted
    - While having entire history of the project at one place, there maybe the risk of losing everything

## Distributed VCS
- Developed to rectify the cons of CVSs
- In this system, client mirrors the entire repository of project including its history along with its latest snapshot
- upon mirroring, files gets distribute in clients, and thus having the backup of the project in multiple systems
- Examples : Git, Mercurial, Darcs, etc.  
![](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSL_lKwEM4ePnokrLjTdo1l15ENhe6C7pS6Iw&s)

# History of Git
- Git was developed when Bitkeeper DVCS ended its free services
- The linux community developed Git in 2005, having goals for the tool to be :
    - speed
    - simple design
    - support for non-liner dev. (parallel branches)
    - fully distributed
    - able to handle large projects efficiently

# Difference between Git and other VCSs
Git | Other VCSs
-|-
Changes in form of snapshots of entire project |Changes are file based
everytime you commit, the git stores the status of all the files at that moment in form of mini filesystem | only the file you make changes in gets snapshoted (known as delta-based VC)
Most operations need only local files and resources to operate, which makes it godly fast | Most operations require to access files from other machines, making the process slower
Git has integrity; it encrypts the information with SHA-1 hash before storing which makes the changes impossible without git knowing about it | Doesn't having this feature
It is hard to erase data in any way from git | you may lose the data more easily than git 


# Three Sections of A Git Project
![](https://static.packt-cdn.com/products/9781782168454/graphics/8454OS_01_4.jpg)

## Working Tree :
- contains files that are pulled from the local database in the git directory
- available to use and modify

## Staging Area :
- A file contained in git directory 
- stores information about what will go into your next commit
- technically known as  'index'

## Git Directory :
- stores metadata and object database for the project
- It is what copied when we *clone* a repo. from internet

# Basic workflow of Git :
1. You modify files in working tree
2. Then, selectively stage the files you want to be a part of next commit; goes in staging area
3. You do a commit to permanently store the snapshot in the git dir.

## Three States of a Git file :
Git has three main states in which a file can reside :
1. **Modified** : means you have changed the file, but not committed yet
2. **Staged** : means you have marked the modified file in its current stage to go for next commit snapshot
3. **Committed** : means the data is safely stored in your local database

> Git is a very stable and matured software that its updates make very less differences

![](https://git-scm.com/book/en/v2/images/areas.png
)
## CHECK VERSION OF GIT IN SHELL:
```
git --version
# OR
git version
```

# First-Time Git Setup
- There are a few things we need to setup to customize our git environment
- Git comes with a tool called ```git config``` that lets you setup these variable

## Setup Your Identity
- set username and email address same as that of GitHub
- It is important because every git commit uses this info.
```
git config --global user.name "userName"
git config --global user.email example@xyz.com
```
- you need to do this only once provided you pass ```--global``` option, because on using this, git will always use that info for everything
- If you want to override the information for specifcic projects, run the command without ```--global``` option in that project. i.e.,
    ```
    git config <command option>
    ```

## Setup Your Text Editor
- we can setup a default text editor that will be used when Git needs you to type a message
    ```
    git config --global core.editor "editor_path"
    ```
- Popular text editor for Git : Vim, Emacs and Notepad++

## Setup Your Default Branch Name
- By default, Git will create a branch called *master* on creating a new repo with ```git init```
- To set custom default branch name :
    ```
    git config --global init.defaultBranch custom_name
    ```

## Check Configuration Settings
- To get all configuration settings :
    ```
    git config --list
    ```
to get a specific key's(config. variable) value, ```use git config <key>```
- example :
    ```
    git config user.name
    >> userName
    ```
## Getting Help
- If you need help while using Git, there are three equivalent ways to get the manual page (manpage) help for any of the Git commands:
    ```
    git help <command_name>
    git <command_name> --help
    man git -<command_name>
    ```
- Example :
    ```
    git help config
    ```
- These commands even work offline
- To get more concise help, use ```-h```
    ```
    git <command_name> -h
    ```

# Git Basics
Consists of :
- configure and initialize a repository
- begin and stop tracking files
-  stage and commit changes

Its the majority of work we generally do with Git
## Getting A Git Repository
- There are two ways to obtain a git repo :
    1. Turn a local directory into git directory/repository
    2. *clone* an existing repo from internet

### 1. **Turn a local directory into git directory/repository** :
Go to the empty project directory, which is not under version control in terminal, and type :
```
git init
```
- upon doing this, a new subdir. will create with name ```.git``` that conatins all necessary repo files

for version controlling existing files, first track those file using ```git add``` and then commit using ```git commit```
```
git add <files>
git add LICENSE
git commit -m "Initial project verison"
```
- `git  add` puts the modified files into staging area, ready to commit
- `-m` is for message(followed by it) while committing 

### 2. ***clone* an existing repo from internet** :
To clone an existing repository from the internet, use command : `git clone <url>`
```
git clone https://github.com/libgit2/libgit2
```
- That creates a directory named libgit2, initializes a .git directory inside it.

If you want to clone the repository into a directory named something  else, use command : `git clone <url> new_name`
```
git clone https://github.com/libgit2/libgit2 mylibgit
```
## Recording Changes to the Repository
There are two states for a file in a working tree :

**1. Tracked** : files that were in the last snapshot, as well as any newly staged files.
- Unmodified files
- modified files
- staged files  
    
**2. Untracked** : Every file other than *tracked* in working tree.

![](https:# git-scm.com/book/en/v2/images/lifecycle.png)

- ### Checking the Status of Your Files
    To determine which files are in which state, use `git status` command
    ```
    git status

    #  returns something like this, if newly cloned repo:
    On branch master 
    Your branch is up-to-date with 'origin/master'. 
    nothing to commit, working tree clean
    ```
    - It means there are no *untracked* or *modified* files in the directory  

- ### Tracking/Staging Files (new/modifed)
    use the command `git add` to begin tracking *untracked* or staging *modified* files
    ```
    git add <files>
    ```
- ### Short Status
    While the `git status` output is pretty comprehensive, it’s also quite wordy. To get a more compact status, use `git status -s` command
    ```
     git status -s 
    ```
- ### Ignoring Files
    File/s that you want git to **ignore** (git will not modify them or show them as untracked), Use `.gitignore ` command following file name
    ```
    <file/dir._name> .gitignore 
        
    #  returns 
    *.[oa] 
    *~
    ```
    - The first line tells Git to ignore any files ending in **“.o”** or **“.a”*** — *object* and *archive* files
    - The second line tells Git to ignore all files whose names end with a tilde **(~)** : it means temporary files in text editors like *emacs*

    **The rules for the patterns you can put in the .gitignore file:**
     - Blank lines or lines starting with #
     - Standard glob patterns work, and will be applied recursively throughout the entire working tree. 
     - You can start patterns with a forward slash (/) to avoid recursivity. 
     - You can end patterns with a forward slash (/) to specify a directory. 
     - You can negate a pattern by starting it with an exclamation point (!).    


- ### Viewing Your Staged and Unstaged Changes  

    - To see what you’ve changed but not yet staged, type `git diff` 

        ```
        git diff 
        ```
    - To see what you’ve staged for next commit, use `git diff --staged`
        ```
        git diff --staged
        #  OR
       git diff --cached
        ```
- ### Committing Your Changes
    ```
    git commit
    #  OR 
    git commit -m "<message>"
    ```

- ### Skipping the Staging Area
    Adding `-a` option to `git commit` command makes Git automatically stage every file that is already tracked before doing the commit, letting you skip the ` git add` part
    ```
    git commit -a -m "<message>"
    ```

- ### Removing Files
    To remove a file from Git, use ` git rm <filename>`
    ```
    git status
    #  checks the current status of tracked files before removing a file

     git rm EXAMPLE.md
    #  removes EXAMPLE.md from tracked files
    ```
- ### Moving Files  
    - Git doesn’t explicitly track file movement  

    -  If you rename a file in Git, no metadata is stored in Git that tells it you renamed the file.  


    If you want to rename a file in Git, use:
    ```
    git mv file_from file_to
    ```
    - `mv` is move command for renaming files in git
    - `file_from` : current file name
    - `file_to` : new file name

## Viewing the Commit History
To see the entire commit history, use `git log` command
```
git log
#  returns entire commit history
```
## Undoing Things
- ### Undoing commit
    ```
    git commit --amend
    ```
    One of the common undos takes place when you commit too early and possibly forget to add some files, or you mess up your commit message
- ### Unstaging a Staged File
    ```
    git reset <filename>
    # git doesn't use it anymore
    ```
    ```
    git restore --staged <filename>
    # Introduced in Git version 2.23.0 
    ```
- ### Unmodifying a Modified File
    Undoing the changes made in a file  

    ```
    git checkout -- <filename>
    ```
    ```
    git restore <file>
    ```



