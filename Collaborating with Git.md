*This document is for the hands-on part of the workshop series: Working with Command Line and Collaborating with Git*

## Slides
Please download or view slides following this link: 
https://docs.google.com/presentation/d/1QG-Ax-jETaHD0DL9wdzZcuMNdT7REQnuPCX2i9AKETI/edit?usp=sharing

**Outline:** 
![[Pasted image 20260207111333.png|500]]

## Hands-on 

**Important note:** Please follow [these instructions](https://docs.google.com/document/d/1hkGUhKHe2OECgra8lmHhSiOROLaz1kdz1wf4GdSvQ58/edit?usp=sharing) to **install Bash Shell and Git** ahead of time, especially if you are using a Windows computer. Make sure to [download the file (cookie_recipes.txt)](https://drive.google.com/file/d/1Xd2dbtuyB24Mt5xJQcJvf0GroRtnkNG_/view?usp=sharing) that we will be using during the workshop.

### Refresher: Manipulate files with Bash commands

Create a new directory called `cookbook` for the project in `Desktop`; enter that directory;  and check that you are in the right directory. 
```
$ mkdir ~/Desktop/cookbook
$ cd ~/Desktop/cookbook/
$ pwd
$ ls -a
```

Move downloaded file to the newly created directory 
```
$ mv ~/Downloads/cookie_recipes.txt .
$ ls
```

Open file to edit 
```
$ open cookie_recipes.txt
```
Or 
```
$ nano cookie_recipes.txt
```


### Creating Git repository 

Now, let's convert this project (the `cookbook` directory) into a git repository. 
Before we do that, let's make sure out git is set up properly. 

```
$ pwd
$ ls -a
$ git --version    # check that git is installed, and the version installed
```

```
$ git status 
"fatal: not a git repository (or any of the parent directories): .git"

$ git init
Initialized empty Git repository in /Users/huajinw/Desktop/cookbook/.git/
```
### What's happening? 

```
$ ls -a
$ ls -F .git
```
![[Pasted image 20260207224229.png|600]]
.git is a hidden folder that is the core of the Git project. It's the **local repository** that stores all the metadata, history, configuration, and objects (files and changes) for the project.

### Tracking changes 
```
$ git status
```
![[Pasted image 20260207220122.png|600]]
At this step git repository empty, meaning that it's not tracking / indexing any files. 
Now let's tell Git what files to keep track of, and commit the change. 
```
$ git add cookie_recipes.txt    # add files to the staging area
$ git status
```
![[Pasted image 20260207220739.png|400]]
```
$ git commit -m "add cookie_recipes file"
$ git status
```
![[Pasted image 20260207222419.png|400]]


### Examining changes

Now, let's make some changes to the `cookie_recipes.txt` file, and see how Git handles these changes. 

First, use nano or any other text editor to change sugar amount from 1 1/2 cups to 1 cup. Save changes. 
```
$ nano cookie_recipes.txt
$ cat cookie_recipes.txt
```

```
$ git status
$ git diff
```
`git diff` shows the differences between the current state of the file and the most recently saved version
![[Pasted image 20260209131507.png|600]]

```
$ git add .
$ git commit -m "reduce sugar content for the kids"
```

### Exploring history

```
$ git status
$ git log
```

`git log` lists all commits made to a repository in reverse chronological order.
![[Pasted image 20260209134338.png|600]]

![[Pasted image 20260209141254.png|300]]
```
$ git diff HEAD~1 cookie_recipes.txt

$ git diff e510d9 cookie_recipes.txt
```

You can use `checkout` to restore to a previous commit. 
```
$ git checkout HEAD~1 cookie_recipes.txt
$ cat cookie_recipes.txt
$ git status
```
![[Pasted image 20260209215111.png|600]]
#### Caution: Don’t Lose Your HEAD
Don't forget to include the file name when you checkout, otherwise Git would think that you want to move the HEAD position. 
```
$ git checkout HEAD~1  # Caution! this line leads to detached head.
```
To recover / reattached the head: 
```
$ git switch -
or 
$ git checkout main
```
![[Pasted image 20260209215644.png|600]]
