#git初步       
- 注.使用任何的git操作之前，都需要切换到git项目目录下
> 1. git status 查看当前git仓库状态
> 2. git init 初始化git仓库
> 3. git add file 修改file文件的状态为添加，并没有被提交，是存在缓存中
> 4. git rm --cached file 更改上面文件的状态为无状态(移除缓存)
> 5. git config user.name yu ;  
     git config user.email 1419699711@qq.com   
     添加git用户，在进行提交之前如果没有配置用户会报错,这是针对当前git仓库的  
	 git config --global user.name yu，可以使用 --global参数设置全局的
> 6. git commit -m message 提交并附带提交信息
> 7. git log 提交日志
> 8. git config core.autoclrf false 每次使用git命令(add,commit)的时候会报warning: LF will be replaced by CRLF in XXXX ，这是自动添加换行(linux下格式)引起的问题  
可以使用 --global参数设置全局的
> 9. git branch 查看当前分支的情况
> 10. git branch a 在当前的基础上新建一个分支名字为 a
> 11. git checkout a 切换分支到 a
> 12. git checkout -b a 综合上面两个命令，在当前基础上创建分支a并切换到a
> 13. git merge a 把a分支的内容合并到master分支，前提要先切换到master分支
> 14. git branch -d a 删除分支a
> 15. git branch -D a 强制删除分支a
> 16. git tag v1.0 为当前的状态新建一个v1.0的标签
> 17. git tag 查看历史tag记录
> 18. git checkout v1.0 切换到v1.0时的状态

#github初步
- 在向github提交代码前，需要ssh授权

1. 生成ssh key， 在Git Bash中使用命令: ssh-keygen -t rsa  
rsa 算法生成密钥，接着连续三个回车键（不需要输入密码），然后就会生成两个文件 id _rsa 和 id _rsa.pub ，而 id _rsa 是密钥（默认路径/c/Users/yu/.ssh/id_rsa），id _rsa.pub 就是公钥（/c/Users/yu/.ssh/id_rsa.pub）  
2. 在github上添加 ssh key  
进入自己的GitHub的设置界面，如图
![](http://i.imgur.com/hm1H3vi.png)
点击 New SSH Key 按钮，并把上述id_rsa.pub中的内容填入下面Key输入框中，如图
![](http://i.imgur.com/wBlVAEV.png)
点击 Add SSH Key 就可以了
3. 测试秘钥是否成功  
命令：ssh -T git@github.com, 第一次使用可能提示github无法被验证试过可信任，输入yes
![](http://i.imgur.com/hTdFI3V.png)
4. 开始跟GitHub打交道  
  
	1) clone GitHub上的项目到本地  
	在GitHub上创建一个新的项目(如果没有)名字是:github-study-test，执行如下命令  

	   ` git clone git@github.com:yuehongjie/github-study-test.git`
   
    这样就把项目 clone 到了本地，这个时候本地项目本身就已经是一个git 仓库了，不需要执行 git init 进行初始化，而且甚至都已经关联好了远程仓库，我们只需要在这个 github-study-test 目录下任意修改或者添加文件，然后进行add 和 commit，就像普通的本地git仓库一样

	如何获取项目地址:  在GitHub上进入项目，点击 Clone or download ,并选择 Use SSH

	![](http://i.imgur.com/k0aUzle.png)

	2) 向GitHub提交代码命令  

	`git push origin master`  
  
  
	这样就把本地项目提交到了 GitHub 远程 master 分支  
  
	有时候在push之前先pull一下，把远程最新的代码更新本地，命令  
  
	`git pull origin master`  
  
	3) 关联本地项目  
如果我们本地已有一个完整的git仓库，并且已经进行过很多次commit了，那么上面的在clone方式就不合适了,这时就需要我们把本地的git仓库关联到远程GitHub仓库上  
   第一步. 在GitHub上新建一个项目假设为test  
   第二步. 把本地项目假设是test2关联到远程test，使用命令:  

	`git remote add githuborigin git@github.com:yuehongjie/test.git`  
这样就把本地仓库和远程仓库关联好了，命令中的 githuborigin 是一个远程仓库的别名，可以随便起，起别名的原因是因为我们可能除了向GitHub提交，还可能向公司的的远程仓库提交，方便区别  
   第三步. 更新远程仓库到本地(当然这一步不是必须的，我这里这么做的原因是远程仓库新建的时候也创建了个README.md文件，而我本地没有)，命令:   
	`git pull githuborigin master`   
   第四步. 向GitHub(远程仓库)提交本地仓库的内容

	`git push githuborigin master`  
   这里提交到master分支，当然也可以提交到其他分支  
   p.s.可以使用 git remote -v 查看当前仓库关联了哪些远程仓库