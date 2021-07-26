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

            ```console
            git commit
            git commit
            ```
            
    
      2. Branching in Git

            Branches are pointers to commits. "Branch early and branch often." A branch essentially says "I want to include the work of this commit and all parent commits.

         Make a new branch called bugFix and switch to that branch.

         Solution 1:

         ```console
         git branch bugFix
         git checkout bugFix
         ```

         Solution 2:

         ```console
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

         ```console
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

            ```console
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
         
         ```console
         git checkout C4
         ```

      2. Relative Refs (^)

         ```git log``` is what we will use in the real world to see what our commit tree looks like. Relative refs make it easier to move up or down a relative number of times in the commit tree. ```^``` moves up one level in the commit tree and ```~<num>``` moves upwards the number of times specified.
         
         
         To complete this level, check out the parent commit of bugFix. This will detach HEAD.

         You can specify the hash if you want, but try using relative refs instead!
         
         Solution 1: (relative ref)
         
         ```console
         git checkout bugFix^
         ```
         
         Solution 2: (relative ref)
         
         ```console
         git checkout bugFix~1
         ```
         
         Solution 3: (relative ref)
         
         ```console
         git checkout C4^
         ```
         
         Solution 4: (direct hash)
         
         ```console
         git checkout C3
         ```
         

      3. Relative Refs #2 (^)

         A common use of relative refs is to move branches around You can directly reassign a branch to a commit with the -f option: ```git branch -f main HEAD~3``` will force the main branch to 3 parents behind the HEAD.
         
         To complete this level, move HEAD, main, and bugFix to their goal destinations shown
         
         Solution:
         
         ```console
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
         
         ```console
         git reset HEAD^
         git checkout pushed
         git revert pushed
         ```

         
    #### Moving Work Around - "Git" comfortable with modifying the source tree :P

    
      1. Cherry-pick Intro
            ```git cherry-pick <commit1> <commit2> <...>``` says you want to grab a series of commits and copy it below your current location (HEAD)

            To complete this level, simply copy some work from the three branches shown into main. You can see which commits we want by looking at the goal visualization.

           Solution:
           
           ```console
           git cherry-pick C3 C4 C7
           ```


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
    
          Another use case that happens commonly is we need to change a commit way back in our commit history. 
          
          The section utilizes ```git commit --amend```. A good explanation of that command is at the [Pro Git Book](https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History). This is useful for making a small change to your most recent commit, like modifying the commit message. 
          
          Here is the problem: 

         We will overcome this difficulty by doing the following:

         We will re-order the commits so the one we want to change is on top with git rebase -i
         
         We will git commit --amend to make the slight modification
         
         Then we will re-order the commits back to how they were previously with git rebase -i
         
         Finally, we will move main to this updated part of the tree to finish the level (via the method of your choosing)
         
         There are many ways to accomplish this overall goal (I see you eye-ing cherry-pick), and we will see more of them later, but for now let's focus on this technique. Lastly, pay attention to the goal state here -- since we move the commits twice, they both get an apostrophe appended. One more apostrophe is added for the commit we amend, which gives us the final form of the tree

           ```console
          git rebase -i C1 

          git checkout newImage 

          git commit --amend 

          git checkout caption

          git rebase -i C1 

          git branch -f main C3 
          
          git checkout main
          
          ```
          
      3. Juggling Commits #2

            The reordering done in the prior section can cause rebase conflicts, so we can use git cherry-pick to avoid those. 
    
            git cherry-pick will plop down a commit from anywhere in the tree onto HEAD
            
            The problem: So in this level, let's accomplish the same objective of amending C2 once but avoid using rebase -i. I'll leave it up to you to figure it out! :D
            
            ```console
            git checkout main
            git cherry-pick c2
            git cherry-pick c3
            ```
            
            My solution used 3 commands, their solution used 4 commands. That's a little odd that it worked. It didn't require me to use the git ammend command which I thought I might have to use. 

             
 
    
      4.  Git Tags

            Branches are useful but they are mutable and often changing. Tags are a way to (almost) permanently mark certain commits as milestones.
         
            Solution:
         
            ``` console
            git tag v0 c1
            git tag v1 c2
            git checkout v1
            ```

      5.  Git Describe
    
            ```git describe``` will tell you where you are relative to the closest anchor.
            
            Solution:

            ```console
            git describe
            git describe HEAD
            git describe main
            git describe c5
            git describe c3
            git describe side
            git commit
            ```
     
    
    
    #### Advanced Topics - For the Truly Brave!
    1. Rebasing over 9000 times

         Rebasing 
         Branches
         Man, we have a lot of branches going on here! Let's rebase all the work from these branches onto main.

         Upper management is making this a bit trickier though -- they want the commits to all be in sequential order. So this means that our final tree should have C7' at the bottom, C6' above that, and so on, all in order.

         Solution:

         ```console
         git rebase c6
         git checkout c3
         git rebase c2'
         git checkout c7
         git rebase c3'
         git checkout c7'
         git rebase -i c0
         git branch -f main c7''
         ```
      
      
    3. Multiple parents

         The ```^``` operator specifies which parent reference to follow from a merge commit.
         
         To complete this level, create a new branch at the specified destination.

         Obviously it would be easy to specify the commit directly (with something like C6), but I challenge you to use the modifiers we talked about instead!
         
         Solution:
         
         ```console
         git branch bugWork main~1^2~1
         ```
         
         Alternate solution but not using the operators taught in this lesson:
         
         ```console
         git branch bugWork C2
         ````
         
         
    5. Branch spaghetti

         
    
    
   
    
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
