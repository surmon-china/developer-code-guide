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