---
title: "搭建 hugo 博客"
date: 2019-02-22T22:49:02+08:00
tags: ["blog", "hugo"]
categories: ["blog"]
---

![hugo-logo-wide](/images/init_hugo/hugo-logo-wide.svg)

目前比较流行的 blog 系统有 hexo 和 hugo。前者基于 node.js，插件、主题丰富；后者基于 golang，插件、主题没有前者丰富，但也够用，性能比前者强。嘛，毕竟自己是吃后端饭的，工作也以 golang 为主。自己的 blog 就选择 hugo 了。

<!--more-->

## 安装 hugo & 初始化 blog

1. 首先使用 `brew install hugo` 安装 hugo；
2. 执行 `hugo new site blog` 初始化一个 blog；
3. 执行 `hugo server -D` 开启 debug 预览模式。

## 配置 even 主题

hugo blog 主题比较多，可以去[这里](https://themes.gohugo.io/tags/blog/)选择。个人比较喜欢使用比较多的 even，毕竟流行的东西资料多，适合入门。

```sh
cd blog
git submodule add https://github.com/olOwOlo/hugo-theme-even themes/even
# 需要复制一份 demo 配置文件到本地配置文件路径
cp themes/even/exampleSite/config.toml .
```

配置比较多，刚入门只做了以下几个简单修改。

```toml
[author]                  # essential                     # 必需
  name = "your name"

logoTitle = "your logo title"        # default: the title value    # 默认值: 上面设置的title值

# show word count and read time ?                       # 是否显示字数统计与阅读时间
moreMeta = true
```

## 配置评论区

[这篇文章](https://blog.shuiba.co/comment-systems-recommendation)详细对比了各种 blog 评论系统，个人比较喜欢的评论区插件有以下两个：

1. Disqus: 老牌评论系统，blog 评论系统中做的最好的，缺点是由于不可抗力，国内用户访问受限。  
    ![disqus_preview](/images/init_hugo/disqus_preview.png)  
  
2. gitalk: 基于 github issues 和 oauth 的评论系统，比同样原理的 gitment 样式要好一些，但是其 oauth 授权太大了，客户可以在 blog 页面上获取 oauth app id 和 app secret，这样引起了个人的强烈不适，所以放弃了这个方案。  
    ![gitalk_preview](/images/init_hugo/gitalk_preview.png)

综上，最后选择使用 Disqus 作为个人 blog 的评论系统，注册 Disqus 账号后，申请 shorname，在 config.toml 中配置。

```toml
disqusShortname = "your disqus shorname"      # disqus_shortname
```

另外，[官网](https://gohugo.io/content-management/comments/)中介绍了一些别的评论系统，由于搜索到的资料有限，没有继续研究下去。

## 部署

1. 在 github 上创建一个 `<your-github-name>.github.io` 的项目；

2. 执行 `hugo` 编译；

3. 进入 `public` 目录；

4. 执行以下命令，将编译后内容推送到 github 上:

    ```sh
    echo "# <your-github-name>.github.io" >> README.md
    git init
    git add .
    git commit -m "first commit"
    git remote add origin git@github.com:<your-github-name>/<your-github-name>.github.io.git
    git push -u origin master
    ```
5. 访问 `https://<your-github-name>.github.io`

## 参考
* [Hugo中文文档](http://www.gohugo.org/)
* [第三方评论系统推荐 • 水八口记](https://blog.shuiba.co/comment-systems-recommendation)
