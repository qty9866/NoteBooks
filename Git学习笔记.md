# Git学习笔记

## 认识Git

**认识工作区和暂存区**

将新文件拷贝至`hudfile`文件夹内，查看git状态

```bash
Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ cp ../index.html.01 index.html

Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ cp -r ../images/ .

Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        images/
        index.html

nothing added to commit but untracked files present (use "git add" to track)

Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)

```

**让git对新加入的文件进行管理**

```bash
Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ git add images index.html
warning: in the working copy of 'index.html', LF will be replaced by CRLF the next time Git touches it

Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ ls -al
total 18
drwxr-xr-x 1 Hud 197121    0 Aug 16 22:16 ./
drwxr-xr-x 1 Hud 197121    0 Aug 16 22:14 ../
drwxr-xr-x 1 Hud 197121    0 Aug 16 22:34 .git/
drwxr-xr-x 1 Hud 197121    0 Aug 16 22:16 images/
-rw-r--r-- 1 Hud 197121 1303 Aug 16 22:14 index.html
-rw-r--r-- 1 Hud 197121   51 Aug 11 20:31 readme.txt
-rw-r--r-- 1 Hud 197121  149 Aug  9 21:23 test2.go

Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ git status
On branch master
Your branch is up to date with 'origin/master'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   images/git-logo.png
        new file:   index.html							#已经被放入暂存区了
```

**创建正式的提交**

```bash
Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ git commit -m'Add index'
[master e47b4e5] Add index
 2 files changed, 49 insertions(+)
 create mode 100644 images/git-logo.png
 create mode 100644 index.html
 
 $ git log							# 提交的信息
commit e47b4e5600afbc5da3b2e6771157e42d84e18586 (HEAD -> master)
Author: Hud <qitianyu2007@126.com>
Date:   Tue Aug 16 22:40:48 2022 +0800

    Add index
```

对于已经添加过然后进行修改的文件，可以使用g`it add -u`进行更新

```bash
Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   index.html

no changes added to commit (use "git add" and/or "git commit -a")

Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ git add -u
warning: in the working copy of 'index.html', LF will be replaced by CRLF the next time Git touches it

Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 3 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   index.html
```



### **git给文件进行重命名**

**`git mv [filename] [new_filename]`**

```bash
Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 4 commits.
  (use "git push" to publish your local commits)

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        renamed:    readme.txt -> readme.md
```

**清理**

```bash
Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ git reset --hard
HEAD is now at 19d878d Add Refering

Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ git status
On branch master
Your branch is ahead of 'origin/master' by 4 commits.
  (use "git push" to publish your local commits)

nothing to commit, working tree clean

```



### git log查看版本演变历史

- **简介的查看git log历史** `git log --oneline`

  ```bash
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
  $ git log --oneline
  cc14d60 (HEAD -> master) move readme to readme.md
  19d878d Add Refering
  35d0a2d Add js
  addd920 Add style.css
  e47b4e5 Add index
  2cff4ff (origin/master) Add Readme,txt
  a4486d4 test2.go v3.0
  3e46913 test2.go v2.0
  2aac365 test2.go v1.0
  c3e4ad6 test2.go
  ```

- **只查看最近的x次commit操作** `git log -nx` 

  ```bash
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
  $ git log -n4 --oneline
  cc14d60 (HEAD -> master) move readme to readme.md
  19d878d Add Refering
  35d0a2d Add js
  addd920 Add style.css
  ```

- **查看所有分支的log** `git log -all`

- **查看图形化log**   `git log --graph`

  ```bash
  $ git log --graph
  * commit cc14d6008628a36d134a536f3f5e6b9ea2f7129c (HEAD -> master)
  | Author: Hud <qitianyu2007@126.com>
  | Date:   Sat Aug 20 22:37:32 2022 +0800
  |
  |     move readme to readme.md
  |
  * commit 19d878dca355525d28886d71e4efc0d22afda809
  | Author: Hud <qitianyu2007@126.com>
  | Date:   Wed Aug 17 00:00:23 2022 +0800
  |
  |     Add Refering
  |
  * commit 35d0a2d520f0ec2471a346ce59f6f6421326b821
  | Author: Hud <qitianyu2007@126.com>
  | Date:   Tue Aug 16 23:37:51 2022 +0800
  |
  |     Add js
  |
  * commit addd920dfb5d613f4b59e8dee79a12f0e3717da9
  | Author: Hud <qitianyu2007@126.com>
  | Date:   Tue Aug 16 23:01:57 2022 +0800
  |
  |     Add style.css
  |
  * commit e47b4e5600afbc5da3b2e6771157e42d84e18586
  | Author: Hud <qitianyu2007@126.com>
  | Date:   Tue Aug 16 22:40:48 2022 +0800
  |
  |     Add index
  |
  * commit 2cff4ff586a0236d64d5082ff856b81ebb701ca3 (origin/master)
  | Author: Hud <qitianyu2007@126.com>
  | Date:   Thu Aug 11 20:36:59 2022 +0800
  |
  |     Add Readme,txt
  |
  * commit a4486d405fb2c1eb7071221e068960288a7aebe6
  | Author: Hud <qitianyu2007@126.com>
  | Date:   Tue Aug 9 21:24:48 2022 +0800
  |
  |     test2.go v3.0
  |
  * commit 3e469138b9ccfd3acebe9d6d5bee91624059ac7b
  | Author: Hud <qitianyu2007@126.com>
  | Date:   Tue Aug 9 20:40:36 2022 +0800
  |
  |     test2.go v2.0
  |
  ```

- **查看git log帮助**

  ```bash
  $ git help --web log  //通過網頁查看git log help
  ```

- **使用图形化界面查看版本历史**

  ```bash
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
  $ gitk
  ```

### 查看.git目录

- #### **HEAD**

```bash
Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
$ cd .git/

Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git (GIT_DIR!)
$ ls -al
total 26
drwxr-xr-x 1 Hud 197121   0 Aug 21 12:29 ./
drwxr-xr-x 1 Hud 197121   0 Aug 20 22:36 ../
-rw-r--r-- 1 Hud 197121  25 Aug 20 22:37 COMMIT_EDITMSG
-rw-r--r-- 1 Hud 197121  23 Aug  9 20:05 HEAD
-rw-r--r-- 1 Hud 197121  41 Aug 20 22:33 ORIG_HEAD
-rw-r--r-- 1 Hud 197121 299 Aug 11 20:37 config
-rw-r--r-- 1 Hud 197121  73 Aug  9 20:05 description
-rw-r--r-- 1 Hud 197121 462 Aug 21 12:29 gitk.cache
drwxr-xr-x 1 Hud 197121   0 Aug  9 20:05 hooks/
-rw-r--r-- 1 Hud 197121 626 Aug 20 22:36 index
drwxr-xr-x 1 Hud 197121   0 Aug  9 20:05 info/
drwxr-xr-x 1 Hud 197121   0 Aug  9 20:23 logs/
drwxr-xr-x 1 Hud 197121   0 Aug 20 22:37 objects/
drwxr-xr-x 1 Hud 197121   0 Aug  9 21:22 refs/

Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git (GIT_DIR!)
$ cat HEAD
ref: refs/heads/master
```

HEAD文件中，使用ref到当前使用的分支上

- #### config

  ```bash
  $ cat config
  [core]
          repositoryformatversion = 0
          filemode = false
          bare = false
          logallrefupdates = true
          symlinks = false
          ignorecase = true
  [remote "origin"]
          url = git@github.com:qty9866/hud-files.git
          fetch = +refs/heads/*:refs/remotes/origin/*
  [branch "master"]
          remote = origin
          merge = refs/heads/master
  ```

  存放了配置信息

- #### ref文件夹

  ```bash
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git/refs (GIT_DIR!)
  $ ls -al
  total 4
  drwxr-xr-x 1 Hud 197121 0 Aug  9 21:22 ./
  drwxr-xr-x 1 Hud 197121 0 Aug 21 12:29 ../
  drwxr-xr-x 1 Hud 197121 0 Aug 20 22:37 heads/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 21:22 remotes/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 20:05 tags/
  ```

  git仓库可以由很多个标签`tag`（里程碑）的，heads对应的就是分支：一个独立的开发空间，例如一个分支给前端，一个分支给后端。不同分支互不影响，又可以在需要是进行集成

  **查看ref文件中的内容**

  ```bash
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files (master)
  $ cd .git/refs/heads/
  
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git/refs/heads (GIT_DIR!)
  $ ls -al
  total 1
  drwxr-xr-x 1 Hud 197121  0 Aug 20 22:37 ./
  drwxr-xr-x 1 Hud 197121  0 Aug  9 21:22 ../
  -rw-r--r-- 1 Hud 197121 41 Aug 20 22:37 master
  
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git/refs/heads (GIT_DIR!)
  $ cat master
  cc14d6008628a36d134a536f3f5e6b9ea2f7129c
  ```

  **看看这个文件的类型是什么**

  ```bash
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git/refs/heads (GIT_DIR!)
  $ git cat-file -t cc14d600862
  commit
  ```

  是一个commit文件，再看看branch分支文件

  ```bash
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git/refs/heads (GIT_DIR!)
  $ git branch -av
  * master                cc14d60 [ahead 5] move readme to readme.md
    remotes/origin/master 2cff4ff Add Readme,txt
  ```

  可以看到分支master指向的就是`cc14d60`

- #### Objects文件

  ```bash
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git (GIT_DIR!)
  $ cd objects/
  
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git/objects (GIT_DIR!)
  $ ls -al
  total 8
  drwxr-xr-x 1 Hud 197121 0 Aug 20 22:37 ./
  drwxr-xr-x 1 Hud 197121 0 Aug 21 12:29 ../
  drwxr-xr-x 1 Hud 197121 0 Aug 16 22:40 05/
  drwxr-xr-x 1 Hud 197121 0 Aug 17 00:00 19/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 20:39 2a/
  drwxr-xr-x 1 Hud 197121 0 Aug 11 20:36 2c/
  drwxr-xr-x 1 Hud 197121 0 Aug 16 23:37 35/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 20:40 3e/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 21:24 40/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 20:40 48/
  drwxr-xr-x 1 Hud 197121 0 Aug 20 22:36 4d/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 20:23 4e/
  drwxr-xr-x 1 Hud 197121 0 Aug 16 22:34 6a/
  drwxr-xr-x 1 Hud 197121 0 Aug 11 20:36 6e/
  drwxr-xr-x 1 Hud 197121 0 Aug 16 23:58 82/
  drwxr-xr-x 1 Hud 197121 0 Aug 16 23:37 87/
  drwxr-xr-x 1 Hud 197121 0 Aug 16 23:01 8f/
  drwxr-xr-x 1 Hud 197121 0 Aug 16 22:40 96/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 21:24 a4/
  drwxr-xr-x 1 Hud 197121 0 Aug 16 23:37 ab/
  drwxr-xr-x 1 Hud 197121 0 Aug 16 23:01 ad/
  drwxr-xr-x 1 Hud 197121 0 Aug 16 23:01 ae/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 20:22 b9/
  drwxr-xr-x 1 Hud 197121 0 Aug 17 00:00 bb/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 20:23 c3/
  drwxr-xr-x 1 Hud 197121 0 Aug 20 22:37 cc/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 20:38 cf/
  drwxr-xr-x 1 Hud 197121 0 Aug 16 23:37 d2/
  drwxr-xr-x 1 Hud 197121 0 Aug 16 22:34 da/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 20:39 e3/
  drwxr-xr-x 1 Hud 197121 0 Aug 16 22:40 e4/
  drwxr-xr-x 1 Hud 197121 0 Aug 16 23:00 ef/
  drwxr-xr-x 1 Hud 197121 0 Aug 11 20:32 f1/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 20:40 f3/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 20:05 info/
  drwxr-xr-x 1 Hud 197121 0 Aug  9 20:05 pack/
  
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git/objects (GIT_DIR!)
  $ cd e3
  
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git/objects/e3 (GIT_DIR!)
  $ ls -al
  total 5
  drwxr-xr-x 1 Hud 197121  0 Aug  9 20:39 ./
  drwxr-xr-x 1 Hud 197121  0 Aug 20 22:37 ../
  -r--r--r-- 1 Hud 197121 53 Aug  9 20:39 d0cd337bc8b4125e1261ee5a842f6e5aace559
  
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git/objects/e3 (GIT_DIR!)
  $ git cat-file -t e3d0cd337bc8b4
  tree
  
  ```

  这里面两个字符的文件夹名与文件夹中的哈希值组合，组成一个哈希，查看类型，是一个tree

  **查看他的内容**

  ```bash
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git/objects/e3 (GIT_DIR!)
  $ git cat-file -p e3d0cd337bc8b4
  100644 blob cf873b248a2e4b0aaed472d6702c96a0b77b089c    test2.go
  ```

  看看这个blob文件

  ```bash
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git/objects/e3 (GIT_DIR!)
  $ git cat-file -t cf873b248a2e4
  blob
  
  Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git/objects/e3 (GIT_DIR!)
  $ git cat-file -p cf873b248a2e4
  package main
  
  func main() {
          println("this is hello from hud!")
  }
  ```

### commit、tree、blob三个对象之间的关系

一个commit对应一棵树，tree视图存放着快照，也就是当前commit对应的所有文件夹、文件的一个快照。意思就是这次commit提交的内容究竟是什么样子，通过这棵树tree来进行呈现的。

对于git而言，只要文件内容相同，就是同一个blob。

举个例子，查看git log

```bash
$ git log -n4 --oneline
cc14d60 (HEAD -> master) move readme to readme.md
19d878d Add Refering
35d0a2d Add js
addd920 Add style.css
```

选择add style.css的这个文件的hash

```bash
Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git (GIT_DIR!)
$ git cat-file -t addd920
commit

Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git (GIT_DIR!)
$ git cat-file -p addd920
tree 8fd476376ffade22a444af1f31aebee240c23fae
parent e47b4e5600afbc5da3b2e6771157e42d84e18586
author Hud <qitianyu2007@126.com> 1660662117 +0800
committer Hud <qitianyu2007@126.com> 1660662117 +0800

Add style.css
```

可以看到commit对应了一个tree 父commit，作者信息和提交者信息

```bash
Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git (GIT_DIR!)
$ git cat-file -p 8fd476376ffad
040000 tree 96b67e399c8496ec36cbbbcb776eb924fad7f9a7    images
100644 blob 6ad4c68d567a1a5b415dcfce2010fce1a60b245f    index.html
100644 blob f1d2e10fa9c6132bd937e5d47fcb7a9c2808eb32    readme.txt
040000 tree aee37060401d19e7bd9f80b7b33920a000e96b5b    styles
100644 blob 40fb542f04bf192b185f3dedf3b8d42dcaf113ea    test2.go
```

两棵树和三个blob

```bash
Hud@PC-Hud MINGW64 ~/git-learning/hud-files/.git (GIT_DIR!)
$ git cat-file -p 96b67e399c8496ec
100644 blob daf480669aa9256fa18b5c28e467af816f16482d    git-logo.png
```

但是這個blob文件无法查看，因为是二进制格式的

**练习：**

```bash
#新建一个git仓库
Hud@PC-Hud MINGW64 ~/new-git
$ git init watch_git_objects
Initialized empty Git repository in C:/Users/Hud/new-git/watch_git_objects/.git/

#进入git仓库
Hud@PC-Hud MINGW64 ~/new-git
$ cd watch_git_objects/

#创建一个目录
Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ mkdir doc
#查看git状态，发现创建空目录时候git不予理会
Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ git status
On branch master

No commits yet

nothing to commit (create/copy files and use "git add" to track)
#进去doc目录
Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ cd doc
#创建readme
Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects/doc (master)
$ echo "hello world" > readme

Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects/doc (master)
$ cd ..
# 这个时候git终于有反应了
Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        doc/

nothing added to commit but untracked files present (use "git add" to track)
```

**查看.git/objects**

```bash
Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ find .git/objects/ -type f
# 現在是空的
```

**add添加进去**

```
Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ git add doc
warning: in the working copy of 'doc/readme', LF will be replaced by CRLF the next time Git touches it

Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   doc/readme


Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ find .git/objects/ -type f
.git/objects/3b/18e512dba79e4c8300dd08aeb37f8e728b8dad
```

git add指令执行后，objects中有了hash，看看这个hash是什么：

```bash
Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ git cat-file -t 3b18e512dba
blob

Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ git cat-file -p 3b18e512dba
hello world

```

这说明有新的文件加入暂存区后，git就会主动的为我们生成blob

现在看看objects里面的文件以及类型

```bash
Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ find .git/objects/ -type f
.git/objects/07/e73d5bb332cd94621f4042fcf5bb5436fbad94
.git/objects/2c/5264370f2630da80ee38f412213d59657af6e8
.git/objects/3b/18e512dba79e4c8300dd08aeb37f8e728b8dad
.git/objects/f5/5a12e98ffd80349f3499cc52a06b8afb93ec90

Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ git cat-file -t 07e73d5bb3
commit

Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ git cat-file -t 2c5264370f
tree

Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ git cat-file -t 3b18e512db
blob

Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ git cat-file -t f55a12e98f
tree
```

两个tree中，一个存放doc文件夹 一个存放blob文件：

```bash
Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ git cat-file -p 2c5264370f
100644 blob 3b18e512dba79e4c8300dd08aeb37f8e728b8dad    readme

Hud@PC-Hud MINGW64 ~/new-git/watch_git_objects (master)
$ git cat-file -p f55a12e98f
040000 tree 2c5264370f2630da80ee38f412213d59657af6e8    doc
```

分离头指针：commit的文件不存在与分支当中

