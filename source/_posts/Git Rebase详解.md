### 介绍git rebase

Rebase，理解为“变基”，意思是“变更基底”。基于某分支（称为”基分支“）创建另一个分支（称为”待基变分支“），通过 rebase 操作，将待基变分支上的 Commit 暂存，然后将基分支上最新产生的 Commit 合并到待基变分支，最后将待基变分支上暂存的 Commit 合并到待基变分支

### 举例详解

Master 为主分支，同时在此是作为基分支，Feature 分支为基于 Master 创建的特性分支，同时作为待基变分支，两个分支对应的 Commit 记录如下：

Master 分支: A->B->M
Feature 分支: A->B->F1->F2

* 由上看出，Feature 分支是基于 Master 分支上的 Commit B 创建的

* Master 基于 Commit B新增 Commit M，Feature 分支基于 Commit B 新增 Commit F1、Commit F2

* 在 Feature 分支上执行 `git rebase Master`，首先暂存 Feature 分支的 Commit F1、Commit F2，接着将 Master 分支新产生的 Commit 进行 rebase 到 Feature 分支，即 Feature 分支: A->B->M，最后再将 Feature 分支暂存的 Commit 合并到  Feature 分支，也就是 A->B->M + F1->F2，即 A->B->M->F1->F2

* 原 Feature 分支 Commit F1、Commit F2 对应的 Commit ID, 在执行 rebase 命令后，Commit 内容不会变，但 Commit F1、Commit F2 会生成新的 Commit ID

### 注意事项

* Git Rebase 操作不会产生新的 Commit记录，这不同于 Git Merge
* Git Rebase 会改写历史 Commit 记录，也就是 rebase 这个过程会生成新的 Commit ID
