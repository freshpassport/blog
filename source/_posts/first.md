---
title: 博客搭建成功
date: 2016-05-25 14:05:49
categories: 博客
tags:
toc: true
---

祝贺博客搭建成功。顺便把hexo搭建博客的过程记录一下。。。

<!--more-->

## 什么是hexo
hexo可以用于在github部署静态页面的一个工具，可以参考[hexo官网](https://hexo.io/zh-cn/)。
有关hexo的优点可以查看[谷歌](https://www.google.com.hk/search?q=hexo+%E4%BC%98%E7%82%B9&gws_rd=ssl)或者[百度](https://www.baidu.com/s?wd=hexo%20%E4%BC%98%E7%82%B9&rsv_spt=1&rsv_iqid=0x88b0cd700002097d&issp=1&f=8&rsv_bp=0&rsv_idx=2&ie=utf-8&tn=baiduhome_pg&rsv_enter=1&rsv_sug3=12&rsv_sug1=5&rsv_sug7=100&rsv_sug2=0&inputT=3991&rsv_sug4=3991)

## 环境
* 系统：debian 8.4 (GNOME3桌面)
* 工具：nodejs(npm), git
  debian自带的nodejs和npm版本比较低，后面安装会遇到好多问题，建议使用官网的最新版本
  我用的是v6.2.0 [稳定版](https://nodejs.org/dist/v6.2.0/node-v6.2.0-linux-x64.tar.gz)
  下载到本地解压缩，然后把node-v6.2.0-linux-x64/bin目录加入到系统的$PATH环境变量即可

## hexo安装&配置
总的来说hexo安装和配置比较简单的，具体可以参考[官网文档](https://hexo.io/zh-cn/docs/)
这里说一下我的安装步骤：
* 安装: npm install -g hexo-cli
* 建站：
    * hexo init <目录名> # 以后整个站点的目录就是这个了
    * cd <目录名>
    * npm install # 安装依赖的组建（高版本node可以不需要这个步骤）
* 配置：
  hexo有两类配置文件，文件名都是_config.yml；一种是hexo系统的配置文件，存放在博客<目录名>/_config.yml；一种是主题的配置文件，存放在博客<目录名>/themes/<主题名>/_config.yml
  配置的时候别搞混了，两个配置文件的关系可以理解为hexo的配置文件是全局配置，主题配置文件只针对某个主题。
  
  下面说一下hexo的配置:

  先说说基本配置：
  * title: 博客的标题
  * subtitle: 博客的子标题
  * author: 作者
  * language: 语言，默认是英文；中文有几种：zh-CN,zh-Hans,zh-TW等，具体能选什么要看主题的支持，可以通过查看主题目录下的languages目录，看支持哪些语言
  * url: 博客的网址，需要加http或者https开头  

  再说说分类和tag配置（这个我折腾了好久才弄明白）：
  * category_map: 配置分类名称和实际存放路径的对应关系，格式为<分类名称>:<路径>
    * 分类名称可以是中文，就是页面显示的名称
    * 路径是相对于/的路径，增加一个路径的页面通过命令hexo new page 'page_name'添加，和增加普通页面的命令hexo new 'page_name'不同
    * 增加好名称映射后，可以在hexo new 'page_name'新建的页面的文件头增加一个categories字段，在这个字段可以设置一个分类的名称，以后hexo会自动归档文件
  * tage_map: 原理同category_map，区别是新建的文件头可以设置多个tag


## 主题安装&配置
  hexo的主题比较多，样式各异，质量也参差不齐，我试了不下5个主题，最终选择了[Maupassant主题](https://www.haomwei.com/technology/maupassant-hexo.html)

  原因是Maupassant主题：
  * 界面简洁
  * 支持百度统计、多说、站内搜索等
  * 支持搜索功能、分类功能

  说了优点，再说说遇到问题：
  Maupassant主题需要安装node-sass这个插件，国内安装容易失败，后面将解决方法。

  安装步骤：
  * 进入博客目录，执行git clone https://github.com/tufu9441/maupassant-hexo.git themes/maupassant
  * 修改博客全局配置文件，设置theme为maupassant
  * 还没结束，坑来啦！！！ 下面两个插件需要用cnpm安装
    * hexo-renderer-jade
    * hexo-renderer-sass


  安装cnpm: npm install -g cnpm --registry=https://registry.npm.taobao.org
  > cnpm详细使用请参考[官网](https://npm.taobao.org/)

  继续安装插件（还是在博客根目录哦）
  * cnpm install hexo-renderer-jade --save
  * cnpm install hexo-renderer-sass --save

  不出意外的话两个插件安装完成（绕坑成功！）感谢[猪头强提供的方法](http://www.rockcoding.com/2016/03/02/hexo/)

### jads&sass插件未正确安装的后果
  界面没有任何样式

### 配置
  主题配置文件themes/maupassant/_config.yml修改如下（你自己的修改请参考后自行设定）
  * 搜索类：google_search设置为false（这个国内基本没用）
  * 留言类：我使用多说评论系统，所以设置duoshuo为我的id
  * 统计类：我使用百度统计，设置baidu_analytics为我的id
  * 菜单：我保留了home,archive,about，其他的删掉了
  * 小部件：就是widgets字段，根据需要裁剪吧

## 运营博客

  环境搭建好了，正式开工写博客了

### 本地工作
  除了发布以外的事情基本都能在本地完成（以下操作都在博客根目录完成）
  * 写博客：hexo new 'page_name' # page_name和标题没有关系，只是文件名
    * 新生成的博客文件存放在sources/_post/page_name.md （markdown格式哦）
    * 打开page_name.md文件，文件头几个字段需要说明一下：
      * title: 文章的标题
      * categories: （如果没有可以增加这项）分类的名称是在博客_config.yml全局配置文件的category_map设置的名称之一
      * toc: 文章目录，设置true打开文章目录
  * 生成博客: hexo generate 或者简写hexo g
  * 运行博客: hexo server或者简写hexo s

### 发布
#### github配置
  需要在自己的github建立一个<用户名>.github.io这样名字的git库
### hexo配置
  修改全局_config.yml配置文件deploy字段：
  * 设置type为git （之前版本是github，3.0以后是git）
  * 增加repository字段，内容是上面新建的git库的完整路径（可以登录到github查看，最好是复制地址过来）
  * 增加branch字段，内容是master（其他的分支名我没试过不知道）
  安装git组件：npm install hexo-deployer-git --save
  发布：hexo deploy

### 验证
  自己登录到http://<用户名>.github.io查看博客

## 搭建过程&写博客感受
  码字真累啊
  学到了不少知识，尤其是前端开发的知识。从hexo学习到了前端框架方面的一些思想，很有启发。

## ToDo
  自动化：现在的操作都是开几个term手动操作的，以后考虑自动化提高效率
  多机：几个电脑都可以写博客，部署，数据能互相同步（考虑依靠github实现，ms已经有人这么做了，知道的给我留言啊）
  图片：现在纯码字，以后考虑用七牛存储放图片，目前研究学习中。。。

## 参考文档
  [hexo官方文档](https://hexo.io/zh-cn/docs/setup.html)
  [maupassant中文参考](https://www.haomwei.com/technology/maupassant-hexo.html)
  [使用hexo时遇到的小坑](http://www.rockcoding.com/2016/03/02/hexo/)
  [使用Github搭建静态博客（Hexo）](https://segmentfault.com/a/1190000000458953)
