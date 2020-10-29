https://www.liaoxuefeng.com/wiki/896043488029600/1163625339727712

# 在gitee上创建项目

在码云首页顶部，下图所示，右上角头像旁边的加号，鼠标移上去会显示下拉的，点击“新建项目”。![image-20201028211356701](img/image-20201028211356701.png)

填写好项目的名称、路径等，然后点击“提交”

# git生成SSH密钥

打开Git Base Here然后输入下面命令

```shell
cd
```

然后输入：

```shell
ssh-keygen.exe
```

然后按回车，再次按回车，在回车，按三次回车：

![img](img/20190508091058616.png)

即可看到密钥，

C:\Users\Administrator\.ssh\id_rsa.pub

从该文件中复制密钥

点击SSH公钥

![image-20201028214005427](img/image-20201028214005427.png)

右侧的添加公钥，标题随便填写，公钥 里面将上面我们复制的那个本地密钥粘贴到这里，然后点击“确定”即可。这样我们就有权限对自己在码云上的项目进行读写操作了。

# 建立本地仓库

新建文件夹，右键---Git bash here

![image-20201028214332336](img/image-20201028214332336.png)



# 提交第一行代码

##  方法1

先将仓库clone到本地，修改后再push到 Gitee 的仓库仓库

```shell
$ git clone https://gitee.com/用户个性地址/HelloGitee.git #将远程仓库克隆到本地
```

在克隆过程中，如果仓库是一个私有仓库，将会要求用户输入 Gitee 的账号和密码。按照提示输入即可。

当然，用户也可以通过配置本地的git配置信息，执行`git config`命令预先配置好相关的用户信息，配置执行如下：

```shell
$ git config --global user.name "你的名字或昵称"
$ git config --global user.email "你的邮箱"
```

修改代码后，在仓库目录下执行下面命令

```shell
$ git add . #将当前目录所有文件添加到git暂存区
$ git commit -m "my first commit" #提交并备注提交信息
$ git push origin master #将本地提交推送到远程仓库
```

## 方法2

先创建仓库

```shell
$ git init 
$ git remote add origin https://gitee.com/用户个性地址/HelloGitee.git
```

这样就完成了版本的一次初始化。接下去，进入你已经初始化好的或者克隆仓库的目录,然后执行：

```shell
$ git pull origin master
```

修改/添加文件，否则与原文件相比就没有变动。

```shell
$ git add .
$ git commit -m "第一次提交"
$ git push origin master
```

# git同步到github和gitee

* 先删除已关联的名为origin的远程库：

```shell
git remote rm origin
```

* 然后，再关联GitHub的远程库：

```shell
git remote add github git@github.com:chloneda/demo.git
```

* 接着，再关联码云的远程库：

```shell
git remote add gitee git@gitee.com:chloneda/demo.git
```

修改.git文件夹内的config文件：

```text
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
[remote "origin"]
    url = git@github.com:chloneda/demo.git
    fetch = +refs/heads/*:refs/remotes/github/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
```

将上述文件内容[remote "origin"]内容复制，修改origin名称，内容如下：

```text
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
[remote "github"]
    url = git@github.com:chloneda/demo.git
    fetch = +refs/heads/*:refs/remotes/github/*
[remote "gitee"]
    url = git@gitee.com:chloneda/demo.git
    fetch = +refs/heads/*:refs/remotes/gitee/*
[branch "master"]
    remote = origin
    merge = refs/heads/master
```

* 查看远程库

通过以上两种方式的任一种方式配置完成后，我们用`git remote -v`查看远程库信息：

```shell
gitee   git@gitee.com:chloneda/demo.git (fetch)
gitee   git@gitee.com:chloneda/demo.git (push)
github  git@github.com:chloneda/demo.git (fetch)
github  git@github.com:chloneda/demo.git (push)
```

* 上传代码

```shell
git add .
git commit -m "update"
```

* 提交到github

```shell
git push github master
```

* 提交到码云

```shell
git push gitee master
```

* 更新代码

```shell
# 从github拉取更新
git pull github

# 从gitee拉取更新
git pull gitee
```

