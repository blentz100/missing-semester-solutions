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
  
   
      ### Learn Git Branching Tutorial
      #### Introduction Sequence - A nicely paced introduction to the majority of git commands
    
      1. Introduction to Git Commits
    
            Git commits are lightweight snapshots of a project you are working on, and switching between them is fast. 

            Each time we do a ```git commit``` we create a new snapshot that is tied to a parent commit. 

            Make two commits to complete this level.

            Solution:

            ```
            git commit
            git commit
            ```
            
    
      2. Branching in Git

            Branches are pointers to commits. "Branch early and branch often." A branch essentially says "I want to include the work of this commit and all parent commits.

         Make a new branch called bugFix and switch to that branch.

         Solution 1:

         ```
         git branch bugFix
         git checkout bugFix
         ```

         Solution 2:

         ```
         git checkout -b bugFix
         ```

      4. Merging in Git

         ```git merge``` creates a special commit that has two unique parents. This allows us to combine the work from two branches into one commit. 

         Make a new branch called bugFix
         
         Checkout the bugFix branch with git checkout bugFix
         
         Commit once
         
         Go back to main with git checkout
         
         Commit another time
         
         Merge the branch bugFix into main with git merge
         
         Solution:

         ```
         git branch bugFix
         git checkout bugFix
         git commit
         git checkout main
         git commit
         git merge bugFix
         ```

      6. Rebase Introduction

         Rebasing is a second way of combining work. It takes a set of commits, copies, and then plops them down somewhere else. The commit log / history of a repo will be alot cleaner if only rebasing is allowed. 

         Checkout a new branch named bugFix

         Commit once

         Go back to main and commit again

         Check out bugFix again and rebase onto main

         Solution:

            ```
            git branch bugFix
            git checkout bugFix
            git commit
            git checkout main
            git commit
            git checkout bugFix
            git rebase main
            ```

    
    #### Ramping Up - The next serving of 100% git awesomes-ness. Hope you're hungry
    
      1. Detach yo' HEAD

         HEAD is the symbolic name for the currently checked out commit. HEAD (almost) always points to the most recent commit which is reflected in the working tree. Normally HEAD points to a branch name, like bugFix. Detaching HEAD just means attaching it to a commit instead of a branch. 


         This 7 minute video has some good supplemental info on HEAD. https://www.youtube.com/watch?v=ZaI1co-rt9I
         
         ```git show HEAD``` will show you where the HEAD is currently pointed. Detached HEAD just means HEAD does not currently point to the most recent commit. 
         
         To complete this level, let's detach HEAD from bugFix and attach it to the commit instead. Specify this commit by its hash. The hash for each commit is displayed on the circle that represents the commit.
         
         Solution:
         
         ```
         git checkout C4
         ```

      2. Relative Refs (^)

         ```git log``` is what we will use in the real world to see what our commit tree looks like. Relative refs make it easier to move up or down a relative number of times in the commit tree. ```^``` moves up one level in the commit tree and ```~<num>``` moves upwards the number of times specified.
         
         
         To complete this level, check out the parent commit of bugFix. This will detach HEAD.

         You can specify the hash if you want, but try using relative refs instead!
         
         Solution 1: (relative ref)
         
         ```
         git checkout bugFix^
         ```
         
         Solution 2: (relative ref)
         
         ```
         git checkout bugFix~1
         ```
         
         Solution 3: (relative ref)
         
         ```
         git checkout C4^
         ```
         
         Solution 4: (direct hash)
         
         ```
         git checkout C3
         ```
         

      3. Relative Refs #2 (^)

         A common use of relative refs is to move branches around You can directly reassign a branch to a commit with the -f option: ```git branch -f main HEAD~3``` will force the main branch to 3 parents behind the HEAD.
         
         To complete this level, move HEAD, main, and bugFix to their goal destinations shown
         
         Solution:
         
         ```
         git checkout HEAD^
         git branch -f main C6
         git branch -f bugFix HEAD^
         ```
     
      4. Reversing Changes in Git
    
         There are two primary ways to undo changes in git. ```git reset```and ```git revert```
         
         Found a wording issue in this section and ended up submitting a PR for it. https://github.com/pcottle/learnGitBranching/pull/857
         
         ```git reset``` reverses a change by moving a branch backwards in time as if the commit never happened. Open question - what happens to the commit that got erased? Will it still show up if you run git log? Answer: It does not show up in git log anymore, but it seems to still exist, you can still check it out and it comes back to life.  This method works find if you are just working locally, but not so good if you are collaborating with others using a remote repo. 

         ```git revert``` solves that problem. This allows us to reverse changes and share it with others. 
         
         To complete this level, reverse the most recent commit on both local and pushed. You will revert two commits total (one per branch).

         Keep in mind that pushed is a remote branch and local is a local branch -- that should help you choose your methods.
         
         Solution:
         
         ```
         git reset HEAD^
         git checkout pushed
         git revert pushed
         ```

         
    #### Moving Work Around - "Git" comfortable with modifying the source tree :P

    
      1. Cherry-pick Intro

            Use git cherry-pick if you want to pick one of more commits from another branch and add those to the branch you are currently working on.

            git revert undoes a commit by creating a new commit

            git reset actually alters the commit history. 

            Use git reset on a local repo, use git revert on a public repo


      2. Interactive Rebase Intro
      
            git rebase -i will let you reorder the sequence of commits

            Done
    
 
    #### A Mixed Bag - A mixed bag of Git techniques, tricks, and tips
    
      1. Grabbing Just 1 Commit
    
          Let's say you are debugging a problem, you go back and add some print debug statements and print statements. Each one of those has their own commit now. Now you solve the problem and you just want your bugFix commit back into the main branch without bringing along your debug commits. That's the use case for this problem. Two potential solutions are suggested: ```git rebase -i``` or ```git cherry-pick```. 

          Solution using cherry-pick

          ```console
          git checkout main
          git cherry-pick bugFix
          ```

          Solution using git rebase -i 
          ```console
          git rebase -i c1 // delete commits c2 and c3
          git branch -f c4 main'
          ```
 
    
      2. Juggling Commits
    
          //We need to change newImage even though that commit is way back in history

          git rebase -i C1 //reorder so the commit we want is on top

          git checkout newImage //get setup to make the change to newImage

          git commit --amend //make the change to newImage

          git checkout caption...

          git rebase -i C1 //reorder back to the original order

          git branch -f main HEAD~3 //move main to this updated part of the tree with the force -f flag
          
      3. Juggling Commits #2
    
            git cherry-pick will plop down a commit from anywhere in the tree onto HEAD

            My first attempt solved this in 14 commands. Shortest is 4. Need some practice on this one. 
 
    
      4.  Git Tags

      5.  Git Describe
    
    
     
    In progress.
    
    #### Advanced Topics - For the Truly Brave!
    1. Rebasing over 9000 times
    2. Multiple parents
    3. Branch spaghetti
    
    
   
    
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
