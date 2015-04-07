title: "hexo+gitcafe搭建静态博客"
date: 2015-03-30 21:25:21
tags: 
- hexo 
- gitcafe
---
>*****
写博客其实已经很久了，不过呢，占了GFW的光，到目前为止，写过的文章丢了很多，只剩下那能用指头数清的几篇了，自己也懒得再去找回来，趁着域名到期，自己又不想续费了，主要是因为国外的主机访问速度有时候慢的很，访问快的又不便宜，然后发现，网友推荐的github pages不错，很符合我的要求，还免费，所以就到了github，结果呢，github的访问也总是青黄不接，一直在不间断的挂掉，然后我决定再迁这一次，到gitcafe托管，如果再出问题，我真的是就不想再去折腾了。累觉不爱。。。。。
>*****

好了，不说废话了，进入主题，首先我们先熟悉几个东西：
>*****
>* git:分布式版本控制系统，和著名的svn类似，它是连接本地代码和远程同步的重要桥梁。
>* nodejs:允许使用js编写服务器端的一个框架，可以给本地的网站搭建http服务器。
>* gitcafe:代码托管平台，和大名鼎鼎的github类似，算是国内版的github吧，托管在gitcafe的访问速度要比github好很多。
>* hexo：一个基于Node.js的静态博客程序，可以方便的生成静态网页托管在github和gitcafe上
>* markdown:一种使用文本编辑的标记语言，用很少的代码，排很好的版，让你更加关注内容。
>*****

以上就是博客生成到写作要用到的几个软件和平台，接下来进入步骤：

一：安装软件：

1：git，nodejs，这两个直接去官网下载然后傻瓜式的下一步即可。
2：在gitcafe申请一个账号，以备后续要用，也可以后面再申请
3:步骤1完成之后，在任意空白处右键会看到git bash选项，然后点击，会出现git的命令行框，然后输入：
```
npm install hexo -g
```
执行后，可以ctrl+C结束运行，然后接着安装插件：
```
npm install hexo-renderer-ejs --save
npm install hexo-renderer-estylus --save
npm install hexo-renderer-marked --save
```
多试几次，一定要都安上。

二：初始化并生成本地静态博客

完成一后，建立新的文件夹hexo，名字任意。然后git bash中输入：
```
hexo init
hexo generate && hexo server
```
此时，你在浏览器输入:localhost:4000应该就可以看到这个了

![](/img/hexoTemp.png)
如果看不到，提示404页面错误，那么你按照gitbash的提示，再运行下
```
npm install --save
```
生成静态博客，只有这几个简单的命令，如果一直出不来，那么你多执行几次。应该没问题。接下来写篇文章，快捷键：
```
hexo n  newPostName
```
执行此命令后，会在你新建的hexo目录下的source目录下的post目录下，生成一个名为newPostName，后缀名为.md的文件，此时你可以用markdown编辑器打开了，然后写个hello world，然后保存。打开git bash,然后：
```
hexo generate && hexo server   //生成并启动本地服务器
hexo g -d   //生成并发布
```
打开localhost:4000能看到自己的文章了吧。

三：部署到gitcafe去
>****
在步骤二中，我们只是生成了本地博客，只可以用localhost访问，别人是无法看到，此时我们就必须找个服务器，将自己的程序部署上去，然后绑定域名，全世界就都可以访问的到了。对于我来说，gitcafe提供的这个免费功能完全就满足我了，所以没必要再去花钱买主机和域名了。
>***

在上面的步骤中，你已经申请了一个gitcafe账号，接着，可以参考这个
[gitcafe pages的官方帮助页面](https://gitcafe.com/GitCafe/Help/wiki/Pages-%E7%9B%B8%E5%85%B3%E5%B8%AE%E5%8A%A9#wiki) 创建一个gitcafe分支，一定要确保有分支存在。
打开hexo目录下的_config.yml，在下面添加如下代码：
```
# Deployment
## Docs: http://zespia.tw/hexo/docs/deploy.html
deploy: 
  	type: git
  	repository: git@gitcafe.com:your_name/your_name.git 
  	branch: gitcafe-pages
```
此处要注意type是git，不是github，我就是写成了github，结果发布的时候一直失败，提示找不到github，其中your_name为你的gitcafe的用户名，此时再
```
hexo g -d
```
在浏览器中输入:your_name.gitcafe.io就能看到自己的博客了。
到此为止，差不多已经完成了，如果你不喜欢这个博客的主题，可以给换个，参考下面步骤.

四：更换主题：
```
git clone https://github.com/A-limon/pacman.git themes/pacman
git pull
然后再hexo的配置文件中，修改theme属性为pacman,然后
hexo s //在本地浏览器能看到了
hexo g -d //同步到gitcafe中去，输入your_name.gitcafe.io就能看到了

```
主题还有很多，可以自己去折腾了，先clone，再pull，再改配置，新主题就可以用了，很简单吧。

五：罗嗦几个
```
hexo -s //启动本地服务器
hexo n new  //新建文章
hexo new page XXXXX  //新建页面，比如首页的“关于我”页面
hexo  g -d //bash框出现一个让你填写提交密码的地方，直接填写，然后回车，就可以看到新文章，修改和删除文章的话，直接进post文件夹中修改或删除md文件，然后再次
hexo  g -d 即可
如果哪里删除错了，出问题了，可以一个类似于电脑关机重启的老办法：
hexo clean 然后 hexo g -d  即可，首次可能会有延迟，耐心些哦。
同步到github、gitcafe，只要在config配置文件中修改之后再发布就可以了。
```

ok，全文完。






