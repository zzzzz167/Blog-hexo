---
title: 'hexo部署(一):本地部署'
date: 2021-02-23 23:47:57
tags: 
  - hexo
  - 网站
categories: 技术
---

## 前言

最近发现腾讯云搞得博客费钱太多，并且因为我是未成年嘛，也没有办法备案，于是就准备去租一个香港的对象存储，然后搞静态博客，最后我选择了hexo，如你所见这个博客就是由hexo所搭建的
<!-- more -->

## hexo简介

Hexo是一款基于Node.js的静态博客框架，依赖少易于安装使用，可以方便的生成静态网页托管在GitHub和Coding上，是搭建博客的首选框架。快速、简洁且高效的博客框架。Hexo 使用 [Markdown](http://daringfireball.net/projects/markdown/)（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

这次教程主要介绍：

- 最基本的部署
- 撰写属于你的第一篇文章
- 了解文章的基本结构

本文所采用的系统是MacOS，可能有些地方与Windows有所出入，如遇不会的地方还请评论区留下你的问题。

本文配有目录，可根据自己需求进行跳转

## 部署

### npm

#### 安装

在mac上部署npm其实吧也简单，需要用到homebrew，这部分我会单独开一篇文章来讲。

在这里我假设您已经安装好了homebrew

如何判断安装？

```bash
brew -v
```

如果出现版本号说明已经安装好

执行

```bash
brew update
```

更新homebrew

执行

```bash
brew install npm
```

进行安装npm。执行npm -v即可看到安装好的npm版本

#### 换源

终端执行：

```bash
npm config set registry https://registry.npm.taobao.org
```

npm安装与配置结束

### git

```bash
brew install git
```

即可安装完毕

### hexo

#### 安装

所有必备的应用程序安装完成后，即可使用 npm 安装 Hexo。

```bash
npm install -g hexo-cli
```

#### 建站

安装完成后，执行下述命令，hexo便会自动在指定文件夹添加所需文件。

```bash
hexo init <name>
cd <name>
npm install
```

执行完成后，使用

```bash
hexo g
hexo s
```

便可以在<http://localhost:4000中看到以下页面：>

![](https://image-xiaozhizhen.oss-cn-qingdao.aliyuncs.com/2-24.png)

恭喜你现在你的博客就算是在你的本地跑起来了

## 修改基本信息

现在让我们来看一看这个文件夹中的东西都是什么

```bash
.
├── _config.yml #网站的配置信息，您可以在此配置大部分的参数。
├── package.json #应用程序的信息。您可以自由移除留下你需要的东西
├── scaffolds #模版 文件夹。当您新建文章时，Hexo 会根据 scaffold 来建立文件。
├── source #资源文件夹是存放用户资源的地方
|   ├── _drafts
|   └── _posts
└── themes #主题 文件夹。Hexo 会根据主题来生成静态页面
```

不难看出“_config.yml”是这个站点的参数控制，以下是其翻译版本，加了一些必要配置

```bash
<_config.yml>

# Hexo Configuration
## Docs: https://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

title: Hexo
#站点标题
subtitle: ''
#站点副标题
description: ''
#站点描述
keywords:
#站点关键词多个时使用“,”分割
author: John Doe
#作者昵称
language: zh-CN
#网站语言（默认为en应改为zh-CN）
timezone: 'Asia/Shanghai'
#时区：使用电脑默认的就行

# URL
## Set your site url here. For example, if you use GitHub Page, set url as 'https://username.github.io/project'
#设置你的网站地址，比如说，如果你使用github page，设置url像这样“https://username.github.io/project”
url: http://example.com
permalink: :year/:month/:day/:title/
#文章链接格式（一定要规范，方便爬虫爬取信息）
permalink_defaults:
pretty_urls:
  trailing_index: true # Set to false to remove trailing 'index.html' from permalinks
  trailing_html: true # Set to false to remove trailing '.html' from permalinks

# Directory
source_dir: source
#资源文件夹，放在里面的东西就会生成出来
public_dir: public
#存放生成出来的静态文件夹
tag_dir: tags
#标签文件夹
archive_dir: archives
#归档文件夹
category_dir: categories
#分类文件夹
code_dir: downloads/code
#代码文件夹
i18n_dir: :lang
skip_render:
#不需要渲染的文件

# Writing
new_post_name: :title.md 
#默认的名称
default_layout: post
#默认的布局模版
titlecase: false
#是否将标题转化成标题形式
external_link:
  enable: true #在新建标签页中打开网页
  field: site 
  exclude: ''
filename_case: 0
render_drafts: false
#是否渲染草稿
post_asset_folder: false
#是否启用 Asset 文件夹
relative_link: false
#把链接改为与根目录的相对位置
future: true
#显示未来的文章
highlight: #代码块高亮显示
  enable: true
  line_number: true
  auto_detect: false
  tab_replace: ''
  wrap: true
  hljs: false
prismjs:
  enable: false
  preprocess: true
  line_number: true
  tab_replace: ''

# Home page setting
# path: Root path for your blogs index page. (default = '')
# per_page: Posts displayed per page. (0 = disable pagination)
# order_by: Posts order. (Order by date descending by default)
index_generator:
  path: ''
  per_page: 10 #每页数量
  order_by: -date #排序依据

# Category & Tag
default_category: uncategorized #默认分类
category_map: #分类别名
tag_map: #标签别名

# Metadata elements
## https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta
meta_generator: true

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD
time_format: HH:mm:ss
## updated_option supports 'mtime', 'date', 'empty'
updated_option: 'mtime'

# Pagination
## Set per_page to 0 to disable pagination
per_page: 10
pagination_dir: page

# Include / Exclude file(s)
## include:/exclude: options only apply to the 'source/' folder
include:
exclude:
ignore:

# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: landscape #设置使用的主题

# Deployment
## Docs: https://hexo.io/docs/one-command-deployment
deploy:
  type: ''

```

在修改完这些信息后，使用

```
hexo g
hexo s
```

便可在浏览器看到你修改后的效果

## 开始创作

你到现在已经完成了最最最基本的设置，现在便可以撰写文章了

#### 创建文章

- 命令行： 使用 `hexo new <title>`
- 手动创建：在hexo主目录下`source ->_posts`目录中创建`<title>.md`的文件

#### 初步感知

hexo的文章通常是由两部分构成的，分别是：

- Front-matter
- 正文

##### Front-matter

Front-matter 是文件最上方以 `---` 分隔的区域，用于指定个别文件的变量，举例来说：

```
---
title: Hello World
date: 2013/7/13 20:46:25
---
```

以下是预先定义的参数，您可在模板中使用这些参数值并加以利用。

| 参数         | 描述                 | 默认值                                                       |
| :----------- | :------------------- | :----------------------------------------------------------- |
| `layout`     | 布局                 | [`config.default_layout`](https://hexo.io/zh-cn/docs/configuration#文章) |
| `title`      | 标题                 | 文章的文件名                                                 |
| `date`       | 建立日期             | 文件建立日期                                                 |
| `updated`    | 更新日期             | 文件更新日期                                                 |
| `comments`   | 开启文章的评论功能   | true                                                         |
| `tags`       | 标签（不适用于分页） |                                                              |
| `categories` | 分类（不适用于分页） |                                                              |
| `permalink`  | 覆盖文章网址         |                                                              |

只有文章支持分类和标签，您可以在 Front-matter 中设置。在其他系统中，分类和标签听起来很接近，但是在 Hexo 中两者有着明显的差别：分类具有顺序性和层次性，也就是说 `Foo, Bar` 不等于 `Bar, Foo`；而标签没有顺序和层次。

```
categories:
- Diary
tags:
- PS3
- Games
```

##### 正文

正文部分使用md语法撰写，详情可查看我的上一篇文章

#### 更新

在你重新对你的博客做出更新后，通常需要部署到网站，下面介绍几个简单的指令。

`hexo clean`:清理已经生成的静态文件

`hexo g`:生成所需的静态文件

`hexo s`启动本地服务，默认访问网站：<http://localhost:4000>

`hexo d`:部署网站

> 感谢您对本文的阅读，如果遇到不理解的地方，可以通过评论的方式进行交流
>
> 下一篇将会将博客部署在Github Pages上
