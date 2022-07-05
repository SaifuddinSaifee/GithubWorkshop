# Git Explainer

In this module we will have a brief discussion on:
    - What is Git?
    - Why Git?
    - Some essential git concepts and commands

## Explaining git concepts

Git is a **version control system**... That's it!

But wait! what is a version control system?

To understand this better, let's take consider a simple scenario.

Say you have been developing a website using HTML, CSS, and JavaScript (or any of your preferred languages). You have been developing this website for a while now, and it turns out that the source code has inevitably grown to be very large, complex, and challenging to navigate.

One fine day, you made a wholesome change amount of change in the source code (maybe to add a new feature). Because these changes are deeply integrated into the source code, and because these changes are deeply integrated into the source code, **it will be extremely difficult to revert back to those changes** (you can't <kbd>Ctrl + Z</kbd>/<kbd>Cmd + Z</kbd> for the rest of your life, can you?). Upon testing, you realized that due to this particular change in the source code, the entire application has lost its integrity and has become a nest of bugs and errors. *Not so fine day, it seems :(*

If only there was a way to go back and review your previous code and keep track of all the changes in your application's source code. A version control system (VCS) comes in handy here. **Git** is a well-known open-source version control system.

If only there was a way to go back and review your previous code and keep track of all the changes in your application's source code. A version control system (VCS) comes in handy here. **Git** is a well-known open-source version control system.

Version control systems (VCS) are software tools that assist software development teams in managing changes to source code over time. Version control software stores every change to the code in a special type of database. If an faulty change has been patched, the developers can go back in time and compare previous versions of the code to assist in resolving the issue while minimizing disruption to all team members.

### Git

Git is one of the most popular version control systems. Git is known in the industry because it's:
    - Free
    - Open Source
    - Fast
    - Scalable

GitHub is one such platform that leverages the functionalities of Git and make it more efficient for collaborating maintaining source code with other developers.

To get started [Install Git on your machine](https://git-scm.com/downloads). Here's a documentation the helps you with [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

To check whether you have Git installed successfully, enter this command in your command line.

```bash
git --version
```

Output

```bash
git version 2.24.1
```

Traditionally operation with Git are performed using command Line of an Operating system. There are GUI tools that helps you perform Git operation, you decide suits the best to your application. Git also has an excellent integration with some of the most popular code editors such as Visual Studio Code, Sublime and Atom.

For better understanding of Git concepts we will use command line. In this module we'll look at some basic and frequently used Git concepts such as:

- repository
- Workflow
  - Modify
  - Stage
  - Commit
- remote
- branching
- merging
- merge conflicts

#### Repository

A repository in Git consists of two things:

- Your source code files (Just like a regular folder)
- Log of all the changes and branches of the code
  
  These logs and versions of your code are stored in a folder named ".git". You cannot see this folder as it is in hidden state by default because **you are not supposed to temper with the ".git" folder**.

Let's start with the hands-on!

To use the features of Git, we initialize a repository using the `git init` command. There are two simple methods to do so:

1. We create a new repository, we create an empty folder that already that has .git sub-folder in it.

    ```bash
    git init LearnGit
    ```

    Output

    ```bash
    Initialized empty Git repository in D:/LearnGit/.git/
    ```

    Here, we have created a new folder with the name "LearnGit" using the `git init {folder-name}` command. This LearnGit folder contains nothing but a .git folder. Generally, you use this method when you are about to start a new project from scratch.

    If you already have folder that contains the source code and other files, then you may use the second method.

2. We can initialize repository with an **existing** folder with Git. In cases where you already have a source code and you want leverage the features of Git in that folder.
  
  Let's say you have a folder named "MyProject" which contain an HTML file.

  1. Navigate to the target folder.

  ```bash
  cd MyProject
  ```

  2. Initialize this repository using `git init` command.

  ```bash
  git init
  ```

  > [!IMPORTANT]
  > While initializing a repository for an existing folder **do not** specify the folder `git init {folder-name}`, simply navigate inside the folder via command line and type `git init` in the command line.

Voilà! you can now perform git operation in the folders you just initialized!

It's a good practice to include a `README.md` file in your repository because it helps you and other developers understand the project.

#### Workflow — Modify, Stage, Commit

In this module, we will work in a repository named "MyProject". For the sake of inclusivity, we will not be using any specify programming language and instead we'll use text (.txt) files for Git operations.

The git operates in a way that in stores versions of your source code every time you finalize a change in the code. To be more specific every time you commit your code, git creates a new compressed version of your entire project. Every version of your code will be referred as a "commit".

##### 1. Modify

Modify refers any change in the any of the file in the repository. That include:

- Creating new files
- Editing files
- Removing files

So go ahead and create two new named "file1.txt" and "file2.txt", Both containing as simple text "Hello World".

This is considered as a modification as we are creating two files with some data in it.

##### 2. Stage

Now that you have added two files in the repository.  Let's see what Git has to say about this!

To check the situation of the repository, enter the command `git status`:

```bash
git status
```

Output

```bash
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        file1.txt
        file2.txt

nothing added to commit but untracked files present (use "git add" to track)
```

As you can see, `file1.txt` and `file2.txt` are written in red indicating they are "Untracked". It means that these files have been created in the folder, but the git tool has not yet registered these changes in its system.

Stage basically mean you are just **intending** to introduce these changes in the code base.

Consider this: you want to buy a car. You've decided on a Chevrolet Cruze (**modify**). You inform your accountant "Hey! I intend to purchase a new Chevrolet Cruze" (**stage**). The accountant is the git in this scenario.

By staging, you inform Git that you will include these files in the most recent commit. Take note that, according to git, you have not yet added these files; you have simply informed git that you **will be** adding these file.

To stage your changes use the `add` command:

Method 1: Use this method to specifically choose the files you want to stage.

```bash
git add file1.txt file2.txt
```

***or***

Method 2: Use this method to stage all the file in the folder.

```bash
git add .
```

Let's check the git status again.

```bash
git status
```

```bash
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   file1.txt
        new file:   file2.txt
```

As you can see, you have no commits till now. But Git knows what you will commit as you have **staged** those files.

##### 3. Commit

You have finally bought the Chevrolet Cruze! Let's inform the accountant.

That is you have finally decided to inform the git that you want to include file1.txt and file2.txt in the upcoming commit.

To commit your changes, type the command git commit

