---
title: 关于hexo的使用
date: 2017-10-24 23:24:37
tags:
  - hexo
categories:
  - 技术
---
本文用于记录hexo的使用笔记，会不定时更新一些hexo的使用技巧，如果你还没有用过hexo或者不知道hexo是什么，请移步[如何用Github+Hexo搭建博客网站(1)](https://liangmp.github.io/2017/10/31/hexoBlog/)。
<!--more-->

# hexo常用命令行
```
hexo g = hexo generate // 生成
hexo s = hexo server   // 运行服务器
hexo d = hexo deploy   // 部署
hexo new post "title"  // 新建博客文章
hexo hew page "tags/catagories/about" // 开启tags/catagories/about功能，将会在source文件夹下自动新建相应的文件夹和文件
hexo clean // 清除之前生成的静态网页文件，即删除public文件夹内的所有东西，相当于把整个public文件夹删除掉。
```

hexo环境搭建好后，写新的博客文章可以采用以下顺序的命令行：
```
hexo new post "title"  //新建完之后到source/_post里面能找到对应的title.md，打开写文章，保存
hexo clean //清除缓存
hexo generate //生成。建议新手用完整的命令语句而不是使用缩写的hexo g，这样可以让自己清楚每一步是干什么的。
hexo server //运行服务器，然后在浏览器上打开localhost:4000查看效果
hexo deploy // 部署到repository上
```
deploy完之后博客可能不是马上更新的，需要等个几分钟，不要着急。

附上hexo的[中文版指令文档](https://hexo.io/zh-cn/docs/commands.html)

---

# hexo博客建立过程中遇到的常见问题
## port 4000 has been used
在git bash中输入命令行hexo s后报错
解决方法：
方法一：
在git bash输入命令行netstat -ant |grep 4000 
看看被什么占用了,然后如果这个是没人用的东西,就kill掉这个进程
方法二：
可以在_config.yml内加上如下代码更改hexo-server运行时的端口号：
```
server:
  port: 4001
  compress: true
  header: true
```
port可以修改成任意非4000的，只要不再报冲突就行。
参考[segmentfault](https://segmentfault.com/q/1010000008546859)的回答

## 主页博客文章顺序排列不对
很可能是你的文章没有加上date，在.md的title下面加上时间：
date: 2017-10-24 11:08:24
这步可以选做：去public文件夹下找到年份文件夹（如2017），进去调整生成的文件即可。

---

# 不断完善你的博客
## 首页展示折叠
在需要折叠的地方添加`<!--more-->`

## 添加tags和catagories

## 创建"about me" page
方法跟前面的添加tags和catagories类似，git bash: hexo new page "about"
在themes里面的_configy.yml设置中将menu中about 前面的注释去掉即可。
```
menu:
  home: /
  archives: /archives
  tags: /tags
  about: /about
```

---

# 关于markdown的使用技巧
Markdown是一种电子风格的标记语言，它能让写作者关注于写作内容本身，而不是文章的排版。个人觉得Markdown非常方便好用，特别写了一篇博客[Markdown使用指南](https://liangmp.github.io/2017/10/28/markdown/#more)感兴趣的同学可以进去看一下。



*******************************
本文会持续更新
敬请期待。。。
*******************************