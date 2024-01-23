# COCOPODS 换源

```Shell
# 在shell中执行下面命令
$ cd ~/.cocoapods/repos 
$ pod repo remove master
$ git clone https://mirrors.tuna.tsinghua.edu.cn/git/CocoaPods/Specs.git master
#在项目的podfile 文件添加下面一行
#source 'https://mirrors.tuna.tsinghua.edu.cn/git/CocoaPods/Specs.git'
#然后和以前意义，使用pod install进行安装
git clone https://gitee.com/mirrors/CocoaPods-Specs.git master
```