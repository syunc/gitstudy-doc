##### 关于版本控制：
>    记录一个或若干文件内容变化，以便将来查阅特定版本修订情况

##### 发展：
1. 本地版本控制系统：复制整个项目文件夹从而形成新版本。


    优点=>简单

    缺点=>容易搞错
    
2. 集中化的版本控制系统：通过多台客户端连接服务器。


    优点=>每个人可以看到项目上其他人做了什么，管理员容易管理权限

    缺点=>一旦服务器挂了，谁都无法协同工作

3. 分布式版本控制系统：每次将代码仓库完整镜像下来，每个协作者都可在本地拥有一份完整的代码，并可在本地进行修改然后提交到远程仓库


#### Git和其他版本控制系统的差异

- 差异一：
    - GIT ：记录的是上一次每个变动文件的快照,直到文件产生新的变化git再进行新的快照保存,否则就建立一个指向上一文件的指针。
    - 其他：记录变化文件与上一次对比产生了哪些差量，是增量式


- 差异二：
    - GIT ：本地数据资源完备,不需要网络便可频繁更新;等到有网络再提交远程仓库,本地资源完备体现在：臂如查看提交历史，版本回退等。
    - 其他：有些需频繁请求网络以期得到数据资源进行数据更新


- 差异三：
    - GIT ：通过SHA1算法计算出指纹字符串记录文件内容或目录结构，可由远程代码仓库和本地版本文件进行比较，远程和本地都无更新状态下能验证文件的完整性。


#### 关于Git认知





一、工作区、版本库、暂存区的区分

	前提：初始化一个git仓库

-  工作区：本地可以看得见的目录
-  版本库：在隐藏目录.git下就是版本库
-  暂存区：Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个分支master，以及指向master的一个指针叫HEAD。

二、判断文件的三种状态

	前提：想要判断文件状态首先要将文件加入追踪
  
- 已提交：.git目录保存特定版本文件就属于已提交状态。
- 已暂存：如果对文件做了修改并放入暂存区属于已暂存状态。
- 已修改：对文件做了修改但未放入暂存区就属于已修改状态

### Git对象模型

##### 一、对象名

- 每个对象名都是对对象内容做SHA1哈希计算得到而来

	- 优点1 => git只要比较对象名就可以很快知道两个对象是否相同
	
	- 优点2 => 同样的内容在不同仓库拥有相同对象名
	
	- 优点3 => 通过对象内容得到SHA1哈希值与对象名比较判断对象内容是否正确

##### 二、对象组成

- 对象的类型包括：
	- blob：用于存储文件数据，通常是一个文件（通常是二进制文件，没有其他任何属性，文件名修改对其无影响）
	- tree：目录，管理tree和blob(子目录和文件)
	- commmit：一个commit指向一个tree，标记项目时间节点，(通常包含一个tree对象，父对象，作者，提交者，注释)
	- tag ：标记某一个提交方法
- 大小：内容大小
- 内容：取决于对象的类型



### Git工作流程

- 建立版本库
	1. `git init`
	2. `git clone + 远程仓库地址`
- 配置 Git
	
	查看配置信息：`git config --list`
	- 配置用户
	 1. 单个项目配置用户名：`git config user.name + <your_setting_username>`
	 2. 全局配置用户名：`git config --global user.name + <your_setting_username>`
	 3. 系统配置用户名：`git config --system user.name + <your_setting_username>`
	- 配置邮箱
	 1. 单个项目配置邮箱：`git config user.email + <your_email_address>`
	 2. 全局配置邮箱：`git config --global user.email + <your_email_address>`
	 3. 系统配置邮箱：`git config --system user.email + <your_email_address>`


		**ps：配置的用户名有就近原则，例如：在一个项目中，配置的用户名将覆盖全局配置的用户名,优先级：1>2>3;以上配置的作用，Git 用此区分不同的开发人员的身份。**

	- 配置文本编辑器：`git config --global core.editor emacs`
	- 配置差异分析工具：`git config --global merge.tool vimdiff`
	- 配置别名：`git config --global alias.st status`

	- 配置 `.gitignore文件`(作用：列出要忽略的文件列表，不被 Git 纳入版本管理)
	
		=> `.gitignore`格式规范：
		1. 空行和#都会被 git 忽略
		2. 可使用正则模式
		3. ' / ' 后说明要忽略的目录
		4. ' ! ' 在忽略文件中除了此文件
例如：

		![.gitignore](https://i.imgur.com/3yJy71F.jpg)


###  命令详解

###### 添加文件 #######

`git add <file>` 将文件添加至暂存区，即将文件变为追踪状态

`git add .` 将所有文件添加至暂存区


###### 撤销修改#####

`git checkout <file>` 将已追踪文件从modify状态变为未修改状态


###### 取消追踪 #######
`git reset HEAD <file>` 添加到了暂存区时，但想丢弃修改

`git reset --hard HEAD` 将文件恢复至之前未修改的工作区状态（hard 参数是将工作区和暂存区强制一致）



####### 提交到版本库 #######

`git commit -m 'comment'` 提交到版本库并添加注释

`git commit -am 'comment' 相当于 git add . 和 git commit 的结合 ,此时你就省去一条命令，直接将文件添加至暂存区`

----------

`git commit --amend` 如果自上次提交以来你还未做任何修改（例如，在上次
提交后马上执行了此命令），那么快照会保持不变，而你所修改的只是提交信息。

如果执行顺序如下：

 `$ git commit -m 'initial commit'`

 `$ git add forgotten_file`

 `$ git commit --amend`

那么将会将后来添加的文件一起提交。

----------


###### 查看差异 #######
`git diff file`	查看尚未暂存的文件更新了哪些部分

`git diff --cached||statged file`	查看已添加至暂存区的文件与版本库的区别


###### 移除文件 ######

情况一：未添加至暂存区（可以用 git rm 命令完成此项工作，连带从工作目录中删除指定的文
件）

	步骤1： rm filename（手工删除本地文件）
	步骤2： git rm filename（记录移除操作）
情况二：已添加至暂存区（可以用 git rm 命令完成此项工作，连带从工作目录中删除指定的文
件）

	步骤1： git rm -f filename
	或
	步骤1： rm filename
	步骤2： git rm filename
情况三：把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留
在当前工作目录中。 换句话说，你想让文件保留在磁盘，但是并不想让 Git 继续跟踪

	git rm --cached filename 

###### 文件改名 ######

`git mv old_name new_name`

Git 非常聪明能够意识到这是一次改名，实际上这条命令相当于进行了三条命令的操作，即
	
	$ mv old_name new_name
	$ git rm old_name 
	$ git add new_name 



`git cherry-pick + commit_id` 直接将节点复制合并到当前分支


### 远程仓库的使用 ###