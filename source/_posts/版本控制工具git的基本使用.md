---
title: 版本控制工具git的基本使用
date: 2021-10-26 20:19:46
tags: git
categories: git
---

### 什么是版本控制工具？

git 是一个分布式版本控制工具，顾名思义，是一个控制项目版本管理的工具，记录和备份版本以及回撤到不同版本等操作

### git本地仓库的工作流和工作区域

git 的工作区域分为三种，如下表所示：

| 工作区域     | 说明                                    |
|----------| -------------------------------------- |
| 工作区      | 本地的项目目录，也就是实际的工作目录    |
| 暂存区（索引区） | 一个缓存区域，临时保存的改动            |
| git 仓库   | 最终暂存区的文件都会被提交到本地git仓库 |

git 操作文件时候，工作流顺序下表所示：

| 状态            | 说明                                 |
|---------------| ------------------------------------ |
| modified（已修改） | 本地文件已修改了，还未被保存到暂存区 |
| staged（已暂存）   | 本地文件被保存在了暂存区             |
| committed（已提交） | 本地文件被提交到本地git仓库了        |

**注意，这里的修改是比较广义的。删除、编辑、增加都是属于修改**

### git 本地操作的常用命令

* 配置提交时所使用的个人信息

  ```bash
  git config --global user.name "raoyingjun" // 用户名
  git config --global user.email "raoyingjun@foxmail.com" // 邮箱
  ```

  如果 `--global` 参数不存在，配置的用户信息仅在该仓库有效

* 初始化本地 git 仓库

  ```bash
  git init
  ```

  该命令在指定目录下初始化本地 git 仓库。该目录下将会生成一个 `.git` 隐藏文件夹。就可以开始进行git的使用了

* 查看文件的状态

  ```bash
  git status
  ```

  结果包含 `Untracked files` 或者说明文件已修改但未被提交到暂存区

* 添加文件到暂存区

  ```bash
  git add <file>
  ```

  `file` 为要被添加到暂存区的文件名。返回的结果包含 `Changes to be committed` 说明文件被添加到了暂存区，等待被提交到本地git仓库

* 提交更改到本地git仓库

  ```bash
  git commit
  ```

  该命令将会拉起安装 git 时所选择的默认编辑器，在编辑器内写入本次提交的说明。结果显示 `working tree clean` 说明工作区和暂存区是干净的，没有待暂存或待提交的文件。文件已经提交到了git本地仓库

  指定 `-m` 参数可以直接写入提交说明，不会拉起编辑器，比较方便快捷，命令如下

  ```bash
  git commit -m <description>
  ```

  `description` 为提交时的说明

  指定 `-a` 参数设置修改文件后无需执行 git add 命令，直接提交。将会拉取编辑器，在编辑器写入提交说明，命令如下

  ```bash
  git commit -a
  ```

  可以同时指定 `-am` 将add添加到暂存区操作和commit提交操作合并到一起。或者使用 `git commit * -m ` 也可以达到同样的效果

  ```bash
  git commit -am <description> 
  // 或者
  git commit * -m <description> 
  ```

  `description` 为提交时的说明

* 查看提交日志记录信息

  使用 `git log` 查看提交的日志记录信息，**该命令只能查看到当前版本为止的记录**

  ```bash
  HASEE@Royin MINGW64 ~/Desktop/GitProject (master)
  $ git log
  commit 73ad93b19df64c9b79b3ae886ddf63ab1daa8b0d (HEAD -> master)
  Author: raoyingjun <raoyingjun@foxmail.com>
  Date:   Wed Mar 31 17:10:31 2021 +0800
  
      本次提交的说明
  ```

  使用 `git log --pretty=oneline` 查看提交的日志记录信息

  ```bash
  HASEE@Royin MINGW64 ~/Desktop/GitProject (master)
  $ git log --pretty=oneline
  73ad93b19df64c9b79b3ae886ddf63ab1daa8b0d (HEAD -> master) 本次提交的说明
  ```

  使用 `git log --oneline` 查看提交的日志记录信息

  ```bash
  HASEE@Royin MINGW64 ~/Desktop/GitProject (master)
  $ git log --oneline
  73ad93b (HEAD -> master) 本次提交的说明
  ```

  使用`git log --graph` 查看提交的日志记录信息。方便直观的查看分支合并的情况

  ```bash
  $ git log --graph
  *   commit 2819958ace45d4ba7377e81d539ce80ff78a16c8 (HEAD -> main)
  |\  Merge: 8467fbd 8d2e09d
  | | Author: raoyingjun <raoyingjun@foxmail.com>
  | | Date:   Thu Apr 1 18:15:52 2021 +0800
  | |
  | |   本次提交的说明
  | |
  | * commit 8d2e09d39e66fd3a29eb892d0346b7de4aa11adb (hotfix)
  | | Author: raoyingjun <raoyingjun@foxmail.com>
  | | Date:   Thu Apr 1 17:36:31 2021 +0800
  | |
  | |   本次提交的说明
  | |
  * | commit 8467fbddcffb1300f98396480290a07025def49f
  |/  Author: raoyingjun <raoyingjun@foxmail.com>
  |   Date:   Thu Apr 1 17:37:26 2021 +0800
  |
  |     本次提交的说明
  |
  * commit b4a6f5abf45d65e80b67d53da714cbccc9edb3f2 (origin/main, origin/hotfix)
  | Author: raoyingjun <raoyingjun@foxmail.com>
  | Date:   Thu Apr 1 09:39:57 2021 +0800
  |
  |     本次提交的说明
  |
  * commit ddf4e6131e6cb13ae67b99456ebe38fa96a3f7bc
    Author: raoyingjun <raoyingjun@foxmail.com>
    Date:   Wed Mar 31 23:53:54 2021 +0800
  
        本次提交的说明
  ```

使用 `git reflog` 查看提交的日志信息，**该命令可以查看所有版本的提交记录**

  ```bash
  HASEE@Royin MINGW64 ~/Desktop/GitProject (master)
  $ git reflog
  73ad93b (HEAD -> master) HEAD@{0}: commit: 本次提交的说明
  ```

* 从暂存区移除文件

  ```bash
  git restore --staged <file>
  ```

  `file` 为从暂存区移除的文件名

* 丢弃修改

  当文件被添加到暂存区，如果对文件进行了修改，使用以下命令来丢弃修改，回撤到文件被暂存时的状态

  ```bash
  git restore <file>
  ```

  `file` 为要恢复的文件名。

* 比较不同工作区域的文件

  使用 `git diff` 命令来比较不同区的文件的差异

    * 无参数传入，比较工作区和暂存区的差异

      ```bash
      git diff
      ```

    * 比较暂存区和`HEAD`的差异

      ```bash
      git diff --cached
      // 或者
      git diff --staged
      ```

    * 比较工作区和HEAD的差异

      ```bash
      git diff HEAD
      ```

    * 比较工作区和HEAD同名文件的差异

      ```bash
      git diff HEAD -- <file>
      ```

      `file` 为要比较的文件

    * 指定版本之间的比较

        * 比较最新的HEAD和前3次的HEAD的差异

          ```bash
          git diff HEAD^ HEAD
          ```

          `HEAD^` 表示前1个版本，`HEAD^^` 则表示前2个版本，以此类推

        * 比较最新的HEAD和前3个版本的比较

          ```bash
          git diff HEAD~3 HEAD
          ```

          `HEAD~1` 表示前1个版本，`HEAD~4` 就是前4个版本，数字为几就是前几个版本

        * 比较两个历史版本的差异

          ```bash
          git diff hash1 hash2
          ```

  命令返回的结果示例如下：

  ```bash
  HASEE@Royin MINGW64 ~/Desktop/GitProject (master)
  $ git diff
  diff --git a/text.txt b/text.txt
  index 0b4bf3f..f034430 100644
  --- a/text.txt
  +++ b/text.txt
  @@ -1,4 +1,5 @@
   第一行
  -第二行
  +我是第一个插入的行^M
   第三行
  +我是最后插入的行^M
  
  ```

  以下是对 `git diff` 命令返回的结果的释义：

    * `diff --git a/text.txt b/text.txt` 的`a/text.txt`表示变动前的版本，`b/text.txt`表示变动后的版本

    * `index 0b4bf3f..f034430`表示两个版本（a版本和b版本）的git哈希值

    * `100644`表示文件的属性和权限(`100`表示是普通文件，`644`同`linux`权限)

    * `--- a/text.txt`表示变动前的版本

    * `+++ b/text.txt`表示变动后的版本

    * `@@ -1,4 +1,5 @@`表示源代码的1~4行和目标文件的1~5行有差异

    * `-`表示减少的部分

    * `+`表示增加的部分

* 版本的切换

    * 切换到指定的版本

      ```bash
      git reset --hard <hash>
      ```

      `hash` 为要切换的版本的哈希值

    * 切换到前1个版本

      ```bash
      git reset --hard HEAD^
      ```

      `HEAD^` 表示前1个版本，`HEAD^^` 则表示前2个版本，以此类推

    * 切换到前两个版本

      ```bash
      git reset --hard HEAD~1
      ```

      `HEAD~1` 表示前1个版本，`HEAD~4` 就是前4个版本，数字为几就是前几个版本

* 删除文件

    * 在暂存区和工作区删除该文件

      ```bash
      git rm <file>
      ```

      `file` 为要删除的文件。该命令执行后无需再使用 `git add` 命令将删除操作添加到暂存区了，只用将本次删除提交到本地 git 仓库即可

    * 仅暂存区删除该文件

      ```bash
      git rm --cached <file>
      ```

      `file` 为要删除的文件。在工作区的该文件仍然保留

* 工作区文件误删的补救

    * 从本地git仓库拉取一份回工作区

      ```bash
      git checkout <file>
      ```

      `file` 为要拉回的文件

    * 恢复工作区被删除的文件

      ```bash
      git restore <file>
      ```

      `file` 为要恢复的文件

* 分支介绍

  git提供了分支相关的操作，用来切换到不同的分支。master 一般是主干分支，一般功能增加、BUG 修复、多人协同开发等不会直接在 master 上进行，需要另辟分支进行处理，最后处理完后合并到master

* 创建分支

  ```bash
  git checkout -b <newbranch>
  // or
  git branch <newbranch>
  ```

  `newbranch` 为要创建的分支名称。使用第一种方式创建分支时同时会切换到该分支

* 切换分支

  ```bash
  git checkout <branchname>
  ```

  `branchname` 为要切换到的分支名称

* 删除分支

  ```bash
  git branch -d <branchname>
  ```

  `branchname` 为要删除的分支名称。**不能删除当前所在分支。如需删除，得先切换到其他分支，再执行删除**

* 查看分支

  ```bash
  git branch
  ```

  带 `*` 的表示当前所在的分支

  指定 `-v` 参数可以查看各个分支最后一次提交的信息，命令如下

  ```bash
  git branch -v
  ```

* 合并分支

  ```bash
  git merge <branchname>
  ```

  `branchname`为要被合并的分支名称，**合并到当前所在的分支**

* 重命名分支

  ```
  git branch -m <oldbranchname> <newbranchname>
  ```

  `oldbranchname` 和 `newbranchname` 分别为原分支名称和新分支名称。如果 `newbranchname` 分支已存在，指定 `-M` **代替** `-m` 可以强制重命名为已存在的分支

* 添加远程仓库

  ```bash
  git remote add <remotename> <url>
  ```

  `remotename` 为远程仓库的别名，`url` 为远程仓库的地址


* 查看所有的远程仓库别名

  ```bash
  git remote
  ```

  指定 `-v` 参数同时显示其远程仓库所对应的地址 `url`

  ```bash
  git remote -v
  ```

* 删除远程仓库

  ```bash
  git remote rm <remotename>
  ```

  `remotename` 为要删除的远程仓库的名称

* 修改远程仓库名称

  ```bash
  git remote rename <oldremotename> <newremotename>
  ```

  `oldremotename` 和 `newremotename` 分别表示旧名称和新名称

### git 远程仓库的常用命令

* 从远程仓库克隆项目到本地

  ```bash
  git clone <url>
  ```

  ```bash
  `url`为远程仓库的地址
  ```

* 取回远程仓库最新内容

  ```bash
  git fetch <remotehost> <remotebranch>
  ```

  使用 `git fetch <remotehost> <remotebranch>` 将远程仓库的的最新内容全部取回本地。`remotehost` 为远程仓库的地址或远程仓库的别名，`remotebranch` 为远程分支名

  如果仅指定了`remotehost`，则将`remotehost`所对应的远程仓库与本地当前同名分支的最新内容取回到本地当前分支，命令如下

  ```bash
  git fetch <remotehost>
  ```

  **`fetch` 操作不会对本地仓库做任何修改，仅仅是下载到本地**

* 将使用 `fetch` 命令下载到本地的内容合并到本地仓库

  ```bash
  git merge <remotehost>/<remotebranch>
  ```

  `remotehost` 为远程仓库的地址或远程仓库的别名，`remotebranch` 为远程分支名。**合并到当前所在分支**

* 查看远程分支

  ```bash
  git branch -a
  ```

  同时也会显示本地的分支。**在查看远程分支时，查看的是数据的快照，也就是上一次调用 `git fetch` 的结果。并没有与远程仓库实时的连接，也就是查看到的远程分支不一定是最新的，请先使用`git fetch`
  以确保获取到的是最新内容**

* 推送本地分支到远程仓库

  ```bash
    git push <remotehost> <localbranch>:<remotebranch>
  ```

  `remotehost` 为远程仓库的地址或远程仓库的别名，`localbranch` 和 `remotebranch` 分别对应本地分支名和远程分支名。如果本地分支名和远程分支名相同，则可以略写为：

    ```bash
  git push <remotehost> <localbranch>
    ```

  指定`-u`参数同时指定默认远程仓库和分支，直接使用 `git push` 即可，命令如下：

    ```bash
  git push -u <remotehost> <localbranch>
    ```

  **则后面无参数的推送，拉取等命令可以无需加任何参数，默认使用在这时使用 `-u` 所指定的远程仓库和分支** 。对于没有携带任何参数的推送，默认推送到当前分支。如果需要推送到其他主机或分支，请使用完整的`push`命令

  如果要推送当前所在的本地分支到远程仓库同名分支，则可以直接使用以下命令：

  ```bash
  git push <remotehost>
  ```

  `remotehost` 为远程仓库的地址或远程仓库的别名

* 删除远程分支

  ```bash
  git push <remotehost> :<remotebranchname>
  // 或者
  git push <remotehost> --delete <remotebranchname>
  ```

  `remtoehost` 为远程仓库的地址或远程仓库的别名，`remotebranchname` 为要删除的远程分支的名称

* 拉取远程分支到本地

  ```bash
  git checkout -b <localbranch> <remotehost>/<branchname>
  ```

  `localbranch` 为远程分支拉取到本地后的分支名，`remotehost` 为远程仓库的地址或远程仓库的别名，`branchname`
  为要被拉取到本地的远程仓库的分支名。该命令只适用于当在远程仓库存在该分支，并且通过 `git fetch` 操作下载到了本地，且本地并没有该分支时

* 拉取远程仓库内容到本地

  `pull` 操作是将 `fetch` 和 `merge` 操作合并在一起，关系约等于 `pull = fetch + merge`，具体的命令如下：

  ```bash
  git pull <remotehost> <remotebranch>:<localbranch>
  ```

  `remotehost` 为远程仓库的地址或远程仓库的别名，`remotebranch` 为要拉取的远程仓库的分支名称，`localbranch` 为要被合并的分支名称。如果本地分支名和远程分支名相同，则可以略写为：

  ```bash
  git pull <remotehost> <localbranch>
  ```

  如果要从远程仓库拉取的分支名和本地仓库当前所在分支名同名，则可以直接使用以下命令

  ```bash
  git pull <remotehost>
  ```

  `remtoehost` 为远程仓库的地址或远程仓库的别名