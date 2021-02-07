# Git Fundamentals

*This file serves as a somewhat written transcript of the presentation from the workshop/webinar. Some details may be missing, but the core components are here.*

In every software development role, even pushing in other roles now, you will see Git being utilised in some form, you might wonder why that is, and why you have likely seen people complain about it; however, I’d highly recommend looking past that and understanding just a little more of the Git fundamentals. The common adage for Git is along the lines of learn 4 or 5 basic commands and don’t understand what is going on, whilst I can understand this approach, I do not recommend it, as using commands without understanding what they do is a sure fire way to get yourself in some unwanted situations, as may happen with any type of command execution in this case.

## What is Git?
Git is a distributed version control system, there are others too, but Git by far the most widely used. If that sounds confusing to you then you are not alone. If split this up, it starts to make more sense, but we’ll also strip it back further as we go.

- Distributed – A system which is distributed will have different components running separate computers, communicating over a network. When these components interact, they achieve a common goal. In the case of Git, it is distributed, as opposed to centralised, because every user of the data that Git is looking at has can make changes locally, which are then saved to the server located elsewhere – this is typically done with a service like GitHub or GitLab.
- Version Control System – When you hear version control, you can think of it in simple terms as v1, v1.1 and so forth. Git is what enables you to track the version of the data it is working with, typically code, but it is not strict in this sense.

So, in simple terms, Git is a “content tracker” at its core. You set it to track several files and going forward it will detect changes which you must save, creating the next version, or revision, of the files which are being tracked.

## Why would I use Git?
Now, you might be curious as to why you would use Git. Rest assured, I thought the exact same thing when I was not using it; since then, it has saved me countless times.

Picture this, you’re working on a personal programming project, a web app that allows users rank their favourite characters from a popular game from 1 to 10. You want to quickly test a new idea for the layout of the application, but you don’t want it to be permanent, after all it is just a quick test. In this scenario, you are not going to use Git, can you imagine how you would go about this task? You might comment out some styling that you’ve made and apply the other idea you have, maybe you copy the current code into another separate file and make the changes you want, to then paste the old code back in. This quickly becomes a hassle and introduces the possibility of human error, imagine you accidentally saved the test style and now you are required to go back through the changes you made and undo everything to get it back to the way it was before.

In an alternate reality, you were using Git for this project and had your code backed up in a repository with the popular Git service GitHub. To quickly test your changes, you create a new **branch** and **checkout** that branch, you conduct your changes, **commit** them, and once finished you do not like them, now you simply switch back to your previous branch and delete the branch you created for the different styling you wanted. The work you had prior is brought back and nothing has changed. If you did like these changes, you can **merge** them into your prior work.

This is a single example of how Git can be incredibly powerful, but there are other ways that you will encounter when you begin to use it.

## Understanding Git
The first thing to remember is that GitHub, GitLab and any other service which interacts with the Git protocol is not Git itself, think of these as wrapper services that use Git to enable the sharing and backup of content to a remote server, there are other features too, such as enabling easy code reviews, but this is not the focus of this introduction. 

We mentioned a few different Git-specific terms in the previous section, we shall explore what these mean here:

- Commit – A core component of Git, this can be thought of as saving a snapshot of the current project which can be reverted to at any time. It creates a new “blob” of data in the commit history for someone to see.
- Branch – Another separate space in your project where you can conduct changes, these do not affect other branches unless you explicitly allow them to. This allows you to test feature or continue regular development flow before introducing the new changes into your code.
- Checkout – Think of this as “switching to”, if you checkout a branch, you switch to the latest snapshot of changes which have been committed onto it.
- Merge – Combining changes from one branch into another. This is as it sounds, you’re explicitly telling Git to apply the changes to another branch.

### Using Git
If we walk through a simple example of the workflow of Git, this helps cement the understanding of what you can do and why it is done.

Create a folder called `learning-git` and run the initialisation command for Git

    git init

After you have done this, you will create a local repository in the folder. You will notice this has created a `.git` folder too, this is where the configuration is held for your current repository, such as the remote service address you use once it is set and the commit history, alongside many others.

If you create a simple text file in there, such as `intro.txt` and place any text in there, maybe `"Git is great!"` would be a good start.

Now, if you run the command `git status` this will display the current state of the repository on your current branch, which will be `master`, showing you what has changed since the most recent commit - since we haven't made any commits yet, this file will be considered `untracked`.

Run the following commands to add the file and commit it

    git add intro.txt
    git commit -m "My first commit."

Here, you are using `git add <filename>` to *stage* this file, which means you are placing it ready to be committed. You are then committing it with the `git commit` command, the `-m` flag is to provide a message for the commit, this way you can provide it on the commandline without having to drop into a specific text editor; setting a message is useful for when you are reviewing the commit history, so you know what changes were made at that specific point in time.

Now lets say we wish to make a change that doesn't affect our file on the `master` branch until we explicitly allow it to. We will create a new branch using the command `git branch <branch_name>`, we will go for `git branch feature/my-new-idea`, this will create the branch for us. We can then switch to it with the `git checkout feature/my-new-idea` command; you can also short form this using the command below.

    git checkout -b feature/my-new-idea

What is happening here is that you will check out the branch, `-b` flag will create it if it does not already exist. In our case, it doesn't, so it will create the branch before we switch over.

If we edit the text file that we had prior, these changes are not going to be in the `master` branch until we allow them to be. We can quite easily prove this. Firstly, if you edit the text file to include another line that says `"Only in another branch!"`. If we then stage this and commit it using the commands
 
    git add intro.txt 
    git commit -m "Updates to my text file."

If you now quickly switch back to the `master` branch using `git checkout master` and view the file, you will notice that the line is no longer in there. If we then swap back to the other branch, it will return, this is done via `git checkout feature/my-new-idea`.

Now, you might be curious as to how we can get the changes from the `feature/my-new-idea` branch into `master`, this is done through *merging*. To merge we simply switch to the branch we want to pull our changes into and then execute an aptly named `git merge` command.

    git checkout master
    git merge feature/my-new-idea
`
Here we are switching to `master`, the branch we want our changes to be placed into, and then merging the commit we made in `feature/my-new-idea` into `master`.

