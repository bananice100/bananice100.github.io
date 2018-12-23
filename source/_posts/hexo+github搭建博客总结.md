---
title: Hexo+github搭建博客总结
date: 2018-12-14 11:41:22
---

# 一、前期准备工作
  1.安装node.js：
    [安装地址](http://nodejs.cn/)
  2.安装git：
  	[安装地址](https://git-scm.com/downloads)
  	![git工作流](\images\hexo+github搭建博客总结\git工作流.png)
  3.使用npm安装Hexo：
    在cmd中输入
    >npm install -g hexo-cli
    命令的意思是安装hexo包到全局，所以操作路径应该没什么影响
    ![npm命令](\images\hexo+github搭建博客总结\安装hexo.PNG)

# 二、用Hexo在本地搭建博客
  -切换到一个用于保存本地博客的文件夹，输入命令：
    >hexo i blog //hexo init <folder>在指定的文件夹里创建所需要的文件，i是init的缩写
    >cd blog//切换到站点根目录
    >hexo g //hexo generate生成静态文件
    >//静态文件保存在public文件夹中
    >hexo s //hexo server启动服务器，访问网址为:http://localhost:4000/
    ![展示图片](\images\hexo+github搭建博客总结\localhost.png)
  -对hexo页面属性的编辑，例如更改主题等，可以到https://hexo.io查看

# 三、上传到github
  1.注册github账号
  2.创建新项目：
    ！[创建新项目](\images\hexo+github搭建博客总结\创建仓库.PNG)
    项目名称必须是：用户名.github.io
    ![命名](\images\hexo+github搭建博客总结\repository name.PNG)
  3.配置身份信息：
    >git config --global user.name "yourname"
    >git config --global user.email "youremail"
    >//此处的yourname和youremail分别是Github账号的用户名和绑定邮箱
  4.修改hexo站点的配置文件：
    打开博客根目录里面的_config.yml//大多数配置都是在_config.yml中修改的
    修改deploy参数 //deploy参数是关于部署部分的设置。
    ># Deployment
    >## Docs: https://hexo.io/docs/deployment.html
    >deploy: 
    >  type: git
    >  repository: https://github.com/bananice100/bananice100.github.io.git
    >  branch: master
    ![config](\images\hexo+github搭建博客总结\config.PNG)
    *!!!参数后面的冒号一定要加一个空格*
  5.安装一个插件：
    >npm install hexo-deployer-git --save
  6.部署网站：
    >hexo d//hexo deploy的缩写
    部署过程中会弹出一个窗口，按照要求输入github账户密码就行。

# 四、多终端同步
  -同步更新的思路：
    在github上面新建一个hexo分支，把本地hexo站点的文件同步到hexo分支上。
    每次更新之前下载hexo分支上的文件，本地更新完之后再上传。
    *问题：这个多终端共同开发的思路我是直接参考的其他作者的文章，所有参考文章的链接会在底部给出。*
    *但是这个方式在多个人同时编辑的时候可能会产生互相覆盖的问题。后续可能会采取其他方式。*
  
  ![git工作流](\images\hexo+github搭建博客总结\git工作流.png)
  [github简明教程](http://www.runoob.com/w3cnote/git-guide.html)
  *有助于理解下面的操作*

  1.将配置文件上传到hexo分支上
    >git init  //初始化本地仓库
    >git add . //添加文件到Index(暂存区),这里有些教程用source代替.，只上传部分文件。
    >//source文件保存博客需要的md文件和图片等，如果更改_config.yml等其他配置文件可能
    >//就会出现问题，所以这里选择了全部上传。
    >git commit -m "Blog files"
    >git branch hexo      //新建hexo分支
    >git checkout hexo    //切换到hexo分支
    >git remote add origin repository地址.git //绑定远程仓库;
    >例如:git remote add origin https://github.com/bananice100/bananice100.github.io.git
    >git push origin hexo //push到github项目的hexo分支上
    - commit -m 后面的字符串：(会添加在图中的位置)
      ![commit](\images\hexo+github搭建博客总结\commit -m.PNG)
    - 对比hexo分支和本地站点文件：
      ![git](\images\hexo+github搭建博客总结\hexo1.PNG)
      ![local](\images\hexo+github搭建博客总结\hexo0.PNG)

  2.其他终端：
    准备工作：安装Node.js,Git
    第一次更新博客：
    >git clone -b hexo repository地址.git //将github中hexo分支克隆到本地
    >例如:git clone -b hexo https://github.com/bananice100/bananice100.github.io.git
    >cd yourname.github.io 
    >npm install //安装所需组件
    >hexo new post "new blog name" //新建一个.md文件，这个文件是放在/source/_posts路径下的。
    >//"new blog name"就是文件名，打开文件先编辑。
    >git add .
    >git commit -m "blog files"
    >git push orgin hexo  //更新分支
    >hexo d -g//部署博客
    后续:
    后续的编辑就不用clone了,直接用pull更新本地文件。
    >git pull origin hexo //要更新你的本地仓库至最新改动
    剩下的操作和之前一样
    >hexo new post "new blog name"
    >git add .
    >git commit -m "blog files"
    >git push origin hexo
    >hexo d -g

  *Tips:想要在上传之前查看效果，可以不用hexo d -g,而是用hexo s,然后在localhost:4000即可查看。*

# 写在最后：
      这篇总结是在博客搭建完成之后写的，可能会有一些漏写的或者没有想到的东西，在搭建过程中出现问题可以联系
  我们(还没添加评论功能@_@)，其他终端的部分，没有测试，同样不知道会不会出问题。后续会完善。

  参考文章：
  https://blog.csdn.net/Hoshea_chx/article/details/78826689
  https://xuanwo.io/2015/03/26/hexo-intor/
  https://blog.csdn.net/Monkey_LZL/article/details/60870891
  和相关官方文档