---
title: git
tags: #git
---


## setup and config 配置
### git config
这是运行git前需要进行的配置，每台计算机只需要配置一次，程序升级时会保留配置信息。通过git config来配置变量，这些变量存储在三个不同的位置.  
#### git config --system
带'--system'选项的，会读写'/etc/gitconfig'文件，包含系统上每一位用户及他们的仓库的通用配置.  
#### git config --global
带'--global'选项的，会读写'~/.gitconfig' 或 '~/.config/git/config' 文件,针对当前用户的所有仓库.  
例如: 如下代码配置你的用户名和邮箱  
```shell
git config --global user.name "xxx"
git config --global user.email "xxx@xxx.xxx"
```
#### git config [--local]
带'--local'选项，也就是默认的选项，会读写'.git/config'文件,针对该仓库.

#### git config --list  
查看当前用户的配置
如需查看所有配置及它们所在的文件可使用如下命令
```shell
git config --list --show-origin
```

#### git config --global init.defaultBranch
设置默认主分支名称，github,macos默认已经改成main.  
By default Git will create a branch called _master_ when you create a new repository with `git init`. From Git version 2.28 onwards, you can set a different name for the initial branch.

To set _main_ as the default branch name do:
```shell
git config --global init.defaultBranch main
```

## git help
Display help information about Git
查看帮助

## Getting a Git Repository 使用git仓库
### git init 初始化仓库
Initializing a Repository in an Existing Directory  
在文件夹中初始化仓库  
If you have a project directory that is currently not under version control and you want to start controlling it with Git, you first need to go to that project’s directory.
```shell
git init
```
This creates a new subdirectory named `.git` that contains all of your necessary repository files — a Git repository skeleton. At this point, nothing in your project is tracked yet.
### git clone 克隆仓库
Cloning an Existing Repository  
克隆一个已存在的仓库  
the command is "clone" and not "checkout". This is an important distinction — instead of getting just a working copy, Git receives a full copy of nearly all data that the server has. Every version of every file for the history of the project is pulled down by default when you run `git clone`.
 You clone a repository with `git clone <url>`. 
```shell
git clone https://github.com/xxx/xxx
```
## Basic Snapshotting 基本的版本控制操作
### git add 添加要追踪的文件
Tracking New Files 追踪新文件  
In order to begin tracking a new file, you use the command `git add`. To begin tracking the `README` file, you can run this:
```shell
git add README
```
### git status 查看文件的状态
Checking the Status of Your Files

### git diff 查看被修改文件的修改前后差异
If the `git status` command is too vague for you — you want to know exactly what you changed, not just which files were changed — you can use the `git diff` command.

### git commit 提交修改
Committing Your Changes 提交修改

Now that your staging area is set up the way you want it, you can commit your changes. Remember that anything that is still unstaged — any files you have created or modified that you haven’t run `git add` on since you edited them — won’t go into this commit. They will stay as modified files on your disk. In this case, let’s say that the last time you ran `git status`, you saw that everything was staged, so you’re ready to commit your changes. 

#### git commit -m 带注释提交
you can type your commit message inline with the `commit` command by specifying it after a `-m` flag, like this:

```shell
git commit -m "the commit message for your changes"
```

#### git commit -a -m 将已经添加到暂存区的直接提交
Skipping the Staging Area 省略添加到暂存区直接提交  

Although it can be amazingly useful for crafting commits exactly how you want them, the staging area is sometimes a bit more complex than you need in your workflow. If you want to skip the staging area, Git provides a simple shortcut. Adding the `-a` option to the `git commit` command makes Git automatically stage every file that is already tracked before doing the commit, letting you skip the `git add` part:
```shell
$ git commit -a -m "the commit message for your changes"
```

### git restore 恢复工作区文件
git-restore - Restore working tree files
恢复未add的文件，和老版本中checkout一样的作用

#### git restore --staged <filename> 撤销添加到暂存区的文件
To restore a file in the index to match the version in HEAD (this is the same as using git-reset[1])
跟git-reset一样用法，撤销add到staged的文件，也就是删除掉暂存区的文件，保留磁盘修改的内容

### git reset 移动HEAD到指定位置
git-reset - Reset current HEAD to the specified state

### git reset,get restore和git revert 区别

### git 撤销操作不同命令图示
|命令|Working Directory|Staging<br>(index)|Repository|
|---|---|---|---|
|git checkout<changed_file><br>(git restore <changged_file>) |x||
|git reset<changed_file><br>(git restore --staged <changed_file>) ||x|
|git checkout HEAD <changed_file>|x|x||
|git reset --soft HEAD~1|||x|
|git reset HEAD~1||x|x|
|git reset --hard HEAD~1|x|x|x|

### git rm 
Removing Files 删除暂存区中的文件

To remove a file from Git, you have to remove it from your tracked files (more accurately, remove it from your staging area) and then commit. The `git rm` command does that, and also removes the file from your working directory so you don’t see it as an untracked file the next time around.

If you simply remove the file from your working directory, it shows up under the “Changes not staged for commit” (that is, _unstaged_) area of your `git status` output

### git mv
Moving Files 移动暂存区中的文件

Unlike many other VCSs, Git doesn’t explicitly track file movement. If you rename a file in Git, no metadata is stored in Git that tells it you renamed the file. However, Git is pretty smart about figuring that out after the fact — we’ll deal with detecting file movement a bit later.

### .gitignore 要忽略的文件
Ignoring Files 忽略要追踪的文件

Often, you’ll have a class of files that you don’t want Git to automatically add or even show you as being untracked. These are generally automatically generated files such as log files or files produced by your build system. In such cases, you can create a file listing patterns to match them named `.gitignore`. Here is an example `.gitignore` file:

```shell
cat .gitignore
```
```
*.[oa]
*~
```

The first line tells Git to ignore any files ending in “.o” or “.a” — object and archive files that may be the product of building your code. The second line tells Git to ignore all files whose names end with a tilde (`~`), which is used by many text editors such as Emacs to mark temporary files. You may also include a log, tmp, or pid directory; automatically generated documentation; and so on. Setting up a `.gitignore` file for your new repository before you get going is generally a good idea so you don’t accidentally commit files that you really don’t want in your Git repository.

The rules for the patterns you can put in the `.gitignore` file are as follows:

-   Blank lines or lines starting with `#` are ignored.
-   Standard glob patterns work, and will be applied recursively throughout the entire working tree.
-   You can start patterns with a forward slash (`/`) to avoid recursivity.
-   You can end patterns with a forward slash (`/`) to specify a directory.
-   You can negate a pattern by starting it with an exclamation point (`!`).

Glob patterns are like simplified regular expressions that shells use. An asterisk (`*`) matches zero or more characters; `[abc]` matches any character inside the brackets (in this case a, b, or c); a question mark (`?`) matches a single character; and brackets enclosing characters separated by a hyphen (`[0-9]`) matches any character between them (in this case 0 through 9). You can also use two asterisks to match nested directories; `a/**/z` would match `a/z`, `a/b/z`, `a/b/c/z`, and so on.

Here is another example `.gitignore` file:

```
# ignore all .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in any directory named build
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf
```

#### note 
In the simple case, a repository might have a single `.gitignore` file in its root directory, which applies recursively to the entire repository. However, it is also possible to have additional `.gitignore` files in subdirectories. The rules in these nested `.gitignore` files apply only to the files under the directory where they are located. The Linux kernel source repository has 206 `.gitignore` files.


## Branching and Merging 分支和合并
### git branch 查看本地分支
#### git branch -r 查看远程分支
#### git branch -a 查看所有分支
#### git branch <branch_name> 创建新的分支（但不会切换到新的分支）
Note that this will create the new branch, but it will not switch the working tree to it; use "git switch <newbranch>" to switch to the new branch.
#### git branch -d(--delete) <branch_name> 删除分支(会提示错误信息)
#### git branch -D <branch_name> 删除分支（强制）
强制删除，不会提示错误信息，不能删除当前所在分支

### git checkout 切换到新的分支或恢复工作区文件
Switch branches or restore working tree files
#### git checkout [<branch>]
To prepare for working on <branch>, switch to it by updating the index and the files in the working tree, and by pointing HEAD at the branch. Local modifications to the files in the working tree are kept, so that they can be committed to the <branch>.
#### git checkout -b <branch_name> 创建分支并切换到新的分支

### git log
Viewing the Commit History 查看提交历史

After you have created several commits, or if you have cloned a repository with an existing commit history, you’ll probably want to look back to see what has happened. The most basic and powerful tool to do this is the `git log` command.

## Sharing and Updating Projects 
### git remote 查看远程仓库
To see which remote servers you have configured, you can run the `git remote` command. It lists the shortnames of each remote handle you’ve specified. If you’ve cloned your repository, you should at least see `origin` — that is the default name Git gives to the server you cloned from:

#### git remote -v 查看远程仓库的url
You can also specify `-v`, which shows you the URLs that Git has stored for the shortname to be used when reading and writing to that remote.

#### git remote add <shortname> <url>
Adding Remote Repositories 添加远程仓库

We’ve mentioned and given some demonstrations of how the `git clone` command implicitly adds the `origin` remote for you. Here’s how to add a new remote explicitly. 

#### git remote rename <old> <new>
Renaming and Removing Remotes 重命名和删除远程仓库
It’s worth mentioning that this changes all your remote-tracking branch names, too. 
#### git remote remove <name>
If you want to remove a remote for some reason — you’ve moved the server or are no longer using a particular mirror, or perhaps a contributor isn’t contributing anymore — you can either use `git remote remove` or `git remote rm`:

### git fetch 从远程仓库拉取（后续需要手动merge）
Download objects and refs from another repository

### git pull
Fetch from and integrate with another repository or a local branch

### git push
Pushing to Your Remotes 提交到远程仓库

When you have your project at a point that you want to share, you have to push it upstream. The command for this is simple: `git push <remote> <branch>`. If you want to push your `master` branch to your `origin` server (again, cloning generally sets up both of those names for you automatically), then you can run this to push any commits you’ve done back up to the server:

```shell
git push origin master
```
#### git push <remote> -d <branch> 删除远程分支


## Patching
### rebase
Reapply commits on top of another base tip
For example, if you want to reorder the last 5 commits, such that what was HEAD~4 becomes the new HEAD. To achieve that, you would call git rebase like this:
```
git rebase -i HEAD~5
```
### github
下载zip是没有版本历史的

2021年之后已经不只是用户名密码来push了，只能通过tokens


## Administration
### git gc 优化仓库，清除不必要文件



## reference
https://git-scm.com/docs
