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

#### Problems

1. If you don't have any past experience with Git, either try reading the first
   couple chapters of [Pro Git](https://git-scm.com/book/en/v2) or go through a
   tutorial like <a href="https://learngitbranching.js.org/" target="_blank">Learn Git Branching</a>. As
   you're working through it, relate Git commands to the data model.

   <details open><summary><b>Solution</b></summary>
   <p> 

   This solution got so long I created it's own repository: [Learn Git Branching Solultions and Notes](https://github.com/blentz100/Learn-Git-Branching-Solutions-and-Notes)

   </p>
   </details>

 
1. Clone the [repository for the
class website](https://github.com/missing-semester/missing-semester).
    1. Explore the version history by visualizing it as a graph.
       <details open><summary><b>Solution</b></summary>
       <p> 

       `git log --all --graph --decorate`
         
        <img src="https://github.com/blentz100/missing-semester-solutions/blob/main/images/gitlogoutput.png?raw=true" alt="drawing" width="600"/>
        
        I was wondering what the different colors mean in the output and found this answer on Stackoverflow: [What do the line colors in git log --graph mean?](https://stackoverflow.com/questions/40675151/what-do-line-colors-in-git-log-graph-mean) (tldr: nothing important)

       </p>
       </details>
    1. Who was the last person to modify `README.md`? (Hint: use `git log` with
       an argument).
       
       <details open><summary><b>Solution</b></summary>
       <p> 
       
       Anish Athalye
       
       ```git log -n 1 README.md```
       
        <img src="https://github.com/blentz100/missing-semester-solutions/blob/main/images/Solution_2.2.png?raw=true" alt="drawing" width="600"/>
       

       </p>
       </details>
    1. What was the commit message associated with the last modification to the
       `collections:` line of `_config.yml`? (Hint: use `git blame` and `git
       show`)
       
       <details open><summary><b>Solution</b></summary>
       <p> 
       
       Commit message: Redo lectures as a collection
       
       `git blame _config.yml`
       
       `git show a884beac`
      
      </p>
      </details>
       


1. One common mistake when learning Git is to commit large files that should
   not be managed by Git or adding sensitive information. Try adding a file to
   a repository, making some commits and then deleting that file from history
   (you may want to look at
   [this](https://help.github.com/articles/removing-sensitive-data-from-a-repository/)).
   
   <details open><summary><b>Solution</b></summary>
       <p> 
       
      Successfully installed bfg cleaner using homebrew installation.
          
      Ran the tool and it defintely changed the commit id's that referenced the
      most recent test commits I did. In order to see the file actually gone
      from the directory listing, I had to checkout an earlier commit. BFG's
      default behavior seems to be to leave the latest commit in place. See
      their documenation for more details. So according to my testing this
      worked as designed. Output:

      ```console
          ➜  missing-semester git:(master) ✗ bfg --delete-files delete_me.txt


            Using repo : /Users/brendanlentz/missing-semester/.git

            Found 77 objects to protect
            Found 6 commit-pointing refs : HEAD, refs/heads/master, refs/remotes/origin/HEAD, ...

            Protected commits
            -----------------

            These are your protected commits, and so their contents will NOT be altered:

             * commit 45ce763c (protected by 'HEAD') - contains 1 dirty file :
                    - delete_me.txt (786 B )

            WARNING: The dirty content above may be removed from other commits, but as
            the *protected* commits still use it, it will STILL exist in your repository.

            Details of protected dirty content have been recorded here :

            /Users/brendanlentz/missing-semester.bfg-report/2021-09-10/08-32-49/protected-dirt/

            If you *really* want this content gone, make a manual commit that removes it,
            and then run the BFG on a fresh copy of your repo.


            Cleaning
            --------

            Found 510 commits
            Cleaning commits:       100% (510/510)
            Cleaning commits completed in 562 ms.

            Updating 2 Refs
            ---------------

                    Ref                          Before     After
                    ------------------------------------------------
                    refs/heads/master          | 45ce763c | df3f4027
                    refs/remotes/origin/master | 45ce763c | df3f4027

            Updating references:    100% (2/2)
            ...Ref update completed in 47 ms.

            Commit Tree-Dirt History
            ------------------------

                    Earliest                                              Latest
                    |                                                          |
                    ...........................................................D

                    D = dirty commits (file tree fixed)
                    m = modified commits (commit message or parents changed)
                    . = clean commits (no changes to file tree)

                                            Before     After
                    -------------------------------------------
                    First modified commit | ef485e99 | 96b3b09f
                    Last dirty commit     | febb6eec | 6e9c0f46

            Deleted files
            -------------

                    Filename        Git id
                    ----------------------------------------------------
                    delete_me.txt | c247dd3a (606 B ), 8c3e0171 (182 B )


            In total, 5 object ids were changed. Full details are logged here:

                    /Users/brendanlentz/missing-semester.bfg-report/2021-09-10/08-32-49

            BFG run is complete! When ready, run: git reflog expire --expire=now --all && git gc --prune=now --aggressive


            ➜  missing-semester git:(master) ✗ git reflog expire --expire=now --all && git gc --prune=now --aggressive
            Enumerating objects: 1947, done.
            Counting objects: 100% (1947/1947), done.
            Delta compression using up to 4 threads
            Compressing objects: 100% (1904/1904), done.
            Writing objects: 100% (1947/1947), done.
            Total 1947 (delta 1181), reused 714 (delta 0), pack-reused 0
            ➜  missing-semester git:(master) ✗

            ➜  missing-semester git:(96b3b09) ✗
      ```
          
      
   </p>
   </details>

1. Clone some repository from GitHub, and modify one of its existing files.
   What happens when you do `git stash`? What do you see when running `git log
   --all --oneline`? Run `git stash pop` to undo what you did with `git stash`.
   In what scenario might this be useful?
   
      <details open><summary><b>Solution</b></summary>
      <p> 
       
      ```console
      ➜  test git clone https://github.com/tomnomnom/gron
      Cloning into 'gron'...
      remote: Enumerating objects: 774, done.
      remote: Counting objects: 100% (7/7), done.
      remote: Compressing objects: 100% (6/6), done.
      remote: Total 774 (delta 1), reused 4 (delta 1), pack-reused 767
      Receiving objects: 100% (774/774), 1.45 MiB | 2.00 MiB/s, done.
      ➜  gron git:(master) echo changingREADMEfilebyappendingthislongweirdstringtoit >> README.mkd
      ➜  gron git:(master) ✗ git stash
      Saved working directory and index state WIP on master: 6d4fe18 Removes older go version from .travis.yml
      ➜  gron git:(master) git log --all --oneline   
      e939829 (refs/stash) WIP on master: 6d4fe18 Removes older go version from .travis.yml
      562f601 index on master: 6d4fe18 Removes older go version from .travis.yml
      6d4fe18 (HEAD -> master, tag: v0.6.1, origin/master, origin/HEAD) Removes older go version from .t
      ravis.yml
      7e958f8 Merge pull request #78 from alblue/master
      ...
     ➜  gron git:(master) git stash pop
      On branch master
      Your branch is up to date with 'origin/master'.

      Changes not staged for commit:
        (use "git add <file>..." to update what will be committed)
        (use "git restore <file>..." to discard changes in working directory)
              modified:   README.mkd

      no changes added to commit (use "git add" and/or "git commit -a")
      Dropped refs/stash@{0} (77752cbd47999c92cc164057e23a9beff7fc54a2)
 


      ```
       
       

      </p>
      </details>



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

   <details open><summary><b>Solution</b></summary>
   <p> 

   [PR #141](https://github.com/missing-semester/missing-semester/pull/141)
      
   <img src="https://github.com/blentz100/missing-semester-solutions/blob/main/images/pr_screenshot.png?raw=true" alt="drawing" width="600"/>
   </p>
   </details>

   
   
   


## [Debugging and Profiling](https://missing.csail.mit.edu/2020/debugging-profiling/)
## [Metaprogramming](https://missing.csail.mit.edu/2020/metaprogramming/)
## [Security and Cryptography](https://missing.csail.mit.edu/2020/security/)
## [Potpourri](https://missing.csail.mit.edu/2020/potpourri/)
## [Q&A](https://missing.csail.mit.edu/2020/qa/)
