# _Gitting_ started with Git

Git is a powerful tool that enables organizations to handle distributed version control with ease. This is a fancy way of saying it's a tool that helps multiple people coordinate their changes to the same codebase across different computers.

Git comes in different forms: there is are command line interfaces and desktop apps like [GitHub Desktop](https://desktop.github.com/) that simplify the process of using Git. It's recommended you download GitHub Desktop now. There are also websites like [GitHub](https://github.com) and [GitLab](https://gitlab.com) that provide their own interfaces for reviewing and interacting with code. Currently, Charger Robotics uses GitHub for it's code.

### Resources for learning the basics of Git

These are some excellent resources for getting familiar with Git & GitHub:

* [Code Academy: Learn Git & GitHub](https://www.codecademy.com/learn/learn-git)
    * Interactive tutorial for learning Git & GitHub
* [GitHub: Using Git](https://docs.github.com/en/get-started/using-git)
    * Text heavy guide for learning about Git
* [GitHub: Introduction to GitHub](https://github.com/skills/introduction-to-github)
    * A brief guide about using GitHub

### Overview of some Git commands/concepts

After you're familiar with Git, check out this diagram:

![](/images/learn-git/git-diagram.png)

This is a great summary of Git's most commonly used commands. "Local" is going to be the copy of the repository on your machine. "Remote" is going to be the repository that lives in the cloud, on GitHub's servers.

##### Column Explanations

* Working directory
    * This is going to be your local files. Any changes made to a file is a change made to your working directory
* Staging area
    * Git allows for files to be "staged", meaning they are prepared to be pushed to GitHub servers. Any changes made to a local file will not automatically have the changes made to the copy in the staging area. Git will have it's own copy of the file from when it was staged that is different than the copy in the working directory
* Local repository
    * This is your local copy of the repository. Local commits are held here until pushed to GitHub
* Remote repository
    * This is the repository that lives on GitHub's servers. When a local commit is pushed to the remote, this updates the local repository with your local changes

##### Command Explanations

* `git add`
    * Moves files from your working directory to the staging area
* `git commit`
    * Bundles all files in the staging area into a commit to your local repository
* `git push`
    * Pushes changes from your local repository to the remote repository
* `git pull`
    * Pulls changes from the remote repository to your local repository
* `git checkout`
    * "Checks out" a new branch from your local repository
