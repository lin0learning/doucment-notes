### Git 基础概念

#### 1. 什么是 Git

Git 是一个开源的分布式版本控制系统，是目前世界上最先进、最流行的版本控制系统。可以快速高效地处理从小到大的项目版本管理。

特点：项目越大越复杂，协同开发者越多，越能体现出 Git 的高性能和高可用性！

#### 2. Git的特性

① 直接记录快照，而非差异比较

② 近乎所有操作都是本地执行

##### 2.1 Git 的记录快照

Git 快照是在原有文件版本的基础上重新生成一份新的文件，类似于备份。为了效率，如果文件没有修改，Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。

#### 3. Git 中的三个区域

使用 Git 管理的项目，拥有三个区域，分别是工作区、暂存区、Git 仓库。

#### 4. Git 中的三种状态

- 已修改 modified
- 已暂存 staged
- 已提交 committed

#### 5. 基本的 Git 工作流程

![image-20220707110556578](C:\Users\oringe\AppData\Roaming\Typora\typora-user-images\image-20220707110556578.png)

① 在工作区中修改文件

② 将想要下次提交的更改进行暂存

③ 提交更新，找到暂存区的文件，将快照永久性存储到 Git 仓库

### Git 基础配置

#### 1. 配置用户信息

安装完Git后，首先设置自己的用户名和邮件地址。

```git
git config --global user.name "****"
git config --global user.email "***@**.**"
```

Git 的全局配置文件地址：C:/User/用户文件夹/.gitconfig 文件

#### 2. 检查配置信息

```
# 查看所有的全局配置项
git config --list --global
# 查看指定的全局配置项
git config user.name
git config user.email
```

#### 3. 获取帮助信息

使用 git help <verb>

例：

```
# 打开 git config 命令的帮助手册
git help config
```

#### 4. 获取 Git 仓库的两种方式

① 将 尚未进行版本控制的本地目录转换为 Git 仓库

② 从其他服务器克隆一个已存在的 Git 仓库

#### 5. 在现有目录中初始化仓库

① 在项目目录中，通过鼠标右键打开 “Git Bash”

② 执行 git init 命令将当前的目录转化为 Git 仓库

#### 6. 检查文件的状态

git status命令查看文件所处状态。在状态报告中可以看到新建的index.html 文件出现在 Untracked files（未跟踪的文件）下面。

或以精简方式显示文件的状态：git status -s

#### 7. 跟踪新文件

```
git add index.html
```

#### 8. 提交更新

现在暂存区中有一个 index.html 文件等待被提交到Git 仓库中进行保存。可以执行 git commit 命令进行提交，其中 -m 选项后面是本次的提交消息，用来对提交的内容做进一步的描述

```
#example
git commit -m "新建了index.html文件"
```

#### 9. 对已提交的文件进行修改

目前，index.html 文件已经被 Git 跟踪，并且工作区和 Git 仓库中的 index.html 文件 内容保持一致。当我们修改了工作区中 index.html的内容之后，再次运行  git status 命令，会看到如下内容：

![image-20220707203220414](C:\Users\oringe\AppData\Roaming\Typora\typora-user-images\image-20220707203220414.png)

文件 index.html 出现在 Changes not staged for commit 下面，说明**已跟踪文件的内容发生了变化，但还没有放到暂存区。**

#### 10. 暂存已修改的文件

需要再次运行 git add 命令，改命令主要有如下3个功效：

1. 开始跟踪新文件
2. 把已跟踪、且已修改的文件放到暂存区
3. 把有冲突的文件标记为已解决状态

#### 11. 撤销对文件的修改

```
git checkout -- index.html
```

git撤销操作的本质：用 Git 仓库中保存的文件，覆盖工作区中指定的文件。

#### 12. 向暂存区中一次性添加多个文件

```
git add .
```

**今后在项目开发中，会经常使用者命令，将新增和修改过后的文件加入暂存区。**

#### 13. 取消暂存的文件

```bash
git reset HEAD 要移除的文件名称
```

commit之后，撤销commit的方法：

```bash
git reset --soft HEAD^
```

HEAD^的意思是上一个版本，也可以写成HEAD~1；如果进行了2次commit，想都撤回，可以使用HEAD~2。

- –mixed：不删除工作空间改动代码，撤销commit，并且撤销`git add . `操作。这个为默认参数，git reset --mixed HEAD^ 和 git reset HEAD^ 效果是一样的。

- –soft：不删除工作空间改动代码，撤销commit，不撤销git add .

- –hard：删除工作空间改动代码，撤销commit，撤销git add . 。注意完成这个操作后，就恢复到了上一次的commit状态。.

如果commit注释写错了，只是想改一下注释，只需要：`git commit --amend`，此时会进入默认vim编辑器，修改注释完毕后保存就好了。





#### 14. 跳过使用暂存区域

Git 标准的工作流程是 工作区 -> 暂存区 -> Git仓库，有时为了操作简便，可以跳过暂存区，直接将工作区中的修改提交到Git 仓库，这时候 Git 工作的流程简化为了 工作区 -> Git仓库。

Git 在提交的时候，给 git commit 加上 **-a**选项，Git就会自动把所有已经跟踪过的文件暂存起来一并提交，从而跳过 git add 步骤：

#### 15. 移除文件

从 Git 仓库中移除文件的方式有两种：

1. 从 Git 仓库和工作区中同时移除对应的文件
2. 只从 Git 仓库中移除指定的文件，但保留工作区中对应的文件

```
# 从 Git 仓库和工作区中同时移除 index.js 文件
git rm -f index.js
# 从 Git 仓库中移除 index.js 文件，但保留工作区中的 index.css 文件
git rm --cached index.css
```

#### 16. 忽略文件

一般情况下有些文件无需纳入 Git 的管理，也不希望它们出现在未跟踪文件列表。在这种情况下可以创建一个名为 **.gitignore** 的配置文件，列出要忽略文件的匹配模式。

#### 17. 查看提交历史

```
# 在上一行展示所有的提交历史
git log --pretty=oneline

# 使用 git reset --hard ,根据指定的提交ID回退到指定版本
git reset --hard <CommitID>
```

#### 小结

① 初始化 Git 仓库的命令

- git init

② 查看文件状态的命令

- git status 或 git status -s

③ 一次性将文件加入暂存区的命令

- git add .

④ 将暂存区的文件提交到 Git 仓库的命令

- git commit -m "提交的消息"

### Github - 远程仓库的使用

#### 1. 远程仓库的两种访问方式

有两种访问方式，分别是 HTTPS 和 SSH ，它们的区别是：

① HTTPS：零配置；但是每次访问仓库时，需要重复输入 Gtihub的账号和密码才能访问成功；

② SSH：需要进行额外的配置；但是配置成功后，每次访问仓库时，不需要重复输入 Github 的账号和密码

#### 2. 基于 HTTPS 将本地仓库上传到 Github

#### 3. SSH key

SSH key 由两部分组成，分别是：

① id_rsa （私钥文件，存放于客户端的电脑中即可）

② id_rsa.pub （公钥文件，需要配置到 Github 中）

### Git 分支

#### 1. 分支在实际开发中的作用

在进行多人协作开发的时候，为了防止互相干扰，提高协同开发的体验，建议每个开发者都基于分支进行项目功能的开发。

#### 2. main 主分支

在初始化本地 Git 仓库的时候， Git默认已经帮我们创建了一个名为 main的分支。通常我们把这个 main 分支叫做 主分支。

#### 3. 功能分支

由于程序员不能在 main 分支上进行功能的开发，就有了功能分支的概念。

功能分支指专门用来开发新功能的分支，临时从main 分支上分叉出来，最终需要合并到 main分支上。

#### 4. 查看分支列表

```
git branch
```

#### 5. 创建新分支

```
git branch 分支名称
```

#### 6. 切换分支 

```
git checkout 分支名称
```

#### 7. 分支的快速创建和切换

```
# -b 表示创建一个新分支
# checkout 表示切换到刚才新建的分支上
git checkout -b 分支名称
```

#### 8. 合并分支

```
# 1. 切换到 main 分支
git checkout main
# 2. 在 main 分支上运行 git merge 命令,将 login 分支的代码合并到 main 分支
git merge login
```

#### 9. 删除分支

当把功能分支的代码合并到 main 主分支上以后，就可以使用如下的命令。

```
git branch -d 分支名称
```

保证删除分支时 Git 不在被删除的分支上，否则会报错且删除失败。

#### 10. 遇到冲突时的分支合并

如果在两个不同的分支中，**对同一个文件进行了不同的修改**，GIt 就无法干净的合并它们。需要打开这些包含冲突的文件，手动解决冲突。

```
# 打开包含冲突的文件，手动解决冲突之后，再执行如下的命令
git add .
git commit -m "解决了分支合并冲突的问题"
```

### Git 分支 - 远程分支操作

#### 1. 将本地分支推送到远程仓库

第一次将本地分支推送到远程仓库，需要运行如下的命令：

```
# -u 表示把本地分支和远程分支进行关联，只在地此意推送的时候需要带 -u 参数
git push -u 远程仓库的别名 本地分支名称:远程分支名称

# 实际案例
git push -u origin payment:pay

# 如果希望远程分支的名称和本地分支名称保持一致，可以对命令进行简化：
git push -u origin payment
```

注意：第一次推送分支需要带 -u 参数，此后可以直接使用 git push 推送代码到远程分支。

#### 2. 查看远程仓库中所有的分支列表

```
git remote show 远程仓库名称
```

#### 3. 跟踪分支

从远程分支中，把远程分支下载到本地仓库中。

```
# 从远程仓库中，把对应的远程分支下载到本地仓库，保持本地分支和远程分支名称相同
git checkout 远程分支的名称
# 示例:
git checkout pay

# 从远程分支中，把对应的远程分支下载到本地仓库，并对下载的本地分支进行重命名
git checkout -b 本地分支的名称 远程仓库名称/远程分支名称
# 示例：
git checkout -b payment origin/pay
```

#### 4. 拉取远程分支的最新代码

```
git pull
```

#### 5. 删除远程分支

```
# 删除远程仓库中，指定名称的远程分支
git push 远程仓库名称 --delete 远程分支名称
# 示例:
git push origin --delete pay
```



实际遇到的一些问题：

1. warning: in the working copy of 'src/main.js', LF will be replaced by CRLF the next time Git touches it
   Git 可以在你提交时自动地把回车（CR）和换行（LF）转换成换行（LF），而在检出代码时把换行（LF）转换成回车（CR）和换行（LF）。 你可以用 git config --global core.autocrlf true 来打开此项功能。 如果是在 Windows 系统上，把它设置成 true，这样在检出代码时，换行会被转换成回车和换行：

   ```
   #提交时转换为LF，检出时转换为CRLF
   $ git config --global core.autocrlf
   ```

   

### Git-Conventional Commits

Conventional Commits，约定式提交。

```
<类型>[可选 范围]：<描述>

[可选 正文]

[可选 脚注]
```

类型：

- fix：修复了某个bug
- feat：新增了某个功能
- build：一些影响构建系统的更新
- chore：一些不更改核心代码的更新
- ci：变更了一些CI系统的配置
- docs：对文档做出了一些修改
- test：新增或修改测试文件
- refactor：重构了代码（但没有新增或修复东西）

### Git 贡献提交规范

- 参考 [vue](https://github.com/vuejs/vue/blob/dev/.github/COMMIT_CONVENTION.md) 规范 ([Angular](https://github.com/conventional-changelog/conventional-changelog/tree/master/packages/conventional-changelog-angular))

  - `feat` 增加新功能
  - `fix` 修复问题/BUG
  - `style` 代码风格相关无影响运行结果的
  - `perf` 优化/性能提升
  - `refactor` 重构
  - `revert` 撤销修改
  - `test` 测试相关
  - `docs` 文档/注释
  - `chore` 依赖更新/脚手架配置修改等
  - `workflow` 工作流改进
  - `ci` 持续集成
  - `types` 类型定义文件更改
  - `wip` 开发中

### 贡献

提一个 Issue 或者提交一个 Pull Request。

**Pull Request:**

1. Fork 代码!
2. 创建自己的分支: `git checkout -b feat/xxxx`
3. 提交你的修改: `git commit -am 'feat(function): add xxxxx'`
4. 推送您的分支: `git push origin feat/xxxx`
5. 提交`pull request`
