#+TITLE: Git Presentation

---

* Git

---

** CheatSheet
|----------------------------+-------------------------|
| Command                    | Usage                   |
|----------------------------+-------------------------|
| ~git cat-file -p <hashid>~ | Print content of object |
|----------------------------+-------------------------|

** What is a commit?

---

- An object
- Pointer to a tree
- Author, Message, Timestamp

** Some Git Terms

- Objects
- Refs [Heads/Tags]
- Branches
- Index
- HEAD

** Cache eq Index eq Staged
** What have I done?

---

 -  RefLog
 - Tracking all commits on braches

 #+BEGIN_SRC bash

 $ git reflog

 735595e (HEAD -> master) HEAD@{0}: commit (initial): initial commit

 $ cat .git/logs/HEAD     
 0000000000000000000000000000000000000000 735595e591374b524987698e3b151edeb040179a Tomer Ben David <tomer.bendavid@thomsonreuters.com> 1524558335 +0300  commit (initial): initial commit

 #+END_SRC

Note:
#+BEGIN_SRC bash
git init gittest
➜  gittest git:(master) cat .git/HEAD  # => HEAD is pointing to a reference
ref: refs/heads/master
➜  gittest git:(master) cat refs/heads/master # => We didn’t do anything yet no such file
cat: refs/heads/master: No such file or directory
#+END_SRC

---

** Untrack

~git rm --cached somefile.txt~

Note:
Remember cache eq index eq stage

** Index

- Add file - index

Note:
#+BEGIN_SRC 
➜  gittest git:(master) ✗ git add test.ts
➜  gittest git:(master) ✗ ls .git
HEAD        branches    config      description hooks       index       info        objects     refs

Note that now we have index file

➜  gittest git:(master) ✗ file .git/index
.git/index: Git index, version 2, 1 entries

➜  gittest git:(master) ✗ git ls-files --stage
100644 a32aa4bc6a512f85e95cc7e8420f52b8619aae96 0	test.ts

➜  gittest git:(master) ✗ git cat-file -p a9534b1f48eba2a01cb0a0b99eb8fa83ba8dde17 
iiii
#+END_SRC

** Objects

- Our current objects

Note:
#+BEGIN_SRC bash
➜  gittest git:(master) ✗ ls .git/objects
a3   info pack

➜  gittest git:(master) ✗ git cat-file -p a32aa4bc6a512f85e95cc7e8420f52b8619aae96
export class MyMain { }
#+END_SRC

** Tree

Note:
#+BEGIN_SRC bash
➜  gittest git:(master) ✗ git cat-file -p master^{tree}
fatal: Not a valid object name master^{tree}

Indeed we have nothing on our tree yet.
#+END_SRC

** Commit

Note:
#+BEGIN_SRC 
➜  gittest git:(master) ✗ git commit -a -m "test.ts"
[master (root-commit) c6f078b] test.ts
 1 file changed, 1 insertion(+)
 create mode 100644 test.ts

git cat-file -p c6f078b # => take from commit result

➜  gittest git:(master) ls .git/objects 
81   a3   c6   info pack

# => We have many more objects

➜  gittest git:(master)git ls-tree master                                
100644 blob a32aa4bc6a512f85e95cc7e8420f52b8619aae96    test.ts

# => We have a single blob in our master.
#+END_SRC

** Refs

Note:
#+BEGIN_SRC 
➜  gittest git:(master) cat .git/refs/heads/master
735595e591374b524987698e3b151edeb040179a
#+END_SRC

** Intellij Pitfalls

- If you remove a file and commit and then pull from intellij
- It might not show the correct status pull might say you have uncommitted changes so we need to do `git status` and then...

---

## Push URL

```bash
➜  lbl-desktop-backend git:(development) ✗ git remote -v
origin  https://github.com/someproject/engine (fetch)
origin  https://git.sami.int.thomsonreuters.com/tmsops-labelingtool/engine (push)
➜  lbl-desktop-backend git:(development) ✗ git remote set-url origin https://git.sami.int.thomsonreuters.com/Tomer.BenDavid/engine
➜  lbl-desktop-backend git:(development) ✗ git remote -v                                                                          
origin  https://git.sami.int.thomsonreuters.com/Tomer.BenDavid/engine (fetch)
origin  https://git.sami.int.thomsonreuters.com/Tomer.BenDavid/engine (push)
```

# Table of Contents

1.  [Git](#orgb29a65d)
    1.  [What is a commit?](#orgdfd40a4)
    2.  [Some Git Terms](#orge3d5e6f)
    3.  [What have I done?](#org920f63b)
    4.  [Index](#org4078cc4)

---

# Git

---

## What is a commit?

-   An object
-   Pointer to a tree
-   Author, Message, Timestamp

---

## Some Git Terms

-   Objects
-   Refs [Heads/Tags]
-   Branches
-   Index
-   HEAD

---

## What have I done?

---

-   RefLog
-   Tracking all commits on braches

  
    $ git reflog
    
    735595e (HEAD -> master) HEAD@{0}: commit (initial): initial commit
    
    $ cat .git/logs/HEAD     
    0000000000000000000000000000000000000000 735595e591374b524987698e3b151edeb040179a Tomer Ben David <tomer.bendavid@thomsonreuters.com> 1524558335 +0300  commit (initial): initial commit

Notes:

    git init gittest
    ➜  gittest git:(master) cat .git/HEAD  # => HEAD is pointing to a reference
    ref: refs/heads/master
    ➜  gittest git:(master) cat refs/heads/master # => We didn’t do anything yet no such file
    cat: refs/heads/master: No such file or directory

---

## Index

-   Add file - index

Notes:

    ➜  gittest git:(master) ✗ git add test.ts
    ➜  gittest git:(master) ✗ ls .git
    HEAD        branches    config      description hooks       index       info        objects     refs
    
    Note that now we have index file
    
    ➜  gittest git:(master) ✗ file .git/index
    .git/index: Git index, version 2, 1 entries
    
    ➜  gittest git:(master) ✗ git ls-files --stage
    100644 a32aa4bc6a512f85e95cc7e8420f52b8619aae96 0	test.ts
    
    ➜  gittest git:(master) ✗ git cat-file -p a9534b1f48eba2a01cb0a0b99eb8fa83ba8dde17 
    iiii
