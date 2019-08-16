title: git常见错误：push出现rejected错误
author: yorkmass
tags:
  - git
  - hexo
  - github
  - push
categories:
  - git
date: 2019-08-16 18:07:00
---
### git常见错误：push出现rejected错误

***
相关问题可参考：[csdn](https://blog.csdn.net/qq_36949176)、[博客园](https://www.cnblogs.com/yorkmass/) 的解决方案<br><br>
我在使用git上传代码的时候，使用如下命令发生了错误
```
git init 
git remote add origin https://gitee.com/imoonfish/dachuang.git
git add .
git commit -m '完成'
git push origin master
```
开始提示需要先pull,再push<br>于是我又执行了一遍命令，依然报错
```
git init 
git remote add origin https://gitee.com/imoonfish/dachuang.git
git pull origin master
git add .
git commit -m '完成'
git push origin master
```
错误如下:<br>
![报错](/img/small/p011.png "git报错")
<br>
可使用-f参数强制push,解决这个问题<br>
```
git push -f origin master
```
或者在pull的时候使用--allow-unrelated-histories参数解决pull的合并问题
```
git pull origin master --allow-unrelated-histories
```
当我使用git status查询状态的时候，显示nothing to commit ,working tree clean 

这时候我才发现原因，我是先新建一个文件夹，执行git init ,然后把自己更改完成的文件粘贴进文件夹，然后再git pull origin master，再git push origin master

解决办法：<br>
新建一个文件夹,依次执行如下命令
```
git init
git remote add origin https://gitee.com/imoonfish/dachuang.git
git pull origin master
```
然后把自己修改完成的文件粘贴到这个文件夹，替换这个文件里面的内容，再依次执行如下命令
```
git add .
git commit -m '完成'
git push origin master
```
 这回就没有报错了！<br>
 ![截图](/img/small/p012.png "报错")
 <br>
 发生以上问题的原因，是这两个项目都不一样，一个是本地项目，一个是远程项目，必须要强制合并。

所以，以后我们应该在远程仓库新建一个空项目，然后使用git clone克隆这个项目到本地，git clone会自动初始化本地仓库环境。然后再把我们的代码粘贴进去，然后再add再commit提交，最后push到远程仓库。