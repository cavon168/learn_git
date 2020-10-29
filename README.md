
## Windows系统上安装Git
1. 去Git官网下载安装包，默认安装，安装好了之后选择 **Git Bash** 打开。
2. 运行 `git --version` 命令，检查一下是否安装好了。
3. 运行 `mkdir learn_git` 命令，新建 **learn_git** 目录。
4. 运行 `cd learn_git` 命令，进入到此目录内。
5. 运行 `ls -al` 命令，查看目录里面的内容。
6. 运行 `git init` 命令，初始化Git仓库。
7. 运行 `ls -al` 命令，查看目录。
8. 配置仓库的用户和电子邮箱信息：<br>
    > 运行 `git config --global user.name "设置您的用户名"` 命令<br>
    > 运行 `git config --global user.email "设置您的电子邮箱"` 命令<br>
    > 运行 `git config --global --list` 命令，检查配置的结果
    
    <br>
## 完成一个简单的Git操作流程
1. 运行 `git status` 命令，查看Git仓库处于什么样的状态。
2. 运行 `pwd` 命令，查看learn_git目录的路劲。
3. 运行 `vim learn_git.html` 命令，在 learn_git 目录下面新建  learn_git.html 文件，也可手动创建。内容写好之后可以 `Ctrl + C` 看最后一行按照提示返回。
4. 运行 `git status` 命令，查看仓库的状态。
5. 运行 `git add learn_git.html` 命令，来跟踪learn_git.html文件。
6. 运行 `git commit -m "提交注释说明"` 命令，提交操作。
7. 运行 `git status` 命令，查看状态。
    > **状态：** 已修改（html） --> 已暂存（html）运行 git add 命令之后 --> 已提交（html）运行 git commit 命令之后。<br>
    > **对应区域：** 已修改 --> 工作区，已暂存 --> 暂存区，已提交 --> Git仓库。<br>
    > **解释：** 新建文件，或者对文件的编辑操作，都是在工作区中进行的，刚才新建了一个 html 文件，Git 能够检测到这里发生的变化，这也就是为什么当我们刚才新建完文件之后，运行 git status 会返回这样的信息。也就是说，当前这个文件处于已修改状态，而且它处于工作区，接下来我们按照git的提示，运行了 git add 命令，这个文件的状态就发生了变化，它从工作区被移到了暂存区，同时它的状态从已修改就变成了已暂存，这时候我们再运行 git status 命令，就显示已经暂存了，还会提示我们运行 `"git rm --cached <file>..."` 命令可以 **取消暂存** ，再然后我们又运行了 git commit 命令，这样文件的状态就从已暂存变成了已提交，同时从暂存区被移到了Git仓库区，再运行 git status 命令就会发现没有需要提交的内容。
8. 编辑 learn_git.html 文件，作为项目的1.0版本。
9. 运行 `git status` 命令，状态为已修改。
10. 运行 `git add .` 命令，加到暂存区。
11. 运行 `git status` 命令，从工作区移到暂存区。
12. 运行 `git commit -m "web1.0"` 命令，已提交。
13. 运行 `git log` 命令，可以显示历史的所有提交。

    <br>
## 将本地仓库同步到远程 GitHub 仓库
1. 打开GitHub仓库，添加一个仓库。
2. 点击右上角 **+ 图标** ，选择 **new repository**，新建仓库。
3. 填写仓库的名字 **Repository name**，比如：**learn_git**。
4. 一路采用默认，点击 **Create repository**。
5. 在GitHub给我们的提示信息里面，我们选择 **SSH协议**，
    > ### 为什么选用 **SSH协议** 呢？
    > 因为如果使用 **HTTPS协议** ，在之后 同步本地和远程仓库的时候，可能每次都要输入GitHub的用户名和密码。<br>
    > 使用 **SSH协议** ，只需要在一开始配置好公私钥就 OK 了，虽然第一次会麻烦一些，但是只需要麻烦这一次。<br>
    > 当然网上一些文章也会提示说，在 **HTTPS协议** 下，可以运行这一条命令：`git config --global credential.helper store` ，同样可以避免以后每次都输入用户名和密码，但是不建议这种方法，因为密码会明文保存在本地，这种操作很危险。当然如果用的苹果电脑的话，使用 **HTTPS协议** 也是可以的。<br>
6. 运行 `git remote add origin git@github.com:cavon168/learn_git.git` 命令。
   > `git remote add` ：给本地仓库添加一个远程仓库。<br>
   > **注意** ：当前要处于 **learn_git路劲下面** 。
7. 运行 `git remote` 命令，验证远程仓库是否添加成功。
8. 配置 **SSH协议** 公私钥：
    > a. 运行 `ssh-keygen -t rsa -C "425247833@qq.com"` 命令，直接采用一路向下回车。<br>
    > b. 公私钥创建好之后，切换到它提示的路劲下面去查看，注意这里的路劲是 **.ssh** 这个路劲 <br>
    > c. 运行 `cd /Users/edz/.ssh` 命令。<br>
    > d. 原型 `ls` 命令，当前有两个文件：id_rsa（私钥） / id_rsa.pub（公钥） 。**注意：私钥不要泄露出去** 。<br>
    > e. 运行 `cat id_rsa.pub` 命令，查看公钥里面的内容。<br>
    > f. 复制公钥里面的一长串字符内容，切换到 GitHub 页面点击图像下面的 **settings** ，选择 **SSH and GPS keys** 进入到这个菜单，点击 **New SSH key** 按钮新建一个 **SSH key** ，Title 可写可不写，**Key** 里面直接把刚才复制的公钥内容粘贴进来，点击 **Add SSH key** 按钮。<br>
9. 运行 `ssh -T git@github.com` 命令，测试本地和远程的 GitHub 是否已经能成功建立连接。
10. 回车输入 `yes` ，可以看到已经成功通过认证。
11. 运行 `cd "f:/dez/learn_git"` 命令，切换回 Git 仓库，learn_git目录下。
12. 运行 `git push -u origin master` 命令，可以看到分支是 master / main。
13. 回到 GitHub 上面验证是否推送成功，成功之后再编辑文件造轮子，重新常规提交操作流程。
14. 运行 `git status` 命令。
15. 运行 `git add .` 命令。
16. 运行 `git status` 命令。
17. 运行 `git commit -m "验证learn_git本地仓库是否成功的推送到GitHub远程仓库。"` 命令。
18. 运行 `git push -u origin master` 命令。

***此时学习Git就已经全部完成了，更加继续努力。***

<br>

> ## <color style="color: red;">**眼过千遍不如手过一遍***<color/>
