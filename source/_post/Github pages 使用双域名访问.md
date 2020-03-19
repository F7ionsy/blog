---
title: Github pages 使用双域名访问
date: 2019-08-15 22:45:16
tags: 技术类
---

最近买了个新域名[F7ionsy.me](https://f7ionsy.me/)，因为国情在此，`.me`域名国内已经无法注册和购买使用，没办法，只能去国外转转。货比三家之后，选择了[porkbun.com](https://porkbun.com/)家的。虽然他家不支持支付宝，但是国内的信用卡可以注册`Paypal`，绑定信用卡，`Paypal`支付，整个过程三分钟不到。这里要吐槽一下国内的支付应用，注册流程复杂且漫长，无力吐槽。可能还是因为国情吧，╮(╯▽╰)╭无奈。

![snipaste_20190815_233200.png](https://f7ionsy-1251389397.cos.ap-shanghai.myqcloud.com/image/Github%20pages%20%E4%BD%BF%E7%94%A8%E5%8F%8C%E5%9F%9F%E5%90%8D%E8%AE%BF%E9%97%AE/snipaste_20190815_233200.png)

买好了域名，国内时打不开的，嘿我这个暴脾气。国内的DNS污染也太严重了，porkbun.com官方提供的DNS解析国内时无效的，无奈换成了腾讯云的，蛮以为这样就可以像之前设置[lihengdong.com](https://lihengdong.com/)一样直接指向`Github`仓库就ok了。然后找了半天才发现`Github pages`不支持绑定两个域名。这咋办，不能让新买的域名吃灰吧，于是去Google上找教程，搜了一圈也都是些二级跳转啥的，这不行，二级跳转也太慢了，虽然能访问，但是速度就是蜗牛。

辗转被我找到了[app.netlify.com](https://app.netlify.com/)这个网站，那么什么是**Netlify**？

它是一个提供静态资源网络托管的综合平台。

简单来说： 它的功能之一就跟我们之前Hexo博客的静态托管平台 `Github Page`一样, 不过，`Netlify`可比`Github Page`功能多多了，而且速度也快。两者的对比在[netlify官网](https://www.netlify.com/github-pages-vs-netlify/)有介绍。

简单来说它可以

- 托管静态资源
- 将静态网站部署到CDN上
- Continuous Deployment 持续部署，当你提交改变到git 仓库，它就会自动运行build command，进行自动部署。
- 可以添加自定义域名
- 重头戏：**可以启用免费的TLS证书，启用HTTPS**





详细部署教程这里就不说了，网上一大堆，这里要特别注意的是，不要在Netlify里添加域名相关的DNS和解析记录，一定要去域名的控制台修改。否则在Netlify中点击修改后，域名设置非但不会生效，而且会丢失设置方法，等你反应过来时，设置方法一营不再显示了，只有删除应用重新来过。

网上的教程一般说配置应用时使用分支部署，其实使用主分支部署也可以且分支部署相对来说钩子的生效时间会稍微长一点，对于`Hexo`博客来说，是不是主分支，不用在乎。

第三点需要注意的是，如果你的SSL证书是域名提供商下发给你的，那你填写SSL证书的时候，注意初级证书和中级证书是在domain.cert.pem的文件中的。这点也是个坑。



配置好之后，打开就是这个样子了，每一次自动部署都有logs。让我没想到的是，Netlify提供的DNS解析国内不仅可以使用甚至速度比腾讯云的还快了100ms左右，来来回回曲曲折折，没想到在这里曲线救国，哈哈哈。

![snipaste_20190815_232008.png](https://f7ionsy-1251389397.cos.ap-shanghai.myqcloud.com/image/Github%20pages%20%E4%BD%BF%E7%94%A8%E5%8F%8C%E5%9F%9F%E5%90%8D%E8%AE%BF%E9%97%AE/snipaste_20190815_232008.png)

相关：

添加域名记录集时，要注意根据Netlify上的提示添加ALIAS、A和txt记录，**切记不要在Netlify里添加域名相关的DNS和解析记录，一定要去域名的控制台修改。**

![snipaste_20190815_232419.png](https://f7ionsy-1251389397.cos.ap-shanghai.myqcloud.com/image/Github%20pages%20%E4%BD%BF%E7%94%A8%E5%8F%8C%E5%9F%9F%E5%90%8D%E8%AE%BF%E9%97%AE/snipaste_20190815_232419.png)

DNS配置完成的样子：

![snipaste_20190815_232754.png](https://f7ionsy-1251389397.cos.ap-shanghai.myqcloud.com/image/Github%20pages%20%E4%BD%BF%E7%94%A8%E5%8F%8C%E5%9F%9F%E5%90%8D%E8%AE%BF%E9%97%AE/snipaste_20190815_232754.png)

SSL证书配置完成的样子：

![snipaste_20190815_232844.png](https://f7ionsy-1251389397.cos.ap-shanghai.myqcloud.com/image/Github%20pages%20%E4%BD%BF%E7%94%A8%E5%8F%8C%E5%9F%9F%E5%90%8D%E8%AE%BF%E9%97%AE/snipaste_20190815_232844.png)

#仅作记录，可能**无法**提供详细参考和教程使用，请知悉。

