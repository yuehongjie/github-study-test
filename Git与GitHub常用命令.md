**p.s. 本文是跟着张哥的 GitHub 系列教程操作的，张哥微信公众号: googdev**

##git

注：在使用的任何的 git 命令前，都要切换到 git 项目目录下

-	**git init**  
	初始化一个 git 仓库

-	**git status**  
 	查看当前 git 仓库的状态

-	**git add <file\>**  
  	修改 file 文件的状态为添加，并没有提交，只是存在缓存区

-   **git rm --cached file**  
  	更改 add 后的文件的状态为无状态(从缓存区移除)

-   **git config user.name yu** 和 **git config user.email yuehongjie93@gmail.com**   
    添加 git 用户，在进行提交之前如果没有配置用户会报错,这是针对当前 git 仓库的  
    git config **--global** user.name yu ，可以使用 --global 参数设置全局的

-   **git commit -m message**  
    提交缓存区内容并附带提交信息  

-   **git log**  
	显示提交日志  

-   **git config core.autoclrf false**  
	解决每次使用 git 命令 ( add , commit ) 的时候会报 warning: LF will be replaced by CRLF in XXXX  
    这是自动添加换行 ( linux 下格式) 引起的问题，可以使用 **--global** 参数设置全局有效   

-   **git tag v1.0**  
	为当前的状态打个 v1.0 的标签  

-   **git tag**  
	查看历史 tag 记录 

-   **git branch**  
    查看当前分支的情况  

-   **git branch a**  
	在当前的基础上新建一个分支名字为 a  

-   **git checkout a**  
	切换分支到 a  

-   **git checkout -b a**  
    综合上面两个命令，如果 a 分支不存在，在当前基础上创建分支 a 并切换到 a  

-   **git checkout v1.0**  
	切换到 tag v1.0 时的状态  
      
-   **git checkout ffd9f2dd68f1eb21d36cee50dbdd504e95d9c8f7**  
	切换到某次 commit ，这个长序列是每次 commit 的 SHA1 值，可以使用 git log 查看  
      
-   **git checkout test.txt**  
	撤销 test.txt 的改变，注 checkout 命令只能撤销还没有 add 进暂存区的文件  

-   **git merge a** 和 **git rebase a**  
	把 a 分支的内容合并到 master 分支，前提要先切换到 master 分支，两个做法的区别是：  
	merge 是把 a 中的内容全部粗暴的合并进来，rebase 会先比较内容改变的顺序，再按顺序合并

-   **git branch -d a**  
	删除分支a  

-   **git branch -D a**  
	强制删除分支a   

-   **git config --global alias.co checkout**  
	**alias** 为 checkout 起别名为 co,然后在输入命令的时候，就可以使用 git co 替代 git checkout ,如果只针对当前仓库 global 不是必须的  

-   **git log 的 NB 的用法**  
	**git log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative**  
	格式化日志的输出，可以很清晰的展现日志信息和分支走向  
	这么难写却又牛逼的命令我们必须给起个别名：  
	**git config --global alias.lg "log --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit --date=relative"**   
	然后就可以使用 **git lg** 就可以了  

-	**git config --global color.ui true**  
	给git的输出着色  

-	**git config --global core.quotepath false**  
	设置显示中文文件名  
	在没设置显示中文名之前，我创建了一个新文件 中文名.txt ,然后使用 git status 查看一下显示如下：  
	![](http://i.imgur.com/PZkJzOS.png)  
	设置显示中文名后，显示如下:  
	![](http://i.imgur.com/JynuM6m.png)

-	**stash 命令**  
	使用场景，如你正在一个分支 a 上修改着代码什么的，但是这时候，有一个紧急的任务，需要你切换到另一个分支 b 去做些工作，  
	而 a 上的代码还是个半吊子，不想去 commit 甚至不想去 add ，这时候 **stash** 命令就大有用处了，**前提是没有执行 commit**  
	
	-	**git stash**  
	 	把当前分支没有 commit 的代码先暂存起来，这时使用 git status 会发现分支很干净
		![](http://i.imgur.com/qRFJVwT.png)  
	
	-	**git stash list**  
		可以看到此时暂存区多了一条记录  
		![](http://i.imgur.com/8WvlEZX.png)   
		暂存成功后，你就可以切换到 b 去做其他的功能  
		b 分支的事情做完后，就可以再切换回 a 分支，继续之前的工作
  
	-	**git stash apply**  
		![](http://i.imgur.com/bgGJ2DX.png)  
		执行后， a 分支之前的代码就又回来了，然后做好把暂存区的 stash 记录删除  

	-	**git stash drop**  
		就是把最近的一条 stash 记录删除， drop 后还可以跟 stash_id 来删除指定的记录 
		![](http://i.imgur.com/KWxvuMe.png)  

	-	**git stash pop**  
		这个命令相当于同时执行了 apply 和 drop ，谨慎起见，使用 git stash list 查看一下是否确实删除了该记录  
		![](http://i.imgur.com/EWTpUbq.png)  

	-	**git stash clear**  
		清空暂存区的所有记录，drop 只是删除一条，drop 后可以跟 stash_id 来删除指定的记录，不跟就是删除最近的
-	**冲突解决**  
	假设我在 a 分支和本地分支上同时修改了文件 test.txt ，在合并啊时候就会出现冲突  
	![合并冲突](http://i.imgur.com/BsLFOgz.png)  

	用git diff可以查看冲突    
	![](http://i.imgur.com/g3AIrH6.png)  

	解决冲突要做的就是修改冲突的文件 test.txt 为最终想提交的内容，并去掉其中的标识符   
	(标识符: ++<<<<<<< HEAD；++=======； ++>>>>>>>>)  
	修改然后 **add** 和 **commit**


---------------------------------------------------------

##GitHub

在向 GitHub 提交代码前，需要 SSH 授权，因此要创建 SSH Key

1.	生成 ssh key， 在 Git Bash 或者命令行中使用命令:
  
		ssh-keygen -t rsa  

	rsa 算法生成密钥，接着连续三个回车键（不需要输入密码），然后就会生成两个文件 id\_rsa 和 id\_rsa.pub  
	命令执行结果会告诉你文件默认路径, 其中 id\_rsa 是密钥（ /c/Users/yu/.ssh/id_rsa ）， id\_rsa.pub 就是公钥（ /c/Users/yu/.ssh/id\_rsa.pub ） 
 
2.	在github上添加 ssh key  
	进入自己的 GitHub 的设置界面，如图：
	![](http://i.imgur.com/hm1H3vi.png)  

	点击 New SSH Key 按钮，并把上述 id_rsa.pub 中的内容填入下面 Key 输入框中，如图：
	![](http://i.imgur.com/wBlVAEV.png)
	点击 Add SSH Key 就可以了

3. 测试秘钥是否成功  

		ssh -T git@github.com  

	第一次使用可能提示 github.com 无法验是否证可信任，输入 yes
	![](http://i.imgur.com/hTdFI3V.png)

4. 开始跟GitHub打交道  
  
	*	clone GitHub上的项目到本地 
 
		在GitHub上创建一个新的项目/仓库(或者用已有的)， 假设名字是： github-study-test ，执行如下命令  

	   		git clone git@github.com:yuehongjie/github-study-test.git
   
    	这样就把项目 clone 到了本地，这个时候本地项目本身就已经是一个 git 仓库了，不需要执行 git init 进行初始化  
		而且甚至都已经关联好了远程仓库，我们只需要在这个 github-study-test 项目下任意修改或者添加文件，然后进行 add 和 commit ，就像普通的本地 git 仓库一样

		如何**获取项目地址**：  在 GitHub 上进入项目，点击 Clone or download ，并选择  Use SSH

		![](http://i.imgur.com/k0aUzle.png)


	*	向 GitHub 提交代码命令  

			git push origin master  
  
		这样就把本地项目提交到了 GitHub 远程 master 分支  
  
		有时候在 **push** 之前先 **pull** 一下，把远程最新的代码**更新到本地**，命令  
  
			git pull origin master
 
  
	*	关联本地项目到 GitHub  
		如果我们本地已有一个完整的 git 仓库，并且已经进行过很多次 commit 了，那么上面的在 clone 方式就不合适了，这时就需要我们把本地的 git 仓库关联到远程 GitHub 仓库上  
   
		1.	在 GitHub 上新建一个项目假设为 test  
		
   		2.	把本地项目假设是 test2 关联到远程 test ，使用命令：  

				git remote add githuborigin git@github.com:yuehongjie/test.git
  
			这样就把本地仓库和远程仓库关联好了，命令中的 **githuborigin** 是一个远程仓库的**别名**，可以随便起  
			起别名的原因是因为我们可能除了向 GitHub 提交，还可能向公司的的远程仓库提交，方便区别  

   		3.	更新远程仓库到本地 
 
			这一步不是必须的，我这里这么做的原因是远程仓库新建的时候也创建了个 README.md 文件，而我本地没有，pull 命令：
   
				git pull githuborigin master  

  		4. 向 GitHub 提交本地仓库的内容

				git push githuborigin master 
  
   			这里我是提交到master分支，当然也可以提交到其他分支  

   	p.s.可以使用 git remote -v 查看当前仓库关联了哪些远程仓库  

--------------------------------------------------------
##git & GitHub

常用的操作命令：

**在 master 分支新建一个叫 develop 的分支**

	git branch develop

注：新建分支是基于当前所在的分支基础上进行的，即以上命令是基于 master 分支新建了一个叫 develop 的分支，此时 develop 分支跟 master 分支的内容完全一样

**切换到 develop 分支**

	git checkout develop

可以把上面两个步骤和合并，新建并自动切换到 develop 分支：

	git checkout -b develop

**把 develop 分支推送到远程仓库**

	git push origin develop

注：该命令执行时如果远程仓库没有 develop 分支则会报错

**把 develop 分支推送到远程仓库，如果远程仓库没有该分支则会创建**

	git push origin develop:develop

注：develop:develop 的第二个 develop 是为远程分支起的名字，可以随便起，但推荐保持一致，以免混乱

**查看本地分支列表**

	git branch

**查看远程分支列表**

	git branch -r

**查看本地和远程所有分支**

	git branch -a

**删除本地分支 a**

	git branch -d a

**同时删除本地多个分支(a、b)**
	
	git branch -d a b

**强制删除本地分支 a**

	git branch -D a

**删除远程分支 develop2**

	git push origin :develop2

**如果远程有个分支 release ,而本地没有，你想把远程的 release 分支更新到本地**

	git checkout -b release origin/release

如果执行命令报错：
>
> error: pathspec 'release' did not match any file(s) known to git.
> error: pathspec 'origin/release' did not match any file(s) known to git.
> 

先执行如下命令：

	git fetch

