title: "Hexo搭建Wiki"
date: 2015-04-30 04:09:41
categories: Hexo
toc: false
---
- 2015-4-30 第一次编写


---
![此处输入图片的描述][1]
##0x01准备：
1. [tommy351][2]编写的静态博客框架[Hexo][3]（目前版本是3.0.x）
2. [Wixo][4]的主题
3. GitHub的repos的gh-pages 分支放置wiki，托管于GitHub的Pages服务上
4. 源码放置在Github同一个repos下的source分支下进行版本管理
5. [Travis CI][5]自动化测试框架自动编译网站

<!--more-->
##0x02过程：

### 安装NodeJs
![此处输入图片的描述][6]
因为Hexo是使用Nodejs编写的，所以需要部署NodeJs的环境

- [下载nodejs][7]

Windows 可以直接下载到安装包安装即可，其它系统稍后补充


### 安装Hexo(3.x以上)

#### 安装hexo-cli

    $ npm install hexo-cli -g

3.x以上版本相比2.x以下版本使用上有差别，3.x版本模块化程度较高，你可以不用经常更新hexo-cli，但是多个hexo版本可以共存

#### 初始化目录

    $ hexo init Wiki

> PS I:\> hexo init Wiki
    INFO  Copying data to I:\Wiki
    INFO  You are almost done! Don't forget to run 'npm install' before you start blogging with Hexo!
    
这样就会建立一个Wiki的文件夹，在文件夹里已经做了一些初始化的工作:

- 目录结构：
```
-- wiki
    |-- scaffolds           #工具模板
    |       |-- draft.md
    |       |-- page.md
    |       |-- post.md
    |-- source
    |   |-- _posts          #文章文件夹
    |         |-- hello-world.md
    |-- themes              #主题文件夹
    |     |-- landscape     # 默认主题文件夹
    |-- .gitignore
    |-- _config.yml         #全局配置文件
    |-- package.json        #插件的配置，使用npm install --save 会写入这里
```
另外还有`source/_drafts `存放的是草稿
 
#### 安装 Hexo 

切到Wiki目录下，然后安装指定版本的Hexo > 3.0

    $ npm install hexo --save
    
![此处输入图片的描述][8]
然后，安装相关默认的npm插件

    $ npm install 

![此处输入图片的描述][9]

```
hexo-renderer-ejs@0.1.0 node_modules\hexo-renderer-ejs
├── ejs@1.0.0
└── lodash@2.4.2

hexo-generator-index@0.1.1 node_modules\hexo-generator-index
├── object-assign@2.0.0
└── hexo-pagination@0.0.2 (utils-merge@1.0.0)

hexo-generator-tag@0.1.1 node_modules\hexo-generator-tag
├── object-assign@2.0.0
└── hexo-pagination@0.0.2 (utils-merge@1.0.0)

hexo-generator-category@0.1.2 node_modules\hexo-generator-category
├── object-assign@2.0.0
└── hexo-pagination@0.0.2 (utils-merge@1.0.0)

hexo-generator-archive@0.1.2 node_modules\hexo-generator-archive
├── object-assign@2.0.0
└── hexo-pagination@0.0.2 (utils-merge@1.0.0)

hexo-renderer-marked@0.2.5 node_modules\hexo-renderer-marked
├── object-assign@2.0.0
├── marked@0.3.3
├── strip-indent@1.0.1 (get-stdin@4.0.1)
└── hexo-util@0.1.6 (ent@2.2.0, bluebird@2.9.25, highlight.js@8.5.0)

hexo-renderer-stylus@0.2.3 node_modules\hexo-renderer-stylus
├── stylus@0.50.0 (css-parse@1.7.0, mkdirp@0.3.5, sax@0.5.8, source-map@0.1.43, debug@2.1.3, glob@3.2.11)
└── nib@1.1.0 (stylus@0.49.3)

hexo-server@0.1.2 node_modules\hexo-server
├── object-assign@2.0.0
├── open@0.0.5
├── mime@1.3.4
├── bluebird@2.9.25
├── chalk@0.5.1 (ansi-styles@1.1.0, escape-string-regexp@1.0.3, supports-color@0.2.0, strip-ansi@0.3.0, has-ansi@0.1.0)
├── compression@1.4.3 (vary@1.0.0, on-headers@1.0.0, bytes@1.0.0, debug@2.1.3, compressible@2.0.2, accepts@1.2.5)
├── morgan@1.5.2 (basic-auth@1.0.0, depd@1.0.1, debug@2.1.3, on-finished@2.2.1)
├── connect@3.3.5 (utils-merge@1.0.0, parseurl@1.3.0, debug@2.1.3, finalhandler@0.3.4)
└── serve-static@1.9.2 (utils-merge@1.0.0, escape-html@1.0.1, parseurl@1.3.0, send@0.12.2)
```
默认安装了：

 - [hexo-renderer-ejs][10]   [EJS][11]渲染器
 - [hexo-generator-index][12]   用来配置每页展示文章的数目
 - [hexo-generator-tag][13] 标签生成
 - [hexo-generator-category][14] 目录生成
 - [hexo-generator-archive][15] 文章生成
 - [hexo-renderer-marked][16] markdown 渲染器
 - [hexo-renderer-stylus][17] CSS渲染器
 - [hexo-server][18] Server module for Hexo

安装其他常用的插件：

    $ npm install hexo-deployer-git --save
    $ npm install hexo-generator-feed@1 --save
    $ npm install hexo-generator-sitemap@1 --save
    $ npm install hexo-fs --save
    $ npm install hexo-renderer-mathjax --save

- [hexo-deployer-git][19] 
> Git deployer plugin for Hexo.

- [hexo-generator-feed][20]
> Feed generator for Hexo.

- [hexo-generator-sitemap][21]
> Sitemap generator for Hexo

- [hexo-fs][22]
> 文件 IO 为了要使用mathjax模块

- [hexo-renderer-mathjax][23]
> Add support of MathJax for Hexo.


更多的插件参见[官网插件列表][24] 或者 [Github上的列表][25]
 
### 配置 Hexo
 
 初始化目录
 
    $ git init

创建`source`分支

    $ git checkout -b source

####　安装与配置主题
- fork 主题

从[主题列表][26] 挑选自己喜欢的主题,然后fork到自己的repos，这里使用的是Wiki主题Wixo

> wiki for hexo 

选取 w i x o

- 修改主题配置文件

```
    $ cd .. #切换到上级目录
    $ git clone https://github.com/zhiyue/hexo-theme-wixo themes/wixo
```

修改完成后再push上GitHub上

- 下载主题

```
$ cd Wiki     #切换到Wiki目录
$ git clone https://github.com/zhiyue/hexo-theme-wixo themes/wixo
```

- 使用主题
去全局配置文件 `_config.yml` 修改参数
```
# Extensions
## Plugins: http://hexo.io/plugins/
## Themes: http://hexo.io/themes/
theme: wixo #这里修改为主题的名字
```
- 配置主题
`wixo`主题配置：

```
rss: atom.xml
fancybox: true
favicon: favicon.ico
fold: true
google_analytics: 
```


这个不同的主题配置会很不一样，下面这个是`modernist`主题的配置
```
menu:
  Home: /
  Archives: /archives
rss: /atom.xml

archive_date_format: MMM DD
fancybox: true

duoshuo_shortname: zhiyue

google_analytics:
favicon: /favicon.ico

```

- 使用子模块管理主题

```
$ git submodule add https://github.com/zhiyue/hexo-theme-wixo.git themes/wixo
```

![此处输入图片的描述][27]

- 主题的更新
如果fork的主题作者有更新，可以在GitHub上pull过来然后再合并，然后在自己的blog的目录下要注意一下子模块的更新模式

``` 
$ git submodule init 
$ git submodule update
$ cd themes/wixo
$ git checkout HEAD  #切换到最新的head
$ cd -
$ git add.
$ git commit -m "update submodule " #更新submodule的标记
```

####　全局配置

修改_config.yml 文件只需修改几个，通常需要修改的地方:

- 站点名称
- URL格式
- 归档设置
- disqus评论用户名
- 部署配置

> 注意冒号后面添加一个半角空格 再设置参数


下面是我的`_config.yml`的配置
```
# Hexo Configuration
## Docs: http://hexo.io/docs/configuration.html
## Source: https://github.com/hexojs/hexo/

# Site
title: zhiyue   ## 网站标题
subtitle:       ## 网站副标题
description:    ## 网站描述
author: zhiyue  ## 您的名字
language: zh_CN ## 网站使用的语言
timezone:       ## 网站时区。Hexo 预设使用您电脑的时区

# URL
## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
##如果您的网站存放在子目录中，例如 http://yoursite.com/blog，则请将您的 url 设为 http://yoursite.com/blog 并把 ##root 设为 /blog/。
url: http://blog.printf.me              ## 网址
root: /                                 ## 网站根目录
permalink: :year/:month/:day/:title/    ## 文章的 永久链接 格式
permalink_defaults:                     ## 永久链接中各部分的默认值 



# Directory
source_dir: source          ## 资源文件夹，这个文件夹用来存放内容。
public_dir: public          ## 公共文件夹，这个文件夹用于存放生成的站点文件。
tag_dir: tags               ## 标签文件夹
archive_dir: archives       ## 归档文件夹
category_dir: categories    ## 分类文件夹
code_dir: downloads/code    ## Include code 文件夹
i18n_dir: :lang             ## 国际化（i18n）文件夹
skip_render:                ## 跳过指定文件的渲染，您可使用 glob 来配置路径。

# Writing
new_post_name: :title.md                ## File name of new posts
default_layout: post                    ## 预设布局
titlecase: false                        ## Transform title into titlecase
external_link: true                     ## Open external links in new tab
filename_case: 0                        ## 把文件名称转换为 (1) 小写或 (2) 大写
render_drafts: false                    ## 显示草稿
post_asset_folder: false                ## 启动 Asset 文件夹
relative_link: false                    ## 把链接改为与根目录的相对位址
future: true                            ## 显示未来的文章
highlight:                              ## 代码块的设置
  enable: true                          ## 启用
  line_number: true                     ## 行号
  tab_replace: true                     ## tab 替换

# Category & Tag
default_category: uncategorized         ## 默认分类
category_map:                           ## 分类别名
tag_map:                                ## 标签别名

# Date / Time format
## Hexo uses Moment.js to parse and display date
## You can customize the date format as defined in
## http://momentjs.com/docs/#/displaying/format/
date_format: YYYY-MM-DD                 ## 日期格式
time_format: HH:mm:ss                   ## 时间格式

# Pagination
## Set per_page to 0 to disable pagination
per_page: 10                            ## 每页显示的文章量 (0 = 关闭分页功能)
pagination_dir: page                    ## 分页目录

# Extensions
## Plugins: http://hexo.io/plugins/
## Themes: http://hexo.io/themes/
theme: modernist                        ## 当前主题名称

# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:                                 ##部署
  type:
```
### 写文章

    $ hexo new post "tiltle"
这样就会在`source/_post/`下创建一个`tiltle.md`
Hexo使用markdown语法的纯文本存放文章 后缀为.md 你可以在_post文件夹里面新建这个后缀的.md文件使用的全是UTF-8编码

格式如下：

    title: title #文章标题
    date: 2015-02-05 12:47:44 #文章生成时间
    categories: #文章分类目录 可以省略
    tags: #文章标签 可以省略
    description: #你对本页的描述 可以省略
    
多标签注意语法格式 如下:
```
      tags:
        - 标签1
        - 标签2
        - 标签3
        - etc...
```
正文中可以使用<!--more-->设置文章摘要 如下:
```
  以上是文章摘要
    <!--more-->
    以下是余下全文
```
### 生成与部署

- 生成blog静态文件：

```
    $ hexo g
```
![此处输入图片的描述][28]

- 在本地环境测试：

```
    $ hexo s
```

![此处输入图片的描述][29]

#### GitHub 配置
- 创建gh-pages分支
如果要部署在github上，必须名称叫gh-pages。所以先创建一个叫gh-pages的分支

```
$ git checkout --orphan gh-pages
$ git rm -rf .    # 砍掉所有档案重來
# 加新档案
## git add .
$ git commit -m 'create new branch'
```
- 提交到GitHub
在GitHub创建一个新的repos，然后再本地使用以下命令：
```
    $ git remote add origin https://github.com/(github用户名)/(项目名称).git  ##添加远程仓库
    $ git push --all origin                           ##push
```
- 自定义域名设置 
在`source`文件夹下创建`CNAME`文件 写入你的自定义域名
```
    blog.printf.me
```
- 设置dnspod
添加`CNAME`记录 记录值`zhiyue.github.io.`
![此处输入图片的描述][30]
- 404 页面 和 favicon.ico
在`source`文件夹下 创建`404.html` 和 把`favicon.ico` 放置至此

- deploy 配置
修改_config.yml文件
```
# Deployment
## Docs: http://hexo.io/docs/deployment.html
deploy:
  type: git
  message: update
  repo: https://github.com/zhiyue/blog.git
  branch: gh-pages
```

### 配置travis ci 

- 生成`Personal access tokens` 
在[GitHub token 生成页面][31]按照以下步骤生成一个可以让第三方访问的`token`，它具有可以写`repos`的权限。这样就可以在生成网站的时候通过这个`token`提交到`repos`上了。
![generate token][32]

- 启用`travis ci`
登陆[travis ci][33]绑定GitHub的账户，`travis ci`会同步`repos`的列表，选择你想启用自动化测试的`repos`
![travis ci ][34]

- 编写`.travis.yml`
`travis ci`会依据`.travis.yml`进行一些环境的设置安装以及后续的测试。下面的`.travis.yml`是参考网上的yml编写的
```
# Deploy hexo site by travis-ci
# https://github.com/jkeylu/deploy-hexo-site-by-travis-ci
# LICENSE: MIT
#
# 1. Copy this file to the root of your repository, then rename it to '.travis.yml'
# 2. Replace 'YOUR NAME' and 'YOUR EMAIL' at line 29
# 3. Add an Environment Variable 'DEPLOY_REPO'
#     1. Generate github access token on https://github.com/settings/applications#personal-access-tokens
#     2. Add an Environment Variable on https://travis-ci.org/{github username}/{repository name}/settings/env_vars
#         Variable Name: DEPLOY_REPO
#         Variable Value: https://{githb access token}@github.com/{github username}/{repository name}.git 
#         Example: DEPLOY_REPO=https://6b75cfe9836f56e6d21187622730889874476c23@github.com/jkeylu/test-hexo-on-travis-ci.git

language: node_js

node_js:
  - "0.12"  #设置node_js的版本

branches:
  only:
    - source    #检测的分支，一旦分支有新的提交就会触发脚本

before_install: #安装前的工作
- npm install -g hexo-cli

install:
#- npm install hexo-renderer-ejs@0.1.0 --save
#- npm install hexo-renderer-marked@0.1.0 --save
#- npm install hexo-renderer-stylus@0.1.0 --save
#- npm install hexo-generator-feed@0.2.1 --save
#- npm install hexo-generator-sitemap@0.2.0 --save
#- npm install hexo-tag-bootstrap@0.0.6 --save
- npm install


script:                         #运行的测试脚本
  - "git submodule init"
  - "git submodule update"
  - "hexo generate "
  
after_success:                      #push到github上
  - "git clone $DEPLOY_REPO git_deploy"
  - "cd git_deploy"
  - "git checkout gh-pages"
  - "cd .."
  - "rm -r git_deploy/*"
  - "cp -r public/* git_deploy"
  - "cd git_deploy"
  - "git config --global push.default simple"
  - "git config --global user.name 'zhiyue'"
  - "git config --global user.email cszhiyue@gmail.com"
  - "git add -A"
  - "git commit -m 'Site updated'"
  - "git push -q"
```
- 设置环境变量`DEPLOY_REPO`
   `.travis.yml`中用到的`DEPLOY_REPO`可以按照图片的步骤设置

![genertare var][35]


- travis ci 自动化生成与部署
 
![此处输入图片的描述][36]



- 网站截图：

![此处输入图片的描述][37]

##0x03 参考：

- [Hexo 3.0 靜態博客使用指南][38]
- [使用Jekyll在Github上搭建个人博客（将本地博客上传至github）][39]
- [如何建立一個沒有 Parent 的獨立 Git branch][40]
- [使用Git将本地代码上传到GitHub][41]

---
todo:
- 补充其他系统的详细情况
- 补充多说插件和谷歌analyse
- ~~详细补充配置文件~~
- ~~加配图~~

---


  [1]: http://7xilqm.com1.z0.glb.clouddn.com/Hexo_wiki/Hexo.png
  [2]: http://twitter.com/tommy351
  [3]: http://hexo.io/
  [4]: https://github.com/wzpan/hexo-theme-wixo/
  [5]: https://travis-ci.org/
  [6]: http://7xilqm.com1.z0.glb.clouddn.com/Hexo_wiki/NodeJs.png
  [7]: https://nodejs.org/
  [8]: http://7xilqm.com1.z0.glb.clouddn.com/Hexo_wiki/hexo_install.png
  [9]: http://7xilqm.com1.z0.glb.clouddn.com/Hexo_wiki/npm_install.png
  [10]: https://github.com/hexojs/hexo-renderer-ejs
  [11]: https://github.com/tj/ejs
  [12]: https://github.com/hexojs/hexo-generator-index
  [13]: https://github.com/hexojs/hexo-generator-tagtps://github.com/hexojs/hexo-generator-index
  [14]: https://github.com/hexojs/hexo-generator-categoryr-tagtps://github.com/hexojs/hexo-generator-index
  [15]: https://github.com/hexojs/hexo-generator-archive
  [16]: https://github.com/hexojs/hexo-renderer-marked
  [17]: https://github.com/hexojs/hexo-renderer-stylus
  [18]: https://github.com/hexojs/hexo-server
  [19]: https://github.com/hexojs/hexo-deployer-git
  [20]: https://github.com/hexojs/hexo-generator-feed
  [21]: https://github.com/hexojs/hexo-generator-sitemap
  [22]: https://github.com/hexojs/hexo-fs
  [23]: https://github.com/phoenixcw/hexo-renderer-mathjax
  [24]: http://hexo.io/plugins/
  [25]: https://github.com/hexojs/hexo/wiki/Plugins
  [26]: https://github.com/hexojs/hexo/wiki/Themes
  [27]: http://7xilqm.com1.z0.glb.clouddn.com/Hexo_wiki/git_submodule.png
  [28]: http://7xilqm.com1.z0.glb.clouddn.com/Hexo_wiki/hexo_g.png
  [29]: http://7xilqm.com1.z0.glb.clouddn.com/Hexo_wiki/preview.png
  [30]: http://7xilqm.com1.z0.glb.clouddn.com/Hexo_wiki/dnspod.png
  [31]: https://github.com/settings/tokens
  [32]: http://7xilqm.com1.z0.glb.clouddn.com/Hexo_wiki/generate_token.png
  [33]: https://travis-ci.org
  [34]: http://7xilqm.com1.z0.glb.clouddn.com/Hexo_wiki/travis.png
  [35]: http://7xilqm.com1.z0.glb.clouddn.com/Hexo_wiki/create_var.png
  [36]: http://7xilqm.com1.z0.glb.clouddn.com/Hexo_wiki/test.png
  [37]: http://7xilqm.com1.z0.glb.clouddn.com/Hexo_wiki/wiki_2.png
  [38]: http://ippotsuko.com/build-your-hexo-blog-3/
  [39]: http://segmentfault.com/a/1190000000406019
  [40]: https://ihower.tw/blog/archives/5691
  [41]: http://blog.csdn.net/u010520912/article/details/18993001