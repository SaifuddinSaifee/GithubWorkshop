# Git Explainer

In this module, we will have a brief discussion on:
    - What is Git?
    - Why Git?
    - Some essential git concepts and commands

## Explaining git concepts

Git is a **version control system**... That's it!

But wait! what is a version control system?

To understand this better, let's take consider a simple scenario.

Say you have been developing a website using HTML, CSS, and JavaScript (or any of your preferred languages). You have been developing this website for a while now, and it turns out that the source code has inevitably grown to be very large, complex, and challenging to navigate.

One fine day, you made a wholesome change amount of change in the source code (maybe to add a new feature). Because these changes are deeply integrated into the source code, and because these changes are deeply integrated into the source code, **it will be challenging to revert back to those changes** (you can't <kbd>Ctrl + Z</kbd>/<kbd>Cmd + Z</kbd> for the rest of your life, can you?). Upon testing, you realized that due to this particular change in the source code, the entire application has lost its integrity and has become a nest of bugs and errors. *Not so fine day, it seems :(*

If only there was a way to go back and review your previous code and keep track of all the changes in your application's source code. A version control system (VCS) comes in handy here. **Git** is a well-known open-source version control system.

If only there was a way to go back and review your previous code and keep track of all the changes in your application's source code. A version control system (VCS) comes in handy here. **Git** is a well-known open-source version control system.

Version control systems (VCS) are software tools that assist software development teams in managing changes to source code over time. Version control software stores every change to the code in a special type of database. If a faulty change has been patched, the developers can go back in time and compare previous versions of the code to assist in resolving the issue while minimizing disruption to all team members.

### Git

Git is one of the most popular version control systems. Git is known in the industry because it's:
    - Free
    - Open Source
    - Fast
    - Scalable

GitHub is one such platform that leverages the functionalities of Git and makes it more efficient for collaborating and maintaining source code with other developers.

To start, [Install Git on your machine](https://git-scm.com/downloads). Here's documentation that helps you with [Installing Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

To check whether you have Git installed successfully, enter this command in your command line.

```bash
git --version
```

Output

```bash
git version 2.24.1
```

Traditionally operations with Git are performed using the command line of an Operating system. There are GUI tools that help you perform Git operations you decide to suit best to your application. Git also integrates with some of the most popular code editors, such as Visual Studio Code, Sublime and Atom.

For a better understanding of Git concepts, we will use the command line. In this module, we'll look at some basic and frequently used Git concepts such as:

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
  
  These logs and versions of your code are stored in a folder named ".git". You cannot see this folder as it is in a hidden state by default because **you are not supposed to tamper with the ".git" folder**.

Let's start with the hands-on!

To use the features of Git, we initialize a repository using the `git init` command. There are two simple methods to do so:

- **Method 1**: We create a new repository, and we create an empty folder that already has a .git sub-folder in it.

    ```bash
    git init LearnGit
    ```

    Output

    ```bash
    Initialized empty Git repository in D:/LearnGit/.git/
    ```

    We have created a new folder with the name "LearnGit" using the `git init {folder-name}` command. This LearnGit folder contains nothing but a .git folder. Generally, you use this method when you are about to start a new project from scratch.

    If you already have a folder containing the source code and other files, you may use the second method.

- **Method 2**: We can initialize the repository with an **existing** folder with Git. In cases where you already have a source code and want to leverage the features of Git in that folder. Let's say you have a folder named "MyProject", which contains an HTML file.

     1. Navigate to the target folder.

     ```bash
     cd MyProject
     ```

     2. Initialize this repository using `git init` command.

     ```bash
     git init
     ```

  > **IMPORTANT**: While initializing a repository for an existing folder **do not** specify the folder `git init {folder-name}`. Simply navigate inside the folder via the command line and type `git init` in the command line.

Voilà! You can now perform git operations in the folders you just initialized!

Including a `README.md` file in your repository is a good practice because it helps you and other developers understand the project.

#### Workflow — Modify, Stage, Commit

In this module, we will work in a repository named "MyProject". For inclusivity, we will not be using any specific programming language. Instead, we'll use text (.txt) files for Git operations.

Git operates in a way that stores versions of your source code every time you finalize a change in the code. When you commit your code, Git creates a compressed version of your entire project. Every code version will be referred to as a "commit".

#### 1. Modify

"Modify" refers to any change in any files in the repository. That include:

- Creating new files
- Editing files
- Removing files

So go ahead and create two new files named "file1.txt" and "file2.txt", Both containing the text "Hello World".

This is considered a modification as we are creating two files with some data.

#### 2. Stage

Now that you have added two files to the repository. Let's see what Git has to say about this!

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

As you can see, `file1.txt` and `file2.txt` are written in red, indicating they are "Untracked". It means these files have been created in the folder, but the git tool has not yet registered these changes in its system.

Stage basically mean you are just **intending** to introduce these changes in the code base.

Consider this: you want to buy a car. You've decided on a Chevrolet Cruze (**modify**). You inform your accountant, "Hey! I intend to purchase a new Chevrolet Cruze" (**stage**). The accountant is the Git in this scenario.

By staging, you inform Git to include these files in the most recent commit. Note that, according to Git, you have not yet added these files; you have simply informed Git that you **will be** adding these files.

To stage your changes, use the `add` command:

Method 1: Use this method to choose the files you want to stage.

```bash
git add file1.txt file2.txt
```

***or***

Method 2: This method is used to stage **all** the files in the folder.

```bash
git add .
```

Let's recheck the git status.

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

As you can see, you have no commits. But Git knows what you will commit as you have **staged** those files.

#### 3. Commit

You have finally purchased the Chevrolet Cruze! Let's inform the accountant.

In our case, you have finally decide to inform Git that you want to include file1.txt and file2.txt in the upcoming commit.

To commit your changes, type the command `git commit -m "{A short message about this particular commit or version}"`

```bash
git commit -m "Added two files in the project."
```

Output

```bash
[master (root-commit) c083325] Added two files in the project.
 2 files changed, 2 insertions(+)
 create mode 100644 file1.txt
 create mode 100644 file2.txt
```

In the output, we have a short summary of our latest changes.

2 files changed:

- file1.txt
- file2.txt

2 insertions(+):

- Hello World in file1.txt
- Hello World in file2.txt

> **NOTE**: Git only commits staged changes, i.e. to register changes to the Git, you must stage those changes first.

#### Implementation

Let's simplify and understand what we have done till now.

Git helps you keep a record of what's happening in the project.

- **Modify**: We added two files in our project with some text.
- **Stage**: We stage (inform Git) that we are planning to create a commit (or version) that records that "2 files have been added".
- **Commit**: We finally commit those changes. Here, Git takes a snapshot of your project and writes down what it looks like and how it compares with your previous commit (or version).

Assume you want to add a new feature to your application but are concerned that doing so will break your application. So, before you develop those features in the main source code, you duplicate your entire project code and modify this duplicate project to add your new feature. This is known as **branching**.

When you are done testing the feature in your duplicate application, you **merge** this duplication application code with the main (original) application so that your new feature is now a part of your original application.

So, you need branching for two reasons:

- Add a potentially risky feature (or code) to your project
- For better collaboration management

Let's see branching and merging in action for better understanding. We will stick our existing repository, "MyProject" which contains 2 text files:

To create a branch, type the command `git branch {branch-name}`

```bash
git branch new-feature
```

A new branch named "new-feature" has been created. You can create as many branches as you want for a repository.

To list all the branches in a repository, use the command `git branch`:

```bash
git branch
```

Output:

```bash
* master
  new-feature
```

Here, `master` is the main branch where our original code resides. The `new-feature` branch is the latest branch we have created. Both branches contain the exact same content (2 text files).

Any change in the "master" branch will not be reflected in the "new-feature" branch and vice-versa.

The master branch is highlighted in green along with an asterisk `*`. This indicates that you are currently in the master branch. We want to switch to our "new-feature" branch to work on this new feature.

Switching between branches is a fairly simple concept.

Type the command `git checkout {branch-name}`

```bash
git checkout new-feature
```

Output

```bash
Switched to branch 'new-feature'
```

You have now switched from `master` —> `new-feature`. To verify this switch, Type `git branch`

Output

```bash
  master
* new-feature
```

You can see the asterisk pointer `*` now points to the `new-feature` branch with a green highlight.

Let's create a new file in this branch and then merge it with the `new-feature` branch with our `master branch`. We will create a simple text file named "file3.txt" with the text "Learn Branching".

Type `git status` to check the situation here:

```bash
git status
```

Output

```bash
On branch new-feature
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        file3..txt

nothing added to commit but untracked files present (use "git add" to track)
```

The first line says **On branch new-feature**, there's an untracked called **file3.txt**. Let's stage and commit this file to our branch.

Stage:

```bash
git add .
```

You can check with `git status` again to see the staging area.

Commit:

```bash
git commit -m "file3.txt added"
```

Output

```bash
[new-feature 3816b5d] file3.txt added
 1 file changed, 1 insertion(+)
 create mode 100644 file3..txt
```

You have created, staged and modified a new file in the `new-feature` branch. Consider adding a new feature in your application just like this. Let's merge it with our `master` branch.

To merge your change into the `master` branch, we need to shift toward the master branch.

```bash
git checkout master
Switched to branch 'master'
```

> **TIP**: If you go to Windows' file explorer or type `ls` (in Linux). You will not find "file3.txt." This is because you are in the `master` branch, where file3.txt does not exist. But you can see file3.txt if you switch back to the `new-feature` branch (use `git checkout new-feature` to switch).

Now that you are in `master` branch let's perform the merge operation. Use the `git merge {branch-you-want-merge-from}`

```bash
git merge new-feature
```

Output

```bash
Updating c083325..3816b5d
Fast-forward
 file3..txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 file3..txt
```

The `new-feature` has successfully merged into your `master` branch. You can even see the file3.txt in your current folder/directory.

### Remote

So far, we've been doing all our tasks locally. This means that all the changes are committed to the local machine only. Other developers have no idea or access to our work.

But that does not serve one of the key reasons why Git (and VCS in general) exists:
collaboration

Other developers in the same team should be able to view and contribute to the project simultaneously without overwriting each other's work.

That's the role of remote repositories. So let's create one for our project.

![Create a GitHub repository](https://user-images.githubusercontent.com/18860009/177609231-54a98f66-0359-4f8f-8fba-b15e68389fba.png)
