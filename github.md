前段时间，老师在群里分享了一个 github 的连接，说开源了。

我记得当时，看了看，才那么 几 百 M ，，，还 8.8 W = = ！

昨天，我一朋友自己直接搭自己硬盘上了，我就自己搭搭吧，很简单的，一放一点就成了。

**#** 按我的风格，肯定要记录的详细的不能再详细了 ，就算很简单的步骤，我也要详细点。

**#** 就像，我上次用 linux 的系统，搭建一个网站，要是有大牛直接甩我 一堆命令行 ，该有多好，我直接张贴复制就是怼。 #（斜眼笑。。。）

**# 2017.6.20晚，我百度网盘里存的图片，真的存在一句话！0.0屌啊！我再开一个帖子，写写把。。。**

**这个是关于两个图片马的帖子。
**

```text
https://zhuanlan.zhihu.com/p/27486144
```

这个是开源地址：

```text
https://github.com/m0l1ce/wooyunallbugs
```

这是我存我百度盘里的：

```text
链接: http://pan.baidu.com/s/1nvkFKox 密码: 94sp
```

\----------------------------------------------------------------------------------------------------------------

1，首先去下载一个集成环境工具，这里我用的 phpStudy ， 33M 的这个。



![img](https://pic2.zhimg.com/80/v2-8a82a0983d443b20b7b027f1f259fb05_720w.jpg)

下载地址：[phpStudy 2016.11.03 再次更新，支持自定义php版本](http://www.phpstudy.net/a.php/211.html)



2，然后，我解压到我的 Ｄ 盘上了。



![img](https://pic3.zhimg.com/80/v2-3c6832d45b1073634182db81a4b3d1be_720w.jpg)

3，把源码和数据库先下载开，图片用的是外连，人家也说了，放图片的服务器不会关掉的。





![img](https://pic4.zhimg.com/80/v2-ce1dd65ced704cc9d3ed41427de9090b_720w.jpg)

4，把 bugs.rar 这个源码包解压到了　D:\phpStudy\WWW\bugs\ 这里。





![img](https://pic3.zhimg.com/80/v2-efc19b467c4f179bf8e9da8c3f90a8ca_720w.jpg)

5，在源码里找见 conn.php 这个文件，用记事本打开，或者想我一样下载了 notepad++ ，打开就是了，在里面修改成自己 MySQL 数据库的账号密码 。





![img](https://pic2.zhimg.com/80/v2-09359e6a25b9c9ffad07ad8a552915f1_720w.jpg)

![img](https://pic2.zhimg.com/80/v2-a7af61f7e09ee7d96b84ef93e4bb62fd_720w.jpg)

6，然后把 wooyun.rar 拖进 D:\phpStudy\MySQL\data 这里解压下，这里是数据库存放的地方。





![img](https://pic3.zhimg.com/80/v2-4e3998dac5699cad94593748f5884ce2_720w.jpg)

7，启动 phpstudy ，然后点击面板上的选择版本，看下是不是 5.3 版本的，如果不是就选择到这个 5.3 版本 。（昨天就这个版本问题，害的我一连不上数据库。。。）





![img](https://pic1.zhimg.com/80/v2-7ca81c770a4c22f8ad37291edd6dc8c4_720w.jpg)

8，点击 mysql 管理器，站点域名管理，然后该杂弄杂弄。。。





![img](https://pic4.zhimg.com/80/v2-e1f98db6c75145c4d964dd64b7eb3a4b_720w.jpg)

![img](https://pic3.zhimg.com/80/v2-60ad89bec893625ab0130f27e3de8fba_720w.jpg)

9，一般到这里就结束了，直接启动服务器，然后然后输入 *127.0.0.1* 就能进入了主页面了。





![img](https://pic4.zhimg.com/80/v2-9f9c1a4ccb719d4070d270ddc6dc2f3f_720w.jpg)

10，恩，先修改一个小错误，再继续说说其他的。他的源码不知道杂回事，进入具体的页面时就会在上面出现报错的提示。。。





![img](https://pic2.zhimg.com/80/v2-c9888ee6c32c648b8daf693d61c28d5d_720w.jpg)

10.1，看着挺不好看的，那我就关闭这个提醒吧，





![img](https://pic1.zhimg.com/80/v2-8dfdc1dcdd68cb9d406999c3ddc2c9a0_720w.jpg)

![img](https://pic1.zhimg.com/80/v2-897e4035a4eb309a9f0dc3817c497318_720w.jpg)

**# 额，那个其中有些步骤，需要多点击重启这个按钮的，就是把操作更新到设置中。。。反正最后多重启几下就好了。**



\------------------------------------------------------------------------------------------------------------------------

1，其他，如果修改域名的话，建议用管理员权限打开 phpstudy 这个工具 。



![img](https://pic4.zhimg.com/80/v2-7e87ef43517fb2be07da30597a53b6df_720w.jpg)

2，继续来到域名管理的那个页面。





![img](https://pic2.zhimg.com/80/v2-bf8f346e68e6badedf42fa5942923d21_720w.jpg)

3，然后打开 hosts 这个文本。





![img](https://pic4.zhimg.com/80/v2-b496211343a9054abe05727fa4c1f3f3_720w.jpg)

4，添加自己的域名解析地址。





![img](https://pic3.zhimg.com/80/v2-2aef02b324bdf263f88d565f39eaaf7e_720w.jpg)

5，来看一下效果 。





![img](https://pic1.zhimg.com/80/v2-db24c00c6562f4c5d16eabe25bed8078_720w.jpg)

\-----------------------------------------------------------------------------------------------------------------------



1，下载了一下午的图片，终于下载到我电脑上了。那么开始吧。

2，在 wuyun 源码里新建一个 upload 文件夹。



![img](https://pic1.zhimg.com/80/v2-5984caf9dacd5835547545973c48d80c_720w.jpg)

3，把这一堆的图片全部解压到 upload 这个文件夹里。





![img](https://pic3.zhimg.com/80/v2-594a2db8cc8204aa321cefa82423e32e_720w.jpg)

![img](https://pic4.zhimg.com/80/v2-4f127b76e77dae34bcefef3e2be7ae3f_720w.jpg)

**#** 快一个小时了。。。。 关解压都能解压半个多小时，我也是醉醉的。。。



4，继续用右键管理员权限运行 phpStudy.exe 。

5，继续 点击 MySQL 管理器，点击 站点域名管理 ，新增一个 static.loner.fm 域名，然后路径继续绑定到 wuyun 这个源码路径里，和一开始那个操作差不多，新增，保存。



![img](https://pic1.zhimg.com/80/v2-d0efbe3b527502ee6cac51e106642eec_720w.jpg)

6，继续点击 其他选项菜单，继续打开 hosts 这个文本 ，然后输入在原来的下一行输入以下地址，并保存



```text
localhost   static.loner.fm
```



![img](https://pic1.zhimg.com/80/v2-e806dd998ddd0d2159aed75ab5255960_720w.jpg)

7，最后，启动下环境，输入地址，看下效果，是不是成功本地了。





![img](https://pic1.zhimg.com/80/v2-360c2adf507bfddcf6ed0847b6b2be50_720w.jpg)

![img](https://pic4.zhimg.com/80/v2-9fc0d39c6cbcefe403cd8d7f4bfe472b_720w.jpg)

\---------------------------------------------------------------------------------------------------------------------------



**#** 全文一步一步的写，我对我自己也是醉醉的。。。不过以后可以本地默默的看 8.8 w 的漏洞库的，嘎嘎。(*^__^*) 嘻嘻……