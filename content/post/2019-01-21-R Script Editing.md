---
title: 快速编辑R脚本文件的办法
author: 李泉
date: '2019-01-21'
slug: R
categories:
  - R
tags:
  - R 技巧
description: ''
topics: [R]
---

在R Markdown里面编辑R命令，预览然后输出成pdf、html或word都很方便。不过有一种情况下这种编辑方式还是不方便。就是当文本的绝大部分内容都是R命令，辅以少数说明文字时，这个时候在R Markdown文件里以R命令块的格式来添加R命令就很不方便。有一个简单的办法可以解决这个问题。

假设你有如下R脚本文件：

#' # This is just an R script
#' ## Rendered to a html report with knitr::spin()
#' * just by adding comments we can make a really nice output

#'
#' > And the code runs just like normal, eg. via `Rscript` after all
#' __comments__ are just *comments*.
#'
#' ## The report begins here
#+
knitr::kable(head(mtcars))

#' ## A chart
#+ fig.width=8, fig.height=8
heatmap(cor(mtcars))

#' ## Some tips
#'
#' 1. Optional chunk options are written using `#+`
#' 1. You can write comments between `/*` and `*/`


存成script.R, 然后在命令框中运行knitr::spin("script.R")， 就可以生成两个文件，script.md和script.html，后者可以看到非常整齐的输出。

上面这个脚本文件和一般R脚本文件唯一不同的地方就是每行开头，注释信息以#'开头，R命令以#+开头即可，其它写作方式和在R Markdown里都一样。

这种编辑方式方便快速将大量的R命令文件快速整理成方便发布的格式。

更多的解释在[这里](https://jozefhajnala.gitlab.io/r/r909-rmarkdown-tips/#creating-beautiful-multi-format-reports-directly-from-r-scripts)