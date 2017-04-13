## 基本设置

#### 1. 初始化用户名和邮箱；    

        $ git config --global user.name 'your username'  //使用个人英文名
        $ git config --global user.email you@yourdomain.com  //使用公司分配的企业邮箱

#### 2. 设置大小写敏感；
进入项目目录下，执行以下命令：

        $ git config core.ignorecase false

## 仓库操作
克隆远程仓库的项目到本地：

    $ git clone https://git.coding.net/winhu/winhu.git  //克隆项目到当前目录下的winhu目录
    $ git clone https://git.coding.net/winhu/winhu.git folder_name  //指定目录：克隆项目到当前目录下的folder_name目录

## 文件操作

#### 1. 文件操作流程
![在这里输入图片描述][1]
#### 2. 文件操作命令

        $ git status  //查看本地文件状态，有新文件需要添加，执行下面的添加文件命令  

        $ git add <filename> //添加未加入版本控制的新文件
        $ git add * //添加所有未加入版本控制的新文件

        $ git commit -a -m "提交说明"

        $ git pull origin master  //从远程版本库拉取更新

  无冲突则添加合并说明，有冲突手动处理冲突。

        $ git push origin master  //推送到远程版本库


  [1]: https://coding.net/api/project/18513/files/169771/imagePreview
  
  
  ## 初始化配置
1 配置使用git仓库的人员姓名  

    $ git config --global user.name "Your Name Comes Here"  
  
2 配置使用git仓库的人员email  

    $ git config --global user.email you@yourdomain.com  
  
3 配置到缓存 默认15分钟  

    $ git config --global credential.helper cache   
  
4 修改缓存时间  

    $ git config --global credential.helper 'cache --timeout=3600'   

5 设置大小写区分

    $ git config core.ignorecase false  //在项目目录下执行

## 仓库操作
1 创建新仓库
    
    $ git init

2 检出仓库

    $ git clone /path/to/repository  //创建一个本地仓库的克隆版本
    $ git clone username@host:/path/to/repository  //检出远端服务器上的仓库

## 添加和提交
1 添加文件到暂存区
    
    $ git add <filename>
    $ git add *

2 提交操作

    $ git commit -m "代码提交信息"  //改动已经提交到了 HEAD，但是还没到你的远端仓库

3 查看文件改动情况
    
    $ git status

## 推送改动
1 推送到远程仓库
    
    $ git push origin master

2 添加远程仓库

    $ git remote add origin <server>

## 分支操作
1 查看本地分支

    $ git branch

2 查看远程分支

    $ git branch -r

## 创建分支
1 创建本地分支（建立分支后，仍停留在当前分支，切换分支：git checkout branchName）

    $ git branch branchName

2 创建分支后切换到新分支

    $ git checkout -b branchName

## 提交分支
1 提交到远程分支

    $ git commit -a -m 'my new branch'
    $ git push origin branchName:branchName

2 如果想把本地的某个分支mybranch提交到远程仓库，并作为远程仓库的master分支

    $ git push origin mybranch:master

## 删除分支
1 删除远程分支

    $ git push origin :branchName

2 删除本地分支，强制删除用-D

    $ git branch -d branchName

## 合并分支
将分支branchName和当前所在分支合并

    $ git merge --no-ff branchName

默认情况下，Git执行"快进式合并"（fast-farward merge），会直接将Master分支指向Develop分支。使用--no-ff参数后，会执行正常合并，在Master分支上生成一个新节点。为了保证版本演进的清晰，我们希望采用这种做法。

## 标记tag
对当前分支打tag

    $ git tag tagContent

然后push到远程即可

    $ git push origin BranchName:BranchName

## 创建新项目
    
    mkdir test
    cd test
    git init
    echo "# test" >> README.md
    git add README.md
    git commit -m "first commit"
    git remote add origin https://git.coding.net/winhu-coding/test.git
    git push -u origin master

## 已有项目

    git remote add origin https://git.coding.net/winhu-coding/test.git
    git push -u origin master
