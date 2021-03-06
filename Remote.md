## 远程仓库 Repo

> 远程仓库是指托管在因特网或其他网络中的你的项目的版本库。

- 查看远程仓库[及url]： `git remote [-v]`
- 添加远程仓库 ： `git remote add origin <url>`
    
        其中origin是该远程地址的类似别名,通过这个别名我们就能够不用输入一长串的url,
        你也可以换成其他名字,但是clone一个仓库后git会默认为我们建立一个origin别名,
        也可以在之后更换该别名，命令为：
        git remote rename old_name new_name
- 删除远程仓库：`git remote rm [remote_name]`
- 建立本地分支与远程分支的关联：`git branch --set-upstream-to=origin/develop`
- 删除远程分支：`git push origin --delete branch_name`
 
### 从远程仓库拉取和抓取

- `git fetch [remote_name]`：这个命令会访问远程仓库，从中拉取所有你还没有的数据。 执行完成后，你将会拥有那个远程仓库中所有分支的引用，可以随时合并或查看它并不会自动合并或修改你当前的工作。 当准备好时你必须手动将其合并入你的工作。


### 推送到远程仓库

- `git push [remote_name] [branch_name]` ：只有当你有所克隆服务器的写入权限，并且之前没有人推送过时，这条命令才能生效。 当你和其他人在同一时间克隆，他们先推送到上游然后你再推送到上游，你的推送就会毫无疑问地被拒绝。 你必须先将他们的工作拉取下来并将其合并进你的工作后才能推送。

### 推送标签
- 推送一个标签：`git push origin [tagname]`
- 推送全部标签：`git push origin --tags`