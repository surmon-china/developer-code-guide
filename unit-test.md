## 测试工具
前端测试工具主要使用[karma](https://karma-runner.github.io) + [mocha](https://mochajs.org/)，其他依赖的测试工具包括：karma-mocha和karma-chai。
测试依赖包在package.json已经配置好，只需要更新npm即可。

## 测试环境搭建
1.安装依赖包：命令行进入wind根目录下执行

    $ sudo npm install  //安装相关测试依赖包

2.安装karma命令行工具

    $ sudo npm install -g karma-cli  //安装karma命令行工具

将karma-cli加入环境变量

    $ sudo vi ~/.bash_profile

增加以下内容：
    
    export PATH=/usr/local/lib/node_modules/karma-cli/bin:/usr/local/bin/karma:$PATH
    
> 其中 `/usr/local/lib/node_modules/karma-cli` 为karma的安装目录

修改完后执行：
    
    $ source ~/.bash_profile //使环境变量生效


在命令行中执行：
    
    $ karma --version

输出 `Karma version: 0.13.21` 类似的版本号即为安装成功。

## 执行测试
1.初始化：karma安装好后，命令行进入根目录执行：
    
    $ karma init
    Which testing framework do you want to use ? //按tab选择mocha
    Do you want to use Require.js ? //根据情况选择，我们目前没有用Require.js
    Do you want to capture any browsers automatically ? //根据自己使用的浏览器环境选择
    What is the location of your source and test files ? //测试脚本目录，本项目为`client/admin/scripts/tests/**/*Spec.js`
    Should any of the files included by the previous patterns be excluded ? //留空即可，直接回车
    Do you want Karma to watch all the files and run the tests on change ? //选择yes，监测文件变化

init后，在根目录下会生成karma.conf.js的配置文件。

2.运行测试

    $ karma start //启动测试
