## 上传代码到gitlab上

```Plaintext
git init 
git remote add origin +地址
git add .
git commit -m "Initial commit"
git push -u origin master
```

## 拉取代码和创建自己的分支

```Plaintext
git clone +地址                        --->拉取代码
git branch <分支名>                    --->建立分支
git checkout <创建的分支名>             --->从主分支切换到创建的分支上
```

## 提交代码

```Plaintext
git pull --->拉取服务器代码
git add + 文件
git add -u + 路径：将修改过的被跟踪代码提交缓存
git add -A + 路径: 将修改过的未被跟踪的代码提交至缓存
三种添加到git缓存的方法任选一个使用
git commit -m “注释部分 ref T3070”    ---> 添加解释说明
git push                             ---> 将代码推送到服务器
```

## githubToken

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 

切换二级密码 

git remote set-url origin https://@github.com//.git 

git remote set-url origin [https://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@github.com/jujiacheng/core.git](https://github.com/jujiacheng/audition) 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

 https://github.com/jujiacheng/core.git 

https://github.com/facebook/react.git