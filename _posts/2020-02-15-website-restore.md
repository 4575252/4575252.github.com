---
layout: post
title: '启航，寻找那片OnePiece'
# subtitle: '新冠封闭期，重启个人站点'
date: 2020-02-15
categories: public #开放到首页
tags: git jekyll ruby
cover: '/assets/pic/bg/post-bg-universe.jpg'
---

> 新冠病毒肆虐期间，在家闲的那个蛋疼，也不知道未来和意外那个先来，想想还有好多梦想没有去追索，先从这里开始，**一起努力吧**！

## 一、目标

1. 建设个人博客一套，为下一步梦想推进，暂定GitHub+Jekyll的方式；
2. 将各领域的知识汇总、提炼，发布到博客上；
3. 补充汇总知识盲区；

## 二、安装过程

### 1、准备工具

- 源码管理工具：Git Bash, Git Gui
- 源码仓库&空间商&顶级域名：GitHub 注册、开启[owner].github.io仓库并配置个人域名
- 本地开发及远端运行环境：Ruby、Bundle及国内加速源，windows，支撑jekyll
- 博客中间件：Jekyll、Jekyll Page、H2O主题，动态渲染
- 博文编写：Typora，markdown

### 2、首次搭建过程（一次性）

#### 	2.1 服务端：GitHub注册、开启【所有者】仓库、配置个人域名

- GitHub注册参考**附录一**即可，新开仓库必须要用**owner**.github.io 这个名称(注：owner就是个人github账户)

- 仓库开启后，在setting->GitHub Pages，配置源码分支为master，定义域名为个人域名，此时会在code界面看到一个自动生成的cname， 另https一般要等一两个小时才可开启

- 域名解析（IP第三段可以是108，109，110，通过ping可以得知）

  | 主机记录 | 记录类型 | 记录值          |
  | :------- | -------- | --------------- |
  | www      | CNAME    | owner.github.io |
  | @        | A        | 185.199.109.153 |

  

- 用站长网的超级 ping.chinaz.com，感觉可以加速国内节点的解析

- 测试可简单放个index.html 

#### 	2.2 本地端：Git下载安装及配置、GitHub联调

- 建议捋顺后，尽量用Git Gui简化工作，具体可参考附录3

- Git Bash和Git Gui [官网下载](https://git-scm.com/downloads)， 安装不建议默认**program files** 路径，有空格，容易出诡异的事

- 打开Git Bash 配置Git用户名及本地邮箱

  ``` shell
  git config --global user.name "lzh.home.desktop" //可以随意输入，以后提交的分支都会有这个身份
  git config --global user.email "4575252@gmail.com" // 输入有效邮箱
  ```

  

- 打开Git Bash 生成密钥对

  ``` shell
  ssh-keygen -t rsa -C "your@email.com" （引号里填你上面设置的邮箱），然后一直回车就好
  ```

  出现RSA 2048，代表成功

- 将用户目录下的.ssh目录中的pub公钥文件用文本编辑器打开，添加到github或其他源码托管工具个人设置页的ssh选项中

- 测试密钥对是否有效

  ``` SHELL
  ssh -T git@github.com
  ```

  回车后出现：You’ve successfully authenticated, but GitHub does not provide shell access 。这就表示已成功连上github。

- 将GitHub上的仓库和本地仓库进行关联

  ```shell
  echo "# blog"  >> README.md
  # 初始化git项目
  git init
  # 把所有文件加入版本管理
  git add README.md
  # 提交到本地仓库
  git commit -m "初始化项目"
  # 添加远程仓库，git@github.com:yiifaa/yii-webapp-docker.git为远程仓库地址
  git remote add origin git@github.com:owner/owner.github.io.git
  # 推送到远程仓库
  git push -u origin master
  ```

  提交成功后，用git gui进行，remote-》fetch， Meger-》local的下拉合并操作，验证上下行都OK；如果同步有冲突，勾选 force

  

#### 	2.3 本地端：Windows环境Ruby安装、国内加速源

- 参考附录1

- 先安装msy2和ruby的离线安装包， [rubyGem离线包](https://rubygems.org/pages/download)

- 配置国内[加速源](https://gems.ruby-china.com/)

  ``` shell
  # 查看当前版本，并更新
  $ gem update --system # 这里请翻墙一下
  $ gem -v
  2.6.3
  
  # 切换国内源
  $ gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
  $ gem sources -l
  https://gems.ruby-china.com
  # 确保只有 gems.ruby-china.com
  
  
  #Bundler 的 Gem 源代码镜像命令。
  $ bundle config mirror.https://rubygems.org https://gems.ruby-china.com
  
  #ruby离线安装时连带安装Msy2的MINGW和 dev toolchain，如果失败，可任起一个cmd执行以下命令重新执行
  # 全局命令：安装 Ruby 所需的依赖，选3
  ridk install
  
  
  # 安装rubyGem
  $ cd {unzip-path} // unzip-path表示解压的路径
  $ ruby setup.rb
  ```

  

#### 	2.4 本地端：Jekyll安装调试，主题下载及个人定制

  - #### 安装Jekyll，jekyll-paginate，验证

    ``` shell
    gem install jekyll bundler jekyll-paginate
    bundle install
    jekyll -v
    
    # 新建一个blog测试
    jekyll new myBlog
    cd myBlog
    jekyll serve
    
    # 如果4000端口被占用，可以修改端口
    jekyll serve -P 5555
    ```

    在浏览器里输入： [http://localhost:4000](http://localhost:4000/)，就可以看到你的博客效果了。
    
- 安装[H20主题](https://github.com/kaeyleo/jekyll-theme-H2O)， [参考样例](https://jingwei.link/)

  ```shell
# 新安装其实就是克隆这个主题，解压覆盖本地仓库即可
  
# 更换图片、文字，主要配置是_config.yml
  
# 文章发布到post文件夹，jekyll serve如果开着会动态编译，除了全局配置
  ```

  

- jekyll的目录结构**

  我们只需要关注几个核心的目录结构如下（可以自己创建）：

  - `_layouts` （存放页面模板，md或html文件的内容会填充模板）

  - `_sass`（存放样式表）

  - `_includes` （可以复用在其它页面被include的html页面）

  - `_posts`（博客文章页面）

  - `assets`（原生的资源文件）

  - - `js`
    - `css`
    - `image`

  - `_config.yml` （全局配置文件）

  - `index.html, index.md, README.md` （首页index.html优先级最高，如果没有index，默认启用README.md文件）

  - `自定义文件和目录`

#### 	2.5 本地端：Jekyll点评及其他插件

#### 	2.6 本地端：Typora编写及Git发布、同步

### 3、新电脑搭建（更换电脑、多地办公之用）

执行第2.2 - 2.6即可；

## 三、补充

- **CDN加速** 配置不难，原先域名解析 A->B,变成 A->C->B，不过被DDOS，流量费惊人，暂时先搁置

- **Github Pages的限制**

  Github Pages 并不是无限存储和无限流量的静态站点服务，一些限制如下：

  - 内容存储不能超过1GB。
  - 每个月100GB流量带宽。
  - 每小时编译构建次数不超过10次。（在线修改重新编译并未发现这个限制）
  - 更多参看官方说明：[usage-limits](https://help.github.com/en/github/working-with-github-pages/about-github-pages#usage-limits)。

### 附：参考材料

- [1 GitHub的注册与使用（详细图解）](https://blog.csdn.net/p10010/article/details/51336332)
- [2 快速在 Windows 上搭建 Jekyll 开发环境](https://blog.walterlv.com/post/setup-jekyll-in-windows.html)
- [3 Git可视化极简易教程 — Git GUI使用方法](https://www.runoob.com/w3cnote/git-gui-window.html)

