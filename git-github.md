### git-github

#### 1.	团队协作开发

github口令：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

定义：由团队发起人 通过向心仪组员发送邀请函，邀请加入团队。在github上 settings->manger access->输入邀请人账号->复制邀请函(实质是链接)->发送给成员->成员打开链接->是否接受邀请

![image-20210528170353571](C:\Users\26728\AppData\Roaming\Typora\typora-user-images\image-20210528170353571.png)

push:将本地仓库的代码推送到远程库

pull:将远程库中的代码拉取到本地库进行更新 

clone:将远程库中的代码克隆到本地，从无到有

克隆会做如下三件事：1.克隆远程库代码 2.初始化本地库 3.创建别名

本地库修改后：

		1. 添加暂存区 ： git add .
  		2. 提交本地库：git commit -m "说明信息" 
  		3. 推送远程库:   git push 别名/链接 分支

#### 2.	跨团队开发

![image-20210528170718157](C:\Users\26728\AppData\Roaming\Typora\typora-user-images\image-20210528170718157.png)

1. fork:叉子将别人远程库中的代码搬到自己远程库中,github右上角

   ​	修改后发送 pull request等待仓库主人同意请求

   ​	仓库主人审核代码无误后，同意合并请求

   ​	主人远程仓库更新成功

   pull request:向另一个团队发送拉取请求

#### 3.	git远程仓库别名

命令行：git remote add 别名 仓库网址

切换分支：git checkout 分支名

将本地库代码推送到远程库:	git push 别名/链接 分支名

将远程库代码拉取到本地库：git pull 别名/链接 分支名

合并分支：git merge 分支名 (将指定的分支合并到当前分支上)



#### 4. idea集成git

1.配置git忽略文件 (不参与项目功能的文件)

必须以 xxx.ignore 为后缀 放用户目录下

2.在.gitconfig文件中引用忽略配置文件

[core]

​	excludesfile = 配置文件路径

3.idea 中加载git.exe

4.在导航栏 vcs ->import into version control->create git repository 自动追踪根目录

5.编辑代码后，添加暂存区：右击项目->git->add /提交本地库：commit

​	查看提交版本信息：左下角->version control->log

#### 5.	创建ssh

​     `$ ssh-keygen -t rsa -C Lming45H                                                 `    -C后面是描述信息

​	敲三次回车，用户目录下就有.ssh文件 进入文件      查看：`$ cat id_rsa.pub   

​	复制：公钥在github添加即可    

```
项目流程：
	1.架构师创建项目 托管到远程仓库，创建几个分支，主分支设置更改权限
	2.其他工程师从clone(初次)/pull(更新)项目，编码,add,commit->push到自己的分支上
	3.由组长在main分支上merge其他分支，最后push到main分支上
```

