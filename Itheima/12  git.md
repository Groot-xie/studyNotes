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





# 二、git

+ 定义：Git 是一款免费、开源的分布式版本控制系统，用于敏捷高效地处理任何或大或小的项目
+ 使用 git 的方式：
  1. git gui 图形化界面的方式
  2. git bash 命令行方式
  3. vi编辑器退出 :q!  :wq!





# 三、git 命令

> `git init`

初始化一个 git 仓库，在当前项目下生成一个 git 文件夹



> `git status`

查看文件的状态：如果是红色，说明工作区有代码需要提交。如果是绿色，说明暂存区中的文件需要提交

git 仓库分区

+ 工作区

  书写代码的地方，工作的目录就叫工作区

+ 暂存区

  暂时存储的区域。在 git 中，代码无法直接提交到仓库区，需要提交流程：工作区 --->  暂存区   --->  仓库区。暂存区的目的是避免错误

+ 仓库区

  将保存在暂存区的内容永久转储到 git 仓库中，生成版本号。可以任意的回退到某一个具体版本



> `git add`  工作区 ---> 暂存区

+ 作用：将文件由 工作区 添加到 暂存区

+ 命令：`git add 文件名/目录名`

  ```git
  // 添加当前目录下的所有文件
  git add .
  git add -A
  git add --all
  ```



> `git commit`  暂存区 ---> 仓库区

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



> `git log`

+ 作用：查看提交日志
+ 美化：`git log --pretty=oneline`
+ git reflog 可以查看所有版本的信息操作





# 四、git 对比

> `git diff`

作用：可以查看每次提交内容的不同 

+ `git diff`

  查看工作区与暂存区的不同

+ `git diff --cached`

  查看暂存区和仓库区的不同

+ `git diff HEAD`

  查看工作区与仓库区的不同，HEAD表示最新的提交

+ `git diff 版本号 版本号`

  查看两个版本之间的不同



> 撤销修改

+ `git checkout -- 文件名`

  丢弃工作区的修改，让这个文件回到最近一次`git commit`或`git add`时的状态

+ `git reset HEAD 文件名`

  文件在暂存区 --->  工作区

+ `git reset --hard 版本号/head~数字`

  退回之前版本(文件在仓库区)

+ `git rm 文件名`

  删除文件





# 五、git 重置

> `git reset`

+ 作用：版本回退，将代码恢复到已经提交的某一个版本中

+ 命令

  1. `git reset --hard` 版本号

     将代码回退到某个指定的版本

  2. `git reset --hard head~1`

     将版本回退到上一次提交

     head~1 上一次提交

     head~2 上上次提交

     ....





# 六、git 忽视文件

+ 在仓库的根目录创建一个 `.gitignore` 的文件(文件名固定)

+ 将不需要被 git 管理的文件路径添加到 `.gitignore`

  \# 忽视 idea.txt 文件

  idea.text

  

  \# 忽视 css 下的所有 js 文件

  css/ *.js

  

  \# 忽视 css 文件夹

  css

  

  \# 忽视 css 下的所有文件

  css/\*.*





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
  4. `git merge` 分支名   ----->   合并分支
  5. `git branch -d` 分支名   ----->   删除分支
  6. `git checkout -b` 分支名   ----->   创建并切换分支
  7. `git merge --no--ff -m 备注 login`   ----->   准备合并login分支，禁用`Fast forward`
+ git 合并冲突
  1. 对于同一文件，如果有多个分支需要合并时，容易出现冲突
  2. 如出现冲突只能手动处理，再次提交。一般做法，把自己的代码放到冲突代码的后面即可。





# 八、git 远程仓库( github )

git 和 github 没哟直接的关系

git是一个版本控制工具

github 是一个代码托管平台，开源社区。是 git 的一个远程代码仓库



+ github

  1. 定义：是一个面向开源及私有软件项目的托管平台，因为只支持 git 作为唯一的版本库格式进行托管。故名：github
  2. github 免费，代码所有人都可以看到，但只有自己可以修改。付费的可以隐藏
  3. 创建 git 项目时，不能有中文

+ 命令

  > `git clone`

  + 作用：克隆远程仓库的代码到本地

  + 命令：`git clone 远程仓库地址`

    克隆时会自带 orgin 地址，指向 clone 下的地址

    

  > `git push`

  + 作用：将本地仓库中代码提交到远程仓库

  + 命令：

    1. `git push 仓库地址 master`

    2. `git push -u orgin master`

       -u 表示可以默认使用，以后不加 orgin master

       

  > `git pull`

  + 作用：将远程的代码下载到本地(更新)

    

  > `git remote`

  + `git remote add 仓库别名 仓库地址`

    给仓库地址添加别名

  + `git remote remove` 别名

    删除别名

  + `git clone` 的仓库默认有一个 origin 的别名

  + `git remote`

    查看远程仓库的信息

  + `git remote -v`

    查看远程仓库更详细的信息

  

  > `git rebase`

  + 特点：将分支的提交历史整理成一条直线，直观
  + 缺店：本地的分支提交已经被修改过





# 九、git 配置全局用户名

+ 使用 `--global` 参数，配置全局的用户名和邮箱，只需配置一次即可。推荐配置 github 的用户名和密码

  `git cofig --global user.name ...`

  `git config --global user.email ...`

+ 查看配置信息

  `git config --list`





# 十、git 标签管理

+ 定义：git 标签为版本库的快照

+ 命令

  1. `git tag 标签名 [-m 备注]`

  2. `git tag`

     查看所有标签

  3. `git tag 标签名 [-m 备注] 版本号`

     给以前的版本打标签

  4. `git show 标签名`

     查看某个标签的信息

  5. `git tag -d 标签名`

     删除标签

  

  

# 十一、SHH 免密登录

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



