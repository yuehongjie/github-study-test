#git初步:       
- 注.使用任何的git操作之前，都需要切换到git项目目录下
> 1. git status 查看当前git仓库状态
> 2. git init 初始化git仓库
> 3. git add file 修改file文件的状态为添加，并没有被提交，是存在缓存中
> 4. git rm --cached file 更改上面文件的状态为无状态(移除缓存)
> 5. git config user.name yu ;  
     git config user.email 1419699711@qq.com   
     添加git用户，在进行提交之前如果没有配置用户会报错
> 6. git commit -m message 提交并附带提交信息
> 7. git log 提交日志
> 8. git config core.autoclrf false 每次使用git命令(add,commit)的时候会报warning: LF will be replaced by CRLF in XXXX ，这是自动添加换行(linux下格式)引起的问题
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
> 1. 生成ssh key: ssh-keygen -t rsa  
指定 rsa 算法生成密钥，接着连续三个回车键（不需要输入密码），然后就会生成两个文件 id_rsa 和 id_rsa.pub ，而 id_rsa 是密钥，id_rsa.pub 就是公钥


