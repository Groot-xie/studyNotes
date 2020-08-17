# 一、版本控制系统

+ 定义

  版本控制是一种记录一个或者若干个文件内容变化，以便将来查阅特定版本修订情况的系统(管理代码)

+ 分类

  > 本地版本管理系统

  1. 定义：在一台机器上，记录版本的不同变化
  2. 优点：保证内容不会丢失
  3. 无法解决多人合作的问题

  > 集中式版本控制系统(代表svn)

  1. 定义：有一个单一的集中管理的服务器(中央服务器)。协同工作的人通过客户端连接这台服务器，取出或更新
  2. 优点：多人合作开发
  3. 缺点：过渡依赖中央服务器，容易出现单点故障。过渡依赖网络

  > 分布式版本控制系统(代表git)

  1. 定义：把代码仓库完整地镜像下来(每个人电脑克隆服务器生成仓库)
  2. 优点：代码提交本地仓库。过渡依赖中央服务器得到解决、解决单点故障、解决多人协作





# 二、git 介绍

+ 定义：Git 是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或大或小的项目
+ 使用 git 的方式：
  1. git gui 图形化界面的方式
  2. git bash 命令行方式
  3. vi编辑器退出 :q!  :wq!





# 三、git 命令

## 3.1 `git init`

初始化一个 git 仓库，在当前项目下生成一个 git 文件夹



## 3.2 `git status`

查看文件的状态：如果是红色，说明工作区有代码需要提交。如果是绿色，说明暂存区中的文件需要提交

git 仓库分区

+ 工作区

  书写代码的地方，工作的目录就叫工作区

+ 暂存区

  暂时存储的区域。在 git 中，代码无法直接提交到仓库区，需要提交流程：工作区 --->  暂存区   --->  仓库区。暂存区的目的是避免错误

+ 仓库区

  将保存在暂存区的内容永久转储到 git 仓库中，生成版本号。可以任意的回退到某一个具体版本



## 3.3 `git add`

>   工作区 ---> 暂存区(Stage)

+ 作用：将文件由 工作区 添加到 暂存区

+ 命令：`git add 文件名/目录名`

  ```git
  // 添加当前目录下的所有文件
  git add .
  git add -A
  git add --all
  ```



## 3.4 `git commit`

>   暂存区 ---> 仓库区

+ 作用：将文件由 工作区 添加到 暂存区，生成版本号

+ 命令：`git commit -m “提交说明”`

+ 注意：不写提交说明会进入 vi 编辑器(退出 :q!)，不写提交说明会提交失败

+ 其它命令

  1. `git commit -a -m 提交说明`

     + 作用：由工作区 ----> 仓库区
     + 限制：已经暂存过的文件，可用此快速提交

  2. `git commit --amend -m 提交说明`

     修改最后一次的提交说明

  3. `git commit -am 提交说明`

     只限于修改，一步到仓库区



## 3.5 `git log`

+ 作用：查看提交日志

+ 美化：`git log --pretty=oneline`

+ 示例

  + `git log --oneline`

  + `git log -n4 --oneline`

    最近4条

  + `git log --all graph`

    图形化



## 3.6 `git relog`

+ 用来记录你的每一次命令
+ 如果进行了版本回退，那么被回退的版本通过 `git log` 就找不到了，可以通过 `git relog` 查看版本号
+ 穿梭前，用`git log`可以查看提交历史，以便确定要回退到哪个版本
+ 要重返未来，用`git reflog`查看命令历史，以便确定要回到未来的哪个版本



## 3.7 `git stash`

+ 作用：可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作

+ `git stash list` 查看隐藏列表
+ `git stash apply` 用于恢复。恢复后，stash内容并不删除，你需要用`git stash drop`来删除
+ `git stash pop` 恢复的同时把stash内容也删了
+ 恢复指定的stash： `git stash apply stash@{0}`



## 3.8 `git cherry-pick`

+ 作用：复制一个特定的提交到当前分支



## 3.9 `git mv 旧名 新名`

+ 作用：文件重命名





# 四、git 对比

> `git diff`

作用：可以查看每次提交内容的不同 

+ `git diff`

+ `git diff 文件名`

  查看工作区与暂存区的不同

+ `git diff --cached`

  查看暂存区和仓库区的不同

+ `git diff HEAD`

  查看工作区与仓库区的不同，HEAD表示最新的提交

+ `git diff 版本号 版本号`

  查看两个版本之间的不同





# 五、git 重置

> 撤销修改

- `git checkout -- 文件名`

  <font color=red> 丢弃工作区的修改 </font>，让这个文件回到最近一次`git commit`或`git add`时的状态

  `--` 很重要，没有它就变成了切换分支

- `git reset HEAD 文件名`

  <font color=red> 文件在暂存区 --->  工作区 </font>

- `git reset --hard 版本号/head~数字`

  退回之前版本(文件在仓库区)

- `git rm 文件名`

  删除文件



> `git reset`

+ 作用：版本回退，将代码恢复到已经提交的某一个版本中

+ 几种 `--`

  1. 默认为 `git reset --mixed HEAD^` 修改会被放回工作区
  2. `--soft` 修改会放到暂存区
  3. `--hard` 修改会直接被丢弃

+ 命令

  1. `git reset --hard` 版本号

     将代码回退到某个指定的版本

  2. `git reset --hard head~1`

     将版本回退到上一次提交

     head~1 上一次提交

     head~2 上上次提交

     ....
  
+ `git reset` 后用 `git push -f` 强推，这样会使远程仓库的回退到reset的版本，之后的版本都消失



> `git revert`

+ 作用：撤销修改，做一次重新的提交，生成一次新的 log

+ 命令

  1. `git revert 版本号`

     撤销某个具体版本

  2. `git revert 版本号..版本号`

     撤销区间版本 (前开后闭)

  3. `git revert --no-commit ...`
  
     revert 命令会对每个撤销的 commit 进行一次提交，--no-commit 后可以最后一起手动提交。





# 六、git 标签管理

- 定义：git 标签为版本库的快照

- 命令

  1. `git tag 标签名 [-m 备注]`

  2. `git tag`

     查看所有标签

  3. `git tag 标签名 [-m 备注] 版本号`

     给以前的版本打标签

  4. `git show 标签名`

     查看某个标签的信息

  5. `git tag -d 标签名`

     删除标签
   
  6. 将 tag 推送到远程仓库

     `git push orgin 标签名`
  
  
  
  



# 七、git 分支操作

+ 分支特点
  1. 分支之间互不干扰
  2. 分支可以合并
+ 分支创建
  1. 每次 `git commit` 都会在仓库生成一条记录
  2. 第一次 `git commit` 时，会自动生成一个分支 master 主分支
  3. <font color=ff0000> 分支本质上是一个指针 </font>。当前分支指向最后一次提交的版本。git 中使用 <font color=ff0000> HEAD(最新版本) </font> 指向当前分支。
+ 命令
  1. `git branch`   ----->   查看所有分支
  
  2. `git branch` 分支名   ----->   创建分支
  
  3. `git checkout` 分支名   ----->   切换分支
  
     切换分支这个动作，用`switch`更科学。因此，最新版本的Git提供了新的`git switch`命令来切换分支
  
     + 创建并切换到新的`dev`分支，可以使用：
  
     ```git
     $ git switch -c dev
     ```
  
     + 直接切换到已有的`master`分支，可以使用：
  
     ```git
     $ git switch master
     ```
  
  4. `git merge` 分支名   ----->   合并分支
  
  5. `git branch -d` 分支名   ----->   删除分支
  
  6. `git branch -D <name>` 丢弃一个没有被合并过的分支，强行删除。
  
  7. `git checkout -b` 分支名   ----->   创建并切换分支
  
  8. `git merge --no--ff -m 备注 login`   ----->   准备合并login分支，禁用`Fast forward`
  
     + `Fast forward` 这种模式下，删除分支后，会丢掉分支信息
  
     + `--no-ff` 参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。
  
  9. `git branch --set-upstream-to <branch-name> origin/<branch-name>`
  
     创建本地分支和远程分支的链接关系
+ git 合并冲突
  1. 对于同一文件，如果有多个分支需要合并时，容易出现冲突
  2. 如出现冲突只能手动处理，再次提交。一般做法，把自己的代码放到冲突代码的后面即可。





# 八、gitk：图形界面工具查看版本历史





# 九、探秘

```git
// 看类型 commit、tree、blob
git cat-file -t 版本号
// 看内容
git cat-file -p 版本号
```





# 十、git 忽视文件

- 在仓库的根目录创建一个 `.gitignore` 的文件(文件名固定)

- 将不需要被 git 管理的文件路径添加到 `.gitignore`

  \# 忽视 idea.txt 文件

  idea.text

  

  \# 忽视 css 下的所有 js 文件

  css/ *.js

  

  \# 忽视 css 文件夹

  css

  

  \# 忽视 css 下的所有文件

  css/\*.*





# 十一、git 配置全局用户名

+ 使用 `--global` 参数，配置全局的用户名和邮箱，只需配置一次即可。推荐配置 github 的用户名和密码

  `git cofig --global user.name ...`

  `git config --global user.email ...`

+ 查看配置信息

  `git config --list`
  
+ 几种 `--`

  - `git config --local`

    只对某个仓库有效（缺省等同于local）

  - `git config --global` 

    对当前用户的所有仓库有效

  - `git config --system`

    对系统所有登录的用户有效

+ 显示 config 的配置，加 `--list`

  ```git
  git config --list --local
  git config --list --global
  git config --list --system
  ```



# 十二、git 远程仓库( github )

git 和 github 没有直接的关系，git是一个版本控制工具， github 是一个代码托管平台，开源社区。是 git 的一个远程代码仓库

- github

  1. 定义：是一个面向开源及私有软件项目的托管平台，因为只支持 git 作为唯一的版本库格式进行托管。故名：github
  2. github 免费，代码所有人都可以看到，但只有自己可以修改。付费的可以隐藏
  3. 创建 git 项目时，不能有中文

  

## 13.1 `git clone`

- 作用：克隆远程仓库的代码到本地

- 命令：`git clone 远程仓库地址`

  克隆时会自带 orgin 地址，指向 clone 下的地址

  

## 13.2 `git push`

- 作用：将本地仓库中代码提交到远程仓库

- 命令：

  1. `git push 仓库地址 master`

  2. `git push -u orgin master`

     -u 表示可以默认使用，以后不加 orgin master

     

## 13.3 `git pull`

- 作用：将远程的代码下载到本地(更新)
- `git fetch` + `git merge` = `git pull`



## 13.4 `git remote`

- `git remote add 仓库别名 仓库地址`

  给仓库地址添加别名

- `git remote remove` 别名

  删除别名

- `git clone` 的仓库默认有一个 origin 的别名

- `git remote`

  查看远程仓库的信息

- `git remote -v`

  查看远程仓库更详细的信息



## 13.5 `git rebase`

- 特点：将分支的提交历史整理成一条直线，直观
- 缺店：本地的分支提交已经被修改过
- `git rebase -i 要修改的父版本版本号` <font color=red> 交互式命令 </font>





# 十三、SHH 免密登录

+ git 支持多种数据传输协议

  1. https 协议：需要输入用户名和密码
  2. shh 协议：可以配置免密登陆

+ SSH 免密登陆配置(这些命令需要在 bash 中敲)

  1. 创建 SSH key

     `ssh-keygen -t rsa`

  2. 在文件路径 `C:\用户\当前用户\` 找到 .ssh 文件夹

  3. 文件夹中有两个文件：私钥(id_rsa) / 公钥(id_rsa.pub)

  4. 在 github ---> settings ---> ssh and GPG keys 页面中创建 SSH key

  5. 粘贴公钥 id_rsa.pub 内容到对应文本框

  6. 在 github 中新建仓库或使用现在仓库拿到 `git@github.com:用户名/仓库地址.git`





# 十四、base 命令

- `vi 文件名`  预览文件
- `cp 文件路径 新文件名` 拷贝
- `cd 文件路径` 切换目录
- `pwd` 当前工作路径
- `ls -al` 查看当前目录
- `cat 文件` 输出文件内容
- `wq!` w写入 q退出
- `mkdir` 创建目录
- `echo '文件内容' > 文件名` 创建文件
- `mv 旧名 新名` 重命名

