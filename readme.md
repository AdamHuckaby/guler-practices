# guler-practices
Best practices and version control basics for team programming in Prof Guler's Lab.

## Git and GitHub.com

Git is a version control system. It enables teams of developers to work simultaneously on the same project without stepping on each other's feet too much. Multiple developers can work on separate parts of a project with ease and integrate their work easily. Multiple developers can work on the same part of a project simultaneously, and Git will do its best to help them *merge* their changes into an improved project. Version control is also *very* safe, because every update to the codebase is saved in case of accidental corruption.

Git can be downloaded on a client's computer to interface with a Git sever. Git servers can be public or private, and they are pretty easy to set up.

GitHub.com is a popular service for creating and managing Git repositories on a centralized and ubiquitous Git server. Users can make public (i.e. open-source) repositories for free, or subscribe for $10+/month to create private repositories that function like a traditional Git server.

GitHub is really useful for teaming because just about every developer has a GitHub account and some basic Git skills. We will introduce Git and GitHub here to get your lab started with teamwork and version control

## Downloading and Installing Git

Git is very common and easy to find.

### Linux

Check with your package management software.

```
# Ubuntu
sudo apt-get install git

# CentOS/RHEL
sudo yum install git

# Other
sudo <your-package-manager> install git
```

### MacOS

Use this link to download the installer and walk through with default settings: http://git-scm.com/download/mac

This version is the official MacOS distribution from `git-scm.com`, which is the official maintainer of Git.

### Windows

I suggest this version: https://git-for-windows.github.io/

This is a souped-up version from the same team that runs `github.com`. This will install the Git GUI and the Git BASH programs to your computer. Windows users will use Git BASH to follow along with the examples here as though they were on a UNIX machine. Even for Windows wizards, I recommend Git BASH over any alternative.

When using Git BASH, many Linux commands (as well as `git`) will be made available via a MinGW terminal.




## Setting Up GitHub.com

Create an account in GitHub.com. Then, create a new repository. Name the repo, `my-fresh-new-repo`.

You may be prompted to create a `README.md` file. We will discuss markdown files in a later section. Go ahead and say "yes" to this.


## Using Git to Manage Repositories

This section will discuss various command you will use to manage repos on GitHub.com using Git commands from your system's terminal (or Git BASH for Windows).

### Cloning a Repository

Cloning is similar to downloading, with one exception. When you clone a repository, your system will place hidden files in the download location that enable you to interact with the repository via Git. It is possible to create a repository directly in Git, but, since we have already created one in GitHub, we will clone it.

To clone a repository, navigate to the location you would like to download it, then use `git clone` on the Git endpoint.

```
cd ~/Desktop
git clone https://github.com/<your-username>/my-fresh-new-repo
```

To clone a repository from another user, you must insert use their username. Simply copy the URL from the repository's GitHub.com page.

```
# for example...
git clone https://github.com/chrisconlan/guler-ev-vision
```


### Modifying a Cloned Repository

Go ahead and do whatever you like to the cloned repository. It can be moved around your computer without consequence. Any change you make to it will be saved later as long as you do not mess with the hidden `.git` folder sitting in the root level of the repo. Git does not saved or track the changed to the repository until you tell it to. Most often, you will add files, commit them to the repo, then push those changes to GitHub.com.


### Saving Changes (Locally and Remotely)

Your version of the repository is your local copy. You can save your changes locally without saving them remotely. You can manipulate which changes are saved and which are ignored. You can choose to respect both additions and deletions. Most often, you will use a simple set of 3 commands to save everything and push it up to GitHub.com. Sometimes, but not often, you will exercise finer control over the process.

Saving and pushing, a good default recipe:
```
# Navigate to your local repo
cd ~/Desktop/my-fresh-new-repo

# Add all changes while respecting deletions and moves
git add -A .

# Commit changes to your local repo
git commit -m "Always put a short but descriptive message"

# Push the changes to GitHub.com
git push origin master
```

We can substitute out some commands for different variations to achieve different results.

+ To add all files without respecting deletions and moves, simply use `git add .`. This method may be preferable to veterans who wish to tell Git about their deletions and moves manually using `git mv` and `git rm`.

+ To only add changes to a specific file, use `git add my-file.md`, or any other UNIX-like file command like `git add this-one-repo/*.py`. 

+ To push to a different branch, use `git push origin my-other-branch`. To Git, `master` is a branch (or version) of the "source history tree". We can manually create new branches if we want to make new or experimental changes to the repo without affecting the master branch.

+ To only save locally, simply do not run `git push`. If you do this, your team will not be able to pull your changes down from GitHub.com.


### Downloading Changes

In the language of Git, when someone else modifies a repository, we *pull* and *merge* those changes to our repository. If you have not modified anything that your team has modified, you will simply pull their changes and your repository will be overwritten. If you and your team have made changes to the same files and your local repo differs from the remote repo, we will have to manually reconcile those differences. This is usually messy, so we strive to avoid this by carefully organizing our tasks and projects.

Pulling changes to your local repo:
```
# Navigate to your local repo
cd ~/Desktop/my-fresh-new-repo

# Pull the changes to GitHub.com
git pull origin master
```


## Git and GitHub.com Quirks and Pointers


### File Size

Git and GitHub.com are primarily meant to store text files. Text files are really small. 

When we deal with large data like pictures and DNA, we will rarely be able to store them all on GitHub without using a workaround. Oftentimes, it is sufficient for all participants to simply store a local copy of the data, especially if neither party plans to modify it. Some workarounds are listed below.

+ Give all team members a local copy of the data. Make sure everyone knows not to push the data to GitHub.com. Simple and efficient when possible.

+ Use Git LFS. This stands for Git Light Filesystem, and requires a GitHub.com data plan that is about $25/month per 10Gb. This allows Git to store and manage large files via pointers to local to remote filesystems accessible by everyone using the repo. Oftentimes, Git LFS is set up with Amazon S3 Buckets, and each picture file is replaced with a download link to the individual file. This method is elegant, but requires some backend setup. It is worth it when the files exceed 100Gb total and you have a lot of remote team members.

+ Store the files in a shared Dropbox folder and have every team member download the Dropbox Daemon. This is simple, effective, and way cheaper than Git LFS. Dropbox data costs about $10/month per Tb. Highly recommended. It is not as safe as Git LFS, because any user can accidentally delete the database.


### Public vs. Private Repositories

New users are often concerned about the public nature of free GitHub.com repos. When using open-source dependencies with academic projects, as we generally do, this is not very big concern, because the bulk of the computing muscle is already open-source. 

Public repositories are a great way to attract positive attention and collaboration to your project, look great to potential employers, and encourage participation in the open-source communities that build the software we depend on daily.

GitHub.com has private repositories available for $10/month for 10 private repositories. I recommend this if you would like to increase your data limits on repositories as well.


### `.gitignore` Files

This is a simple text file that specifies which files will be ignored by Git and not pushed or committed. It can be stored anywhere in the repository, but it is typically best to have a single `.gitignore` in the root of your repository.

This file has many uses. For example, IDEs will often store project data and settings data as hidden files. We don't want to push those to GitHub or share them with our peers, so we add them to the `.gitignore`. Additionally, Python will compile scripts and store them on your file system. These are stored as binary data, and are therefore unreadable by Git. We will filter those out as well. Lastly, R will store session data very lazily on your computer, so I always make sure to put `.Rhistory` in the `.gitignore`.

My default `.gitignore` file:
```
**/__pycache__/*
**/*.pyc
**/*.Rhistory
**/*.project
**/*.pydevproject
**/.settings/*
**/.metadata/*
RemoteSystemsTempFiles/*
```

A few pointers on `.gitignore`:

+ Use normal file UNIX-like file references to specify which files to exclude.
+ Use `**/` to specify any file in any directory, multi-level.
+ To remove entire directories, remove their contents like so `directory_to_remove/*`.
+ `.gitignore` files can be stored anywhere and will operate using relative filepaths based on their location in the directory.


### Markdown and readme Files

Any file in markdown format and ending in `.md` or `.MD` can be easily rendered by GitHub.com. Users are encouraged to use this format for easy communication and documentation.

Any file named `readme.md` on GitHub.com will be automatically rendered when visiting the directory on GitHub.com.

