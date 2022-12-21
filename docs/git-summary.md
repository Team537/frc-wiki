# Git Summary

Git is an incredibly powerful tool and allows an organization like Charger Robotics to organize and share code in a well-mannered way that promotes cooperation and collaboration. There are 2 ways to use git. You can install git directly and use Vscode’s inbuilt integration with git which is highly efficient but doesn’t have an intuitive interface. You can also use Github Desktop, which also requires you to download git. Here you can easily view and manage what code you are sending to what branch and it is overall easier for someone to grasp the idea of git and how it works.

#### Github Desktop Interface and Features

Github and by proxy git have many features and they are very useful. The basis of git is the idea of a repository containing branches and “pulling” code from them, altering the code and then “pushing” it up to merge with the branch that the code was initially taken from. This is usually done by submitting a “pull request” which allows you to take the code from the branch. Then once the edits are made, you commit the code to snapshot the current changes. Then you submit a “push request” which then allows you to send the code up and merge with the branch. You can clone branches which allows you to have separate versions of the code specifically for testing certain subsystems like an experimental auto with the capability to destroy infrastructure already written. If this is done on a “master branch”, this can result in tragedy and is the reason why we make separate branches for testing. The structure usually revolves with a master branch and then a testing branch which then splits into individual branches for each subsystem and auto. Once each subsystem’s code is completed and safe to merge, rendering the branch dedicated to that subsystem useless, you can merge the branches into the testing branch to consolidate all the code. After checking it over another time, you can merge the entire branch onto the master branch which is what will be used at competition. Below is the interface of Github Desktop

![](./images/git-summary/git-summary01.png)

As seen here, you can see the repository in the top left corner along with the current branch to the right side of it with the option to fetch origin, which is basically pulling code down.You can see that there are no changed files here but if there were, they would show up there. In the bottom right corner, you can see the option to commit which is darkened because there are now changes to commit. Above that you can see stashed changes which are changes you don’t want to push but also don’t want to lose when you pull down. You can change the current branch by clicking on the current branch which brings up a menu. When you edit code, your changes will show up as shown below.

![](/images/git-summary/git-summary02.png)

You will be shown an interface showing the original version and what has been changed. You can choose to commit but you must add a description first. Once you commit you should be able to see it when you click on History.

![](/images/git-summary/git-summary03.png)

To push the code, click on the button that is next to the Current Branch. Once you do this, you should be good and the merge should show up in the history.

Something important for git is the idea of having a code to abide by when pushing and pulling code. This is important because if something a branch is pulled when there are uncommitted changes, they will be erased. Similarly, if code is deleted and pushed, it is erased on the branch you took it from which is even worse. So to avoid this, always remember to show someone your code before pushing it physically or through a request system in which pull and push requests are sent to  certain members that greenlight merges. You should also always pull before pushing changes up to merge as this makes sure you are integrating as much code as possible. Also remember to stash unsaved code before pulling down and then unstashed to layer and foresee any conflicts.
