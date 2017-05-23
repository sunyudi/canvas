# Git -版本控制工具

## 分支
- 查看分支：`git branch`，当前分支会标有一个`*`

- 创建分支：`git branch [分支名称]`
    + 分支中的代码，与创建那一刻主分支中的内容完全相同

- 切换分支：`git checkout [分支名称]`

- (简写)创建并切换分支：`git checkout -b [分支名称]`

- 合并分支：`git merge [分支名称]`，即：将其他分支合并到当前分支

- 删除分支：`git branch -d [分支名称]`

### 合并分支冲突
- 注意：合并分支时出现冲突只能手动处理文件，然后，再次提交

```
如果在一个从分支中做了修改，然后，在主分支中也做了修改。
此时，将这个从分支合并到主分支的时候，就会出现合并冲突的问题！
```

### 分支的说明
- 1 公司开发的项目都是由多个分支组成：主分支 + dev分支
- 2 项目经理新建项目仓库，所有的程序员都从这个仓库中获取代码，完成开发任务
- 3 项目经理：搭建设计仓库，创建master分支，以及dev分支（以及 debug分支等）
- 4 所有的程序员在 dev分支 上进行开发，并且还有自己维护的分支
- 5 程序员在分支上完成开发任务后，会提交合并请求
- 6 项目经理安排测试，如果没有问题了，最后才会与 master 分支合并


## github
- [github官网](https://github.com/)
- [开源中国-Git](https://git.oschina.net/)

```
在 GitHub 上免费托管的 Git 仓库，
任何人都可以看到喔（但只有你自己才能改）。
所以，不要把敏感信息放进去。
```

### github与git
- 1 git 是一个版本控制工具
- 2 github就是一个网站，这个网站提供了 git 服务器的功能

### 将代码提交到远程仓库（HTTPS）
- 1 在本地创建仓库
    + `git init`
    + `git config`
- 2 新建 README.md 文件，并输入任意内容
- 3 将 README.md 提交到本地
    + `git add`
    + `git commit`
- 4 在github中新建仓库，并拿到仓库地址
- 5 使用命令 `git push [仓库地址] master` 提交内容到github的默认分支
- 6 刷新github仓库页面，在线修改 README.md 文件，并提交
- 7 使用命令 `git pull [仓库地址] master` 获取仓库中的最新内容


### 获取远程仓库内容
- 命令：`git pull [仓库地址] [分支名称]` 获取远程仓库最新内容

- 命令：`git clone [仓库地址] [自定义本地仓库名]` 将整个仓库克隆到本地
    + 实例：`git clone git://github.com/jquery/jquery.git myJQ`

### 简化操作
- 1 `git remote add origin [仓库地址]`
    + 作用：使用origin代替 仓库地址 ，方便操作
    + origin就相当于js的变量，[仓库地址]就相当于变量的值
- 2 `git push -u origin master`
    + 作用：`-u`参数将origin与master连在一起
- 3 使用简化命令 `git push origin` 就代替原来："git remote add origin [仓库地址]"


### SSH介绍
- 非对称加密、公钥和私钥

```
GitHub 需要识别出你推送的提交确实是你推送的，而不是别人冒充的，
而 Git 支持 SSH 协议，所以，GitHub 只要知道了你的公钥，
就可以确认只有你自己才能推送，从而省去每次输入密码的操作。

可以同时设置多个SSH key，比如：你可以在公司电脑提交需要一个key，
回家后自己的电脑提交也需要一个key

ssh是一种安全的传输模式
github要求推送代码的用户是合法的，所以每次推送时候都要输入账号密码，
用以验证你是否为合法用户，为了省去每次都要输入密码的步骤，采用shh公钥，密钥
也就是你说的sshkey来验证你是否为合法用户
在你的电脑生成了一个唯一的ssh公钥和私钥，公钥放到github上面，当你推送的时候，git就会
匹配你的私钥是否跟github上面的公钥是配对的，正确就认为你是合法的，允许推送。

sshkey可以理解为是你的身份标识，放在github上面表明你是这个项目的一个开发人员，但是别
人是可以截获的，你本机的私钥别人就无法截获，sshkey就可以保证每次传输都是安全的。
```

### 将代码提交到远程仓库（SSH）
- 1 创建SSH Key：`ssh-keygen -t rsa`
- 2 在文件路径 `C:\用户\当前用户名\` 找到 `.ssh` 文件夹
- 3 文件夹中有两个文件：
    + 私钥：`id_rsa`
    + 公钥：`id_rsa.pub`
- 4 在 `github -> settings -> SSH and GPG keys`页面中，新创建SSH key
- 5 粘贴 公钥 `id_rsa.pub` 内容到对应文本框中
- 5 在github中新建仓库或者使用现在仓库，拿到`git@github.com:用户名/仓库名.git`
- 6 此后，再次SSH方式与github“通信”，不用输入密码确认身份了

### 最佳实践
- 先获取再提交，即：先`pull`再`push`

- 获取跟新的其他方式：`fetch` 
- [pull和fetch的区别](http://ruby-china.org/topics/4768)


## github搭建博客
- 使用github服务器的 `gh-pages` 分支

```
1 在本地工作目录使用git初始化 `git init`
2 创建自己的博客项目
3 将创建好的博客添加到暂存区 `git add [文件路径]`
4 本地提交： `git commit -m "第一个博客"`
5 创建分支：`git branch gh-pages` 分支名称固定！
6 切换分支：`git checkout gh-pages`
7 提交到github：`git push [github仓库地址] gh-pages`
8 查看github中对应的仓库中，是不是提交到了 "gh-pages" 分支
9 访问：<github用户名>.github.io/<仓库名>/<文件名>

10 默认会访问 index.html 
```

- 动态页面：.jsp / .php / .asp / .aspx

## Git软件（GUI 图形化界面）
- SourceTree / TortoiseGit
- [TortoiseGit使用教程](http://backlogtool.com/git-guide/cn/)


## Git -其他操作

### 文件对比
- 命令：`git diff`：将工作区与暂存区或者仓库对比
- 说明：如果暂存区没有文件，就会将工作区代码与上一次提交对比
    + 1 工作区 与 暂存区对比
    + 2 工作区 与 仓库  对比

- 命令：`git diff --cached`：将当前暂存区与仓库对比
- 命令：`git diff [版本号1] [版本号2] [对比的文件路径]`
    + 对比仓库区两次提交的差异

### 撤销和删除
- `git reset HEAD 文件名` 从暂存区撤销（结果：变为 未 add 状态）
- `git checkout -- test.txt` 撤销文件变化
    + 一种是 readme.txt 自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
    + 一种是 readme.txt 已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
- `rm [文件名称]`：删除文件（物理删除）
- `git rm [文件名称]`：从仓库中删除文件
- `git rm --cached [文件名称]`：从暂存区删除文件

### 结构说明
```
hooks：  存储钩子的文件夹
logs：   存储日志的文件夹
refs：   存储指向各个分支的指针（SHA-1标识）文件
objects：存放git对象
config： 存放各种设置文档
HEAD：   指向当前所在分支的指针文件路径，一般指向refs下的某文件
```
