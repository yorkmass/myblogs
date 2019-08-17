title: Hexo+github搭建个人博客
author: Yaoyi
date: 2019-08-17 14:56:11
tags:
---
#### 使用hexo在github上面搭建个人博客
[可参考CSDN教程](https://blog.csdn.net/qq_36949176/article/details/99684455)
我们需要在电脑上安装git和npm
<br>Linux系统最为方便，直接装git和npm就好了
<br>Windows系统安装git和npm，然后所有命令都在git bash里面操作
<br>npm安装hexo，全局安装<br>
```
npm install -g n
```
然后找一个文件夹，初始化hexo，括号里面为说明，一步一步执行<br>
```
hexo init blog(生成的博客文件夹的名字，自定义,会在对应执行该语句的路径生成对应的文件)
cd blog
npm install
hexo server
```
执行完所有命令就可以在本地通过[http://localhost:4000](http://localhost:4000)访问hexo了
<br>为了方便写博客，我们还需要在本地安装hexo-admin,括号里面解释说明<br>
```
npm install --save hexo-admin
hexo server -d(开启hexo操作)
```
安装完成之后，可以通过[http://localhost:4000/admin](http://localhost:4000/admin)访问
<br>使用[https://travis-ci.com](https://travis-ci.com)执行部署github
<br>在这之前，我们首先需要在github里面新建一个空仓库，仓库名：用户名.github.io 
<br>如：yorkmass.github.io    我的仓库链接：[yorkmass.github.io](https://github.com/yorkmass/yorkmass.github.io)
<br>用于接收hexo生成的静态文件，展示给用户
<br>我们还需要另外给刚才在本机执行的hexo文件新建一个仓库，我的叫myblogs。我的仓库链接：[myblogs](https://github.com/yorkmass/myblogs)
<br>接着就是把刚才在本机生成的目录push到你新建的github仓库(myblogs仓库)中
<br>因为需要连接到travis-ci，他要识别仓库里面的.travis.yml 文件，我们需要在本地的hexo项目的根目录新建一个.travis.yml文件
<br>在里面添加如下内容<br>
```
language: node_js
node_js:
  - "11"
install:
  - npm install
script:
  - hexo g
after_script:
  - cd ./public
  - git init
  - git config user.name "yorkmass"
  - git config user.email "1458510486@qq.com"
  - git add -A
  - git commit -m "init"
  - git push --force "https://${TOKEN}@github.com/yorkmass/yorkmass.github.io.git" "master:master"
branches:
  only:
    - master
```
其中，我们需要修改里面的user.name，把yorkmass改成你github的用户名，我的用户名为yorkmass
<br>把user.email改为你github绑定的邮箱，然后把https://${TOKEN}@github.com/yorkmass/yorkmass.github.io.git
<br>这段东西按着这个格式改为你新建的&nbsp;&nbsp;&nbsp;&nbsp;github用户名.github.io仓库的地址&nbsp;&nbsp;<br>
如果你的用户名为imoonfish,就改成<br>
https://${TOKEN}@github.com/imoonfish/imoonfish.github.io.git
<br>其他不变，这样就把myblogs仓库执行完成的文件发布到yorkmass.github.io仓库里面了。
<br>我们还需要连接github和travis-ci.com
<br>我们登陆我们的github,进入setting页面，然后点击最下面的那个开发者设置Developer setting，然后点击Personal access tokens
<br>
![github01](/img/small/p021.png "github")
![github02](/img/small/p022.png "github")
![github03](/img/small/p023.png "github")
Generate new token，然后添加note（随便写），把能勾选的都勾选，然后会生成一个key，注意：这个key只出现一次，先复制下来到记事本保存一下，等会要用<br>
接着我们使用github账户登陆[travis-ci.com](https://travis-ci.com/)，他会同步你在github的所有仓库，我们打开我们新建的仓库(myblogs仓库），找到这个项目的设置，如图是设置完成的图片。<br>
![github04](/img/small/p024.png "github")
如上图所示，我们需要在Environment Variable环境变量里面添加一行<br>
Name写TOKEN，VALUE写刚才在github生成的key，粘贴进去即。BRANCH填写master即可，然后点击右边的Add按钮
<br>还有下面的一条Cron Jobs，这个我们就随便配置了，一般是每天更新，BRANCH写master，INTERVAL写Runs daily，然后OPTIONS填Always run，然后点击右边的Add按钮即可。<br>
然后我们切换到Current栏，点击Start，开始执行代码，执行成功之后如图所示
<br>![github05](/img/small/p025.png "github")
执行完成之后，它会在你的yorkmass.github.io仓库发布一系列hexo的静态页面， 然后我们通过github用户名.github.io就可以进行访问了，如：[https://yorkmass.github.io](https://yorkmass.github.io)


