# missing-semester-solutions
These are my solutions to the [MIT Missing Semester Course](https://missing.csail.mit.edu/). This course was offerred at MIT in January of 2020 and January of 2019 by [Anish Athalye](https://www.anishathalye.com/), [Jon Gjengset](https://thesquareplanet.com/), and [Jose Javier Gonzalez Ortiz](https://josejg.com/). The lectures, videos, and problems are all available at [https://missing.csail.mit.edu/](https://missing.csail.mit.edu/). 

The course consists of 10 lectures and covers the topics listed below. 

The motivation behind the course is to teach some of the tools you might be expected to know when pursuing a computer science degree, but there is no formal course that teaches them. Since this course was released to the public, many others have forked it and taught their own version of it. 



## [Course overview + the shell](https://missing.csail.mit.edu/2020/course-shell/)
## [Shell Tools and Scripting](https://missing.csail.mit.edu/2020/shell-tools/)
## [Editors(Vim)](https://missing.csail.mit.edu/2020/editors/)
## [Data Wrangling](https://missing.csail.mit.edu/2020/data-wrangling/)
## [Command-line Environment](https://missing.csail.mit.edu/2020/command-line/)
## [Version Control (Git)](https://missing.csail.mit.edu/2020/version-control/)
1. If you don't have any past experience with Git, either try reading the first
   couple chapters of [Pro Git](https://git-scm.com/book/en/v2) or go through a
   tutorial like <a href="https://learngitbranching.js.org/" target="_blank">Learn Git Branching</a>. As
   you're working through it, relate Git commands to the data model.
  
   
   
    **Solution:** In progress. 
    ### Learn Git Branching Tutorial
    #### Introduction Sequence
    Done
    #### Ramping Up
    Done
    #### Moving Work Around
    git revert undoes a commit by creating a new commit
    
    git reset actually alters the commit history. 
    
    Use git reset on a local repo, use git revert on a public repo
    
    git rebase -i will let you reorder the sequence of commits
    
    Use git cherry-pick if you want to pick one of more commits from another branch and add those to the branch you are currently working on.
    
    Done
    
    #### A Mixed Bag
    1 - Grabbing Just 1 Commit
    
    Done.
    
    2 - Juggling Commits
    
    //We need to change newImage even though that commit is way back in history
    
    git rebase -i C1 //reorder so the commit we want is on top
    
    git checkout newImage //get setup to make the change to newImage
    
    git commit --amend //make the change to newImage
    
    git checkout caption...
    
    git rebase -i C1 //reorder back to the original order
    
    git branch -f main HEAD~3 //move main to this updated part of the tree with the force -f flag
    
    Done.
    
    3 - Juggling Commits #2
    
    git cherry-pick will plop down a commit from anywhere in the tree onto HEAD
    
    My first attempt solved this in 14 commands. Shortest is 4. Need some practice on this one. 
 
    
    4 - Git Tags
    
    5 - Git Describe
    
    
     
    In progress.
    
    
    
    
   
    
1. Clone the [repository for the
class website](https://github.com/missing-semester/missing-semester).
    1. Explore the version history by visualizing it as a graph.
    1. Who was the last person to modify `README.md`? (Hint: use `git log` with
       an argument).
    1. What was the commit message associated with the last modification to the
       `collections:` line of `_config.yml`? (Hint: use `git blame` and `git
       show`).
1. One common mistake when learning Git is to commit large files that should
   not be managed by Git or adding sensitive information. Try adding a file to
   a repository, making some commits and then deleting that file from history
   (you may want to look at
   [this](https://help.github.com/articles/removing-sensitive-data-from-a-repository/)).
1. Clone some repository from GitHub, and modify one of its existing files.
   What happens when you do `git stash`? What do you see when running `git log
   --all --oneline`? Run `git stash pop` to undo what you did with `git stash`.
   In what scenario might this be useful?
1. Like many command line tools, Git provides a configuration file (or dotfile)
   called `~/.gitconfig`. Create an alias in `~/.gitconfig` so that when you
   run `git graph`, you get the output of `git log --all --graph --decorate
   --oneline`.
1. You can define global ignore patterns in `~/.gitignore_global` after running
   `git config --global core.excludesfile ~/.gitignore_global`. Do this, and
   set up your global gitignore file to ignore OS-specific or editor-specific
   temporary files, like `.DS_Store`.
1. Fork the [repository for the class
   website](https://github.com/missing-semester/missing-semester), find a typo
   or some other improvement you can make, and submit a pull request on GitHub.
   
    **Solution:** [PR #141](https://github.com/missing-semester/missing-semester/pull/141)
   


## [Debugging and Profiling](https://missing.csail.mit.edu/2020/debugging-profiling/)
## [Metaprogramming](https://missing.csail.mit.edu/2020/metaprogramming/)
## [Security and Cryptography](https://missing.csail.mit.edu/2020/security/)
## [Potpourri](https://missing.csail.mit.edu/2020/potpourri/)
## [Q&A](https://missing.csail.mit.edu/2020/qa/)
