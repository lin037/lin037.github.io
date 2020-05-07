---
title: 如何利用jekyll+github或jekyll+coding制作一个属于自己的博客.
author: 林叁柒
date: 2020-05-07 22:16:36 +0800
categories: [Jekyll, Jekyll搭建]
tags: [Jekyll, GitHub, coding, 博客, 搭建, 教程]
---

## 导语

或许有很多人想要有个地方说说话吧，也正因此，博客诞生了，博客就是网络日记，你可以在自己的博客上写写文章，记录一些事情，记录自己的成长什么的，就和我这个博客一样。而这篇文章就是简述如何利用jekyll+github/jekyll+coding搭建一个免费的个人博客。

## 注意事项

Jekyll的开发环境的安装，对于每种系统是有些不一样的，因为作者也没用过其他的操作系统，所以这篇文章是以Windows为主要，其他操作系统，可以结合本篇文章与Jekyll官方文档来部署开发环境。

Jekyll文档：[中文文档](https://www.jekyll.com.cn/)、[英文文档](https://jekyllrb.com/)

## 所需材料

- GitHub/coding账号——[GitHub注册](https://github.com/join?source=header-home)、[coding注册](https://e.coding.net/signup)
- git环境——[git安装教程](https://blog.csdn.net/huangqqdy/article/details/83032408)

------

## 正文

1. ### 安装Ruby+Devkit

   - [下载地址](http://rubyinstaller.org/downloads/)，下载**Ruby + Devkit 2.6.X**，大家可以根据自己的系统安装合适的，但记得要选带有Devkit的。

   -    官网可能会因为墙的原因，下载会很慢，作者已经下载x64的，x64的兄弟们可以在这里下载：[下载地址（密码：263811）](https://590m.com/file/26856128-442094414)。

   -    下载完后，直接打开下一步下一步地安装即可，选项什么的全默认即可，需注意的是：安装过程中，记得要确保**“Add Ruby executables to your PATH”** 选项选中，这是帮你自动配置环境变量的。

   -    安装完成后，在按键盘上的Windows+R键，在弹出的窗口中输入cmd，回车，调出cmd窗口，输入命令**ruby -v**和**gem -v**即可查看是否安装成功，出现版本号就是成功了。

   ```
   C:\Users\Administrator>ruby -v
   ruby 2.6.6p146 (2020-03-31 revision 67876) [x64-mingw32]
   
   C:\Users\Administrator>gem -v
   3.0.3
   ```

2. ### 换源

   - 因为官方源访问不了，所以我们要换源。

   - 命令`gem sources -l`可以查现有的源，默认是官方和淘宝源。

   - 命令`gem sources -r 源的地址`可以删除源，把已有的源删除，即上面查询到的结果。

   - 命令`gem sources -a https://gems.ruby-china.com/`可以添加我们可以用的源，具体可访问[链接地址](https://gems.ruby-china.com)。
	```
	C:\Users\Administrator>gem sources -l
   *** CURRENT SOURCES ***
   https://rubygems.org/
   https://ruby.taobao.org/
   
	C:\Users\Administrator>gem sources -r https://rubygems.org/
	https://rubygems.org/ removed from sources
	
	C:\Users\Administrator>gem sources -r https://ruby.taobao.org/
	https://ruby.taobao.org/ removed from sources
	
	C:\Users\Administrator>gem sources -l
	*** CURRENT SOURCES ***
	
	C:\Users\Administrator>gem sources -a https://gems.ruby-china.com/
	https://gems.ruby-china.com/ added to sources
	
	C:\Users\Administrator>gem sources -l
	*** CURRENT SOURCES ***
	https://gems.ruby-china.com/
	```

3. ### 安装Jekyll

   - 使用命令`gem install jekyll`安装Jekyll。

   - 使用命令`jekyll -v`查看是否安装成功，若出现版本号即为成功。
   
   ```
   C:\Users\Administrator>jekyll -v
	jekyll 4.0.0
	```

4. ### Jekyll的Hello World

   - 使用命令`jekyll new 项目名`即可创建一个Jekyll项目，过程可能有些慢，稍等一下即可。
   
   - 使用命令`cd 项目名`进入项目中。
   
   - 使用命令`jekyll serve`运行项目。
   
   - 项目启动后，可在浏览器打开http://localhost:4000查看博客了
   
    ```
   E:\lin037blog>jekyll new blog
   Running bundle install in E:/lin037blog/blog...
     Bundler: Fetching gem metadata from https://rubygems.org/...........
     Bundler: Fetching gem metadata from https://rubygems.org/.
     Bundler: Resolving dependencies...
     Bundler: Using public_suffix 4.0.4
     ......
     Bundler: Bundle complete! 6 Gemfile dependencies, 35 gems now installed.
     Bundler: Use `bundle info [gemname]` to see where a bundled gem is installed.
   New jekyll site installed in E:/lin037blog/blog.
   
   E:\lin037blog>cd blog
   
   E:\lin037blog\blog>jekyll serve
   Configuration file: E:/lin037blog/blog/_config.yml
               Source: E:/lin037blog/blog
          Destination: E:/lin037blog/blog/_site
    Incremental build: disabled. Enable with --incremental
         Generating...
          Jekyll Feed: Generating feed for posts
                       done in 0.709 seconds.
    Auto-regeneration: enabled for 'E:/lin037blog/blog'
       Server address: http://127.0.0.1:4000/
     Server running... press ctrl-c to stop.
    ```
   
   ![博客示例图](assets/img/sample/2020-05-07-Make-your-own-blog-with-jekyll-1/localhost4000.png)
   
   - 按ctrl+c可以关闭
   - 如此我们便建好了一个本地的博客，但如果需要让别人可以在网上看到的话，你还需要部署到服务器上面，而GitHub仓库和coding仓库是个不错的选择，免费且方便管理博客。
   
5. ### 部署到GitHub/coding

   - 先说一下GitHub和coding：

     GitHub规模大，较稳定，但毕竟是国外的，国内访问你懂的，并且因为某些原因，不能被百度搜索引擎的爬虫抓取；

     coding是国内的，服务不大稳定，但可以被百度搜索引擎的爬虫抓取。

   - 作者是俩者一起使用的，百度这边coding，谷歌那边GitHub。

   - 这里讲的是GitHub的部署，coding的操作也大同小异的：

     - 到GitHub中，创建一个仓库 [创建地址](https://github.com/new)。

     - 其中**Repository name**改为**你的用户名.github.io**，如我的用户名为**lin037**，所以我的**Repository name**应为**lin037.github.io。**

     - **Create repository**创建仓库。

     - 进入仓库页面，然后复制你的仓库地址，就在中间那个文本框那里。

     - 在你创建的Jekyll项目文件下，右键，如果你安装了git的话，会有个Git Bash Here的选项，点击会打开git窗口，在git窗口输入以下命令：

     ```
     echo "# 你的仓库名" >> README.md        //声明
     git init							//初始化
     git add .							//把当前所有文件提交到本地暂存区
     git commit -m "first commit"		  //提交到当前工作空间的修改内容
     git remote add origin 你的仓库地址	  //添加远程仓库地址
     git push -u origin master			  //提交到仓库
     ```
     
     - 然后输入密码即可提交到仓库。
     - 注意：有可能提交到仓库时会超时，多试俩次即可。
     - 具体执行过程：
     
     ```
     Administrator@WIN-5P2SESEF2HC MINGW64 /e/lin037blog/blog (master)
     $ git init
     Reinitialized existing Git repository in E:/lin037blog/blog/.git/
     
     Administrator@WIN-5P2SESEF2HC MINGW64 /e/lin037blog/blog (master)
     $ git add .
     ......
     
     Administrator@WIN-5P2SESEF2HC MINGW64 /e/lin037blog/blog (master)
     $ git commit -m "first commit"
     ......
     
     Administrator@WIN-5P2SESEF2HC MINGW64 /e/lin037blog/blog (master)
     $ git remote add origin https://github.com/MITSUKI-CYBERPUNK/MITSUKI-CYBERPUNK.github.io.git
     
     Administrator@WIN-5P2SESEF2HC MINGW64 /e/lin037blog/blog (master)
     $ git push -u origin master
     ......
     ```
     
     - 提交成功后，到仓库页面，点击**Settings**设置，往下拉，找到**GitHub Pages**选项开启pages功能，一般提交完成后自动会开启，而绿色框框的链接便是你的博客地址了，打开即可在线观看你的博客。
     - 一般地址为https://你设置的Repository name
     - 如此便部署完你的博客了，但样式还不是很好看，文章也不知道咋写，标题啥的也不知道咋修改，别急，往下看。

6. ### Jekyll目录结构

   ```
   _config.yml   Jekyll的配置文件
   _includes     include 文件所在的文件夹
   _layouts      模版文件夹
   _posts        自己要发布的文章
   _sites        预览时产生的文件都放在该文件夹中
   ```
   
7. ### 安装Jekyll主题

   - 你可以去这里找一个你喜欢的主题：[主题地址](https://jekyllthemes.dev/)

   - 如：作者选择的是Chirpy主题，便点击进Chirpy主题，查看GitHub，进入主题的GitHub仓库，复制别人的仓库克隆地址：https://github.com/cotes2020/jekyll-theme-chirpy.git，需注意的是，地址在**Clone or download绿色小按钮**那里。
   - 在你想下载的本地目录那里，打开gitbash窗口，输入指令`git clone 仓库地址`即可把别人的项目下载到本地。
   - 把下载下来的文件，按主题的文档删除一些文件，如Chirpy主题需删除**.travis.yml**和**.github**。
   - 把下载下来的文件复制到你原本已经上传过的项目那里，即第5步的项目那里，覆盖掉就对了。
   - 修改_config.yml配置文件，右键使用记事本打开即可，一般文件每一条配置都有注解的，把一些东西修改成自己的即可，下面是Chirpy主题我稍作修改后的（太多了，截取部分重要点的）：

   ```
   # The Site Settings
   # v2.0
   # https://github.com/cotes2020/jekyll-theme-chirpy
   # © 2017-2019 Cotes Chung
   # MIT licensed
   
   # jekyll-seo-tag settings › https://github.com/jekyll/jekyll-seo-tag/blob/master/docs/usage.md
   #--------------------------
   
   title: 叁柒博客                # 主标题，就是网页的标题
   
   tagline: 一个爱好超多的人              # 标语，就口号，个性签名
   
   description: >-                        # 网站介绍，会被用作seo meta和atom feed
      叁柒博客，博客嘛，当然就是给作者写一些文章，记录一些事情的网站啦。
    至于这个作者会记录些什么，看看博客有哪些类别就知道啦。
   
   # 改成你网站的url地址, 例如：'https://username.github.io'
   url: 'https://lin037.github.io/'
   
   author: 林叁柒                  # 改成你的全名
   
   avatar: /assets/img/sample/avatar.jpg   # 网站头像，logo啥的吧，应该。支持网络资源
   
   github:
     username: lin037             # 改成你的GitHub用户名
   
   twitter:
     username: Lin0372            # 改成你的twitter用户名
   
   social:
     name: 林叁柒                  # 它将在页脚显示版权所有者
     email: 1833340239@qq.com             # 改成你的邮箱地址
     links:
       # The first element serves as the copyright owner's link
       - https://twitter.com/username      # 改成你的twitter主页
       - https://github.com/username       #改成你的GitHub主页
       # Uncomment below to add more social links
       # - https://www.facebook.com/username
       # - https://www.linkedin.com/in/username
   
   google_site_verification: google_site_verification # 改成你的谷歌站长验证字符
   
   #--------------------------
   
   # if your site type is Project Pages site, change below value to '/projectname'
   baseurl: ''
   
   # Change to your timezone › http://www.timezoneconverter.com/cgi-bin/findzone/findzone
   timezone: Asia/Shanghai
   
   google_analytics:
     # 填下你的谷歌分析的ID
     id: ''
     # The Google Analytics pageviews switch.
   
     pv:
       # DO NOT enable it unless you know how to deploy the Google Analytics superProxy.
       enabled: false
       # the next options only valid when `google_analytics.pv` is enabled.
       proxy_url: ''
       proxy_endpoint: ''
       cache: false  # pv data local cache, good for the users from GFW area.
   
   disqus:
     comments: false  # disqus评论的开关，在咱们这被墙了，我们要用gitalk，所以关闭
     shortname: ''    # Fill with your Disqus shortname. › https://help.disqus.com/en/articles/1717111-what-s-a-shortname
   
   # Prefer color scheme setting, available values:
   #
   #     dual   - Follow the system prefer color by default, and a toggle will display
   #              in the left bottom of Sidebar, which used for switch the theme between dark and light.
   #
   #     light  - Use the light color scheme
   #
   #     dark   - Use the dark color scheme
   #
   theme_mode: dual
   
   # boolean type, global switch for ToC in posts.
   toc: true
   
   paginate: 10
   
   markdown: kramdown
   
   highlighter: rouge
   
   kramdown:
     input: GFM
     syntax_highlighter: rouge
     syntax_highlighter_opts: # Rouge Options › https://github.com/jneen/rouge#full-options
       css_class: 'highlight'
       # default_lang: console
       span:
         line_numbers: false
       block:
         line_numbers: true
         start_line: 1
   ......
   ```

   - 然后就是**_data**，**_includes**，**_layouts**这仨文件夹了，你可能需要一点html的知识，对着网站改就行了，看见哪里相似的，就改哪里，不对就改回。
   - 还有**assets**文件夹，这个是资源文件的，你看看哪里图片不对改就是了，注意名字要相同。
   - 其他的可以结合一下你的主题的文档，GitHub仓库那里。
   - 然后在项目文件下的gitbash命令框中输入命令`jekyll serve`即可在本地运行查看效果了。
   - 如果本地运行没错误的话，就可以上传了。
   - 依次使用以下命令上传：

   ```
   git add 要更新的文件
   git commit -m "更新说明"
   git push
   ```

   - 然后就可以去线上链接查看了。

8. ### 撰写新文章

   - 文章一般都是放在**_posts**文件夹下面，打开**_posts**文件夹。
   - 你会看到一个后缀名为**.md**的文件，这个就是文章文件了。
   - 文章文件有几点要求，就是文件名是以时间开头的，如：**2020-05-02-living-example.md**，建议文件名不要有中文。
   - 然后用记事本打开文件，头部会有类似于以下格式的头部信息，但每个主题样式都不大一样，每篇文章必须包含，你需要参考你自己的主题的，然后改成你自己的，以下是Chirpy主题的：

   ```
   ---
   title: 文章标题
   author: 作者
   date: 2020-05-02 23:30:04 +0800
   categories: [类别, 类别]
   tags: [标签, 标签, 标签, ...]
   ---
   ```

   - 上传也是一样的，使用以下命令：

   ```
   git add _posts/文章的文件名
   git commit -m "更新说明"
   git push
   ```

------

## 结尾

关于jekyll还有挺多东西的，接下来有空会更新jekyll添加评论功能和谷歌统计啥的，好吧是因为我还没研究透，要花时间研究。

对了，我的博客地址：[叁柒博客](https://lin037.github.io)，关注下呗~

可能大家搭建环境的时候会报些错误，或者我有哪里写得不对的地方，欢迎大家评论指出哈......