title: Halo博客系统在IDEA运行时log报错
author: Yaoyi
date: 2019-08-17 15:21:01
tags:
---
#### Halo博客系统在IDEA运行时log报错
***
###### 运行别人项目（Halo博客系统）时候导入IDEA：Cannot resolve symbol 'log' 的解决方法
导入别人的项目时，log报错，提示Cannot resolve symbol‘log’，网上查询发现安装lombok插件即可。以下是lombok插件的作用。<br>
官方介绍如下：
```
Project Lombok makes java a spicier language by adding 'handlers' that know how to build and compile simple, boilerplate-free, not-quite-java code.
```
大致意思是Lombok通过增加一些“处理程序”，可以让java变得简洁、快速。
###### Lombok简介：
Lombok能以简单的注解形式来简化java代码，提高开发人员的开发效率。例如开发中经常需要写的javabean，都需要花时间去添加相应的getter/setter，也许还要去写构造器、equals等方法，而且需要维护，当属性多时会出现大量的getter/setter方法，这些显得很冗长也没有太多技术含量，一旦修改属性，就容易出现忘记修改对应方法的失误。
<br>Lombok能通过注解的方式，在编译时自动为属性生成构造器、getter/setter、equals、hashcode、toString方法。出现的神奇就是在源码中没有getter和setter方法，但是在编译生成的字节码文件中有getter和setter方法。这样就省去了手动重建这些代码的麻烦，使代码看起来更简洁些。
##### 解决办法
###### 1.1Ctrl+Alt+S打开Settings
搜索或者直接选择Plugins，在Marketplace里面搜索Lombok安装即可<br>
安装完成之后如图所示<br>
![github031](/img/small/p031.png "github")<br>
重新编译一下，就可以运行项目了，log错误消失