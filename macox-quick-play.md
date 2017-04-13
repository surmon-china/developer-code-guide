### 安装配置常用开发环境

#### 1.安装Node、Ruby，更好npm、gem源为国内镜像。

Node主要用于前段构建和持续集成，如：CSS、JS合并、压缩，包管理等。
Ruby主要用于安装一些gem工具，如sass。

更换npm源：

    $ npm config set registry http://registry.cnpmjs.org  #设置为中国镜像

目前已知的npm 镜像源站点: 
中国镜像站:	http://registry.cnpmjs.org 
官方站: http://registry.npmjs.org 
各国镜像: 
https://registry.nodejitsu.com  美国 
https://npm.strongloop.com	美国 
http://registry.npmjs.org.au	澳大利亚 
http://registry.npmjs.eu	德国 

更换gem源：

    //首先查看gem源
    $ gem sources
    *** CURRENT SOURCES ***

    https://rubygems.org/

    //添加淘宝源
    $ gem sources -a https://ruby.taobao.org
    https://ruby.taobao.org added to sources
    
    //删除ruby官方gem源
    $ gem sources -r https://rubygems.org/
    https://rubygems.org/ removed from sources
    
    
  ### 常用快捷键说明

切换输入法：command + 空格
复制：command + C
粘贴：command + V
剪贴：command + C 然后 command +option + V
刷新：command + R
最小化当前窗口：command + M
Finder前往指定目录：在Finder中运行：command + shift + G



更多快捷键参照：<http://www.ithome.com/html/soft/30862.htm>

***

#### 批量删除目录下的.DS_Store
删除目录下的.DS_Store：

    sudo find ./ -name ".DS_Store" -depth -exec rm {} \;

不过以后系统还是会创建新的.DS_Store 文件，如果需要禁止系统创建，那么可以在终端中运行如下代码（不建议这样使用）：

    defaults write com.apple.desktopservices DSDontWriteNetworkStores true

这样当前账户下就不会再创建新的.DS_Store 文件了。

#### 设置mysql、apache等开机启动
mysql开机启动

    $ sudo vi /Library/LaunchDaemons/com.mysql.plist
输入以下内容：

    <?xml version="1.0" encoding="UTF-8"?>    
    <!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">    
    <plist version="1.0">    
      <dict>    
        <key>KeepAlive</key>    
        <true/>    
        <key>Label</key>    
        <string>com.mysql.mysqld</string>    
        <key>ProgramArguments</key>    
        <array>    
        <string>/usr/local/mysql/bin/mysqld_safe</string>    
        <string>--user=root</string>    
        </array>      
      </dict>    
    </plist>
设置开机启动

    $ sudo launchctl load -w /Library/LaunchDaemons/com.mysql.plist

apache开机启动

    $ sudo launchctl load -w /System/Library/LaunchDaemons/org.apache.httpd.plist  // 开机启动
    $ sudo launchctl unload -w /System/Library/LaunchDaemons/org.apache.httpd.plist // 禁止开机启动
