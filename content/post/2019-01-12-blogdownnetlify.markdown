---
title: Blogdown和Netlify设置事项
author: 李泉
date: '2019-01-12'
slug: blogdownnetlify
categories:
  - R
tags:
  - Blogdown
description: ''
topics: [R]
---

因为对GitHub的使用方式不了解，所以在使用blogdown和Netlify建立博客网站的过程中遇到一些问题，不过好在网上能找到的帮助信息不少，跌跌撞撞的终于让网站上线了。以下是总结的一些细节，希望能帮助你更快的从零基础建设自己的博客网站。

我最开始是看了谢益辉大神在2018年R会议上的一个30分钟左右的教学视频，虽然视频后段的一些技术细节没听懂，但是对使用blogdown的基本流程有了一个整体了解。[谢益辉大神的教学视频在这](https://www.rstudio.com/resources/videos/create-and-maintain-websites-with-r-markdown-and-blogdown/)。


如果看不到视频的的话，Peter Baumgartner的博客上有一个分为四部分的教程。我是网站建好后才看到。他的教程里有很多截图，可以很方便的了解具体操作步骤。[Peter Baumgartner的教程](https://notes.peter-baumgartner.net/tutorial/blogdown-tutorial-part-1/)。遵循他教程里的步骤，就基本能让网站上线了。

我建站过程中遇到的最大障碍是如何将网站设置资料推送到GitHub。这一步很关键，因为Netlify是通过读取GitHub中的文件来更新网站的。关于如何上传的帮助教程[在此](https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/)。注意事项如下：

- 首先是确保你注册了一个GitHub账户，并且在账户中建立了一个文件夹(repository)。名字可以任意起。
- 然后遵照上面上传教程第2到第8步上传网站文件。特别注意第8步中的URL结尾要有.git

文件上传完毕后，就需要到Netlify网站中去设置了。这个上面Peter的[教程](https://notes.peter-baumgartner.net/tutorial/blogdown-tutorial-part-1/)里面有。我遇到的难题是最开始没有将Hugo的版本设置正确。在RStudio里面安装完blogdown以后，可以用blogdown::hugo_version()命令来查Hugo的版本。我安装的是0.53版，所以在Netlify的环境变量中要指明是0.53。截图参见Peter的教程。否则Netlify在解析网站文件的时候会报错(error code 255)。

另外，我在网站上线之后，对原来使用的模版不满意，所以决定更新模版，新的这个界面是blackburn。建议从Hugo的网站下载，解压，然后将blackburn文件夹拖到themes文件夹里。如果使用git clone直接加载，会导致下载一个.git文件，影响Netlify重新解析网站。

将blackburn放入themes文件夹之后，使用以下命令，将其上传到GitHub:

- git add themes/blackburn-master

- git commit -m “message” (message 处填入你自己中意的短语)

- git push -u origin master

注意在命令终端操作时，你需要cd到保存所有网站文件的那个目录中去。

如果你在网站上线后修改了config.toml和about.md文件，也要使用上面三步git命令，然后在Netlify中重新解析才能看到对网站的调整。


关于如何向GitHub上传文件，我最开始是参照Robert Myles  McDonnell的博客。原始链接在[这里](https://robertmylesmcdonnell.netlify.com/2018/01/03/blogdown-netlify/)。我自己的经验是掠过他的前3步，直接参考第4步，如何使用git，以及如何建立.gitignore文件。该文件是隐藏文件，不一定看的到，在mac里，在.gitignore所在的文件夹中，用cmd + shift + . 就可以看到所有隐藏文件，用textedit打开，输入public，保存即可。

掠过前3步的原因是Robert第一步就克隆GitHub里面的文件夹。而谢益辉和Peter都是首先从RStudio开始，先在线下生成所有的文件，然后再上传到GitHub。我个人的经验也是这个顺序比较好。在RStudio里面，点击new project..., 选择New Diectory，选择Website using blogdown，建立一个directory name之后所有的网站文件就会被加载到你所新建的目录里。接下来所有电脑命令终端的操作就都是在这个目录里。

后期对网站的优化还有很多工作要做，这些链接会有帮助：

- [blogdown电子书](https://bookdown.org/yihui/blogdown/)

- [Mike Treglia 的blogdown教程](https://mltconsecol.github.io/post/20170123_blogdown_hugo/)

- [如何给网站的菜单项添加徽标](https://tbradley1013.github.io/2018/08/24/add-rstudio-community-to-your-blogs-social-links/)

- [免费徽标下载](https://fontawesome.com/icons?d=gallery&m=free)

希望你很快能拥有自己的博客网站！
