远程仓库的访问

HTTPS:零配置;但是每次访问仓库时，需要重复输入Github的账号和密码才能访问成功
 
SSH key:需要进行额外的配置;但是配置成功后，每次访问仓库时，不需重复输入Github的账号和密码
        id_rsa(私钥文件，存放于客户端的电脑中即可)
        id_rsa.pub(公钥文件，需要配置到Github中)


Git工作区中文件的4种状态
Git工作区中文件的4种状态
        未被管理：Untracked未跟踪
        已被管理：Unmodified未被修改、Modified已被修改、Staged已暂存
终端表现形式
    未跟踪——红色的??
    已跟踪——绿色的??
    
    已修改、没放入暂存区的文件前面有——红色的M
    已修改、  放入暂存区的文件前面有——绿色的M
 
 
先加入暂存区的文件有——绿色的A
 
当前所处分支——*


配置：设置自己的用户名和邮件地址
    第一步：在桌面空白区域，鼠标右键，选择“Git Bash Here”打开终端
    第二步：输入以下命令
          git config --global user.name "自己名字"
          git config --global user.email "自己邮箱"    
    第三步：找到全局配置文件C:/Users/用户名文件夹/.gitconfig 可以进行查看



基于SSH key将本地仓库上传到GitHub

生成与配置
第一步：桌面空白处，鼠标右键，点击Git Bash Here终端
 
 
第二步
    输入：ssh-keygen -t rsa -b 4096 -C "自己邮箱"
    后连续敲击3次回车：可在C:\Users\用户名文件夹\.ssh目录中，生成id_rsa和id_rsa.pub两个文件（可能名字不一样）
 
 
第三步：配置SSH key
    1.使用记事本打开id_rsa.pub文件，复制里面的文本内容
    2.在浏览器中登录Github，点击头像->Settings -> SSH and GPG Keys -> New SSH key
    3.将id_rsa.pub文件中的内容，粘贴到Key对应的文本框中
    4.在Title文本框中任意填写一个名称，来标识这个Key从何而来
 
 
第四步：检测SSH key是否配置成功
    1.点击Git Bash Here终端，输入：ssh -T git@github.com   // 验证是否已正确设置 ssh key 以向 github 进行身份验证
    2.输入yes,之后就可以看到自己的用户名


基于SSH将本地仓库上传到GitHub
第一步：本地创建Git仓库
本地文件目录下，鼠标右键，点击Git Bash Here终端
    情况一：没有现成的Git仓库
        1.使用终端命令创建 README.md文档
        2.初始化本地Git仓库,并将文件的修改提交到本地的Git仓库中
            git init
            git add README.md
            git commit -m "first commit"
        3.将本地仓库和远程仓库进行关联,并把远程仓库并命名
            git remote add 名字 网址
        4.将本地仓库中的内容推送到远程的origin仓库中
            git push -u origin 名字
    情况二：本地有现成的Git仓库
        1.将本地仓库和远程仓库进行关联,并把远程仓库命名为origin
            git remote add origin 网址
        2.将本地仓库中的内容推送到远程的origin仓库中
            git push -u origin 名字
            git push（后续更新的进行推送同步）
 
第二步：管理项目
    1.本地文件目录下，鼠标右键，点击Git Bash Here终端
    2.输入命令
        初始化仓库：git init
        检查状态：git status -s
        加入暂存区（时间看项目大小）：git add .
        检查状态：git status -s    
        指定提交消息（可能需要等一下）：git commit -m "first commit"
 
 
第三步：进入GitHub创建空白远程仓库
 
 
第四步：选择HTTPS
 
 
第五步：将本地仓库和远程仓库进行关联,并把远程仓库命名为origin
            git remote add origin 网址
 
第六步：修改分支的名字  git branch -m master 名字
            git branch -m master main
 
 
第六步：将本地仓库中的内容推送到远程的origin仓库中  git push -u origin 名字
                git push -u origin main
                git push（后续更新的进行推送同步）


常用一套

查看原项目代码状态：git status
 
修改的代码添加到暂存区：git add .
 
提交代码到本地仓库：git commit -m "完成了"
 
查看分支：git branch
 
切换分支：git checkout 需要切换的分支名
 
合并分支：git merge 需要合并的分支名
 
分支从本地推送到云端
    第一次：git push -u origin 需要推送的分支名
    以  后：git push
重要：第一次使用加上了 -u 参数，是推送内容并关联分支，之后推送直接使用git push即可，因为第一次已经将当前本地master分支和远程origin的master分支关联了。

```bash
git push -u origin master 
等同于
git push origin master //将当前分支提交到远程origin的master分支
加上
git branch --set-upstream-to=origin/master master//将远程仓库origin的master分支与本地仓库master分支关联
```



git init, git add 和git commit 都是前期的准备, 相当于将你本地的文件都上传到了本地仓库，但是还没有像远端仓库提交；

git remote add    就是先将本地仓库与远端仓库建立一个链接： 
为远端仓库所起的名字，一般都是叫origin，其实你也可以要Ceres 或者Earth



举个栗子，假设我已经存在一个文件夹，里面存放自己的代码，里面有一个文件叫README.md已经写好， 则

git init //初始化一个git的本地仓库

git add README.md //将我的文件装上武器，准备发射

git commit -m “first commit” //第一次发射，我的README.md 宝贝已经成功进入到本地仓库

git remote add Ceres your_first_git_address //将第一个git address命名为Ceres
// git remote add origin git@github.com:glwabc/test.git

git push -u Ceres master

//将另一个远端仓库与本地仓库建立一个连接就可以了

git remote add Mars your_second_git_address //将第二个git address命名为Mars

git push -u Mars master //再次发射，目标火星上的master分支
至此，就将一份代码上传到了两个远端仓库，但是注意你仍然时只有一个本地仓库哦

补充：

在用 git push -u Ceres master 时也要注意这里master是你要上传的分支名称，如果你当前所位于的分支不叫master，用这句话上传就会出错


https://deepinout.com/git/git-questions/19_git_one_project_multiple_customers_with_git.html