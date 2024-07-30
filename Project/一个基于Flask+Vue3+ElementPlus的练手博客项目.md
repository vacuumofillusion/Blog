# 一个基于Flask+Vue3+ElementPlus的简单练手博客项目

> 虽然是一个简单的练手项目，但也把前后端基本流程都跑通了，足以领悟到目前的简单Python Web项目开发流程。

## 第一步：项目规划

第一步先规划项目的基本功能，前台和后台，分别有哪些功能，不需要很详细，直接列出来即可。

这一步有助于整理思路，让自己能把项目的功能点想好，避免后面开发过程中再临时起意，或遗漏某个功能。

## 第二步：数据库设计

针对项目功能，设计数据库要用到的表，以及表之间的关系。

数据库一旦设计好了，其实ORM的部分就基本剩下用代码来实现了。

## 第三步：熟悉框架

本次项目已经预先定了后端使用Python的Flask框架，前端使用基于Vue3的ElementPlus框架。

所以，我需要先熟悉这两个框架，了解它们的基本使用方法。

## Flask

这里非常感谢大佬（Dormouse Young）翻译的Flask中文文档，非常详细。

https://dormousehole.readthedocs.io/en/latest/index.html

先学习这个文档了解的Flask的基本使用方法，各种功能，各种组件。

Flask是一个轻量级的框架，包含WSGI、Jinja2、Route、Session、Log、Blueprint、Config等功能

Flask本身不包含ORM，所以我这里使用Flask-SQLAlchemy来操作数据库。

https://flask-sqlalchemy.palletsprojects.com/en/3.1.x/

https://docs.sqlalchemy.org/en/20/

## ElementPlus

Vue3是目前最火的JavaScript框架，所以肯定要用一用。

https://cn.vuejs.org/

ElementPlus是一个基于Vue3的UI组件库，并且也是一个老牌的组件，所以选择使用这个。

https://element-plus.org/zh-CN/component/overview.html

不过在使用过程中，由于要使用Flask内置的Jinja2模板并不是完全前后端分离的设计，所以在前端开发中我并没有做完全的前后端分离，并没有使用NPM或Vite或Webpack这样的前端打包工具。

而是使用的CDN引入，把ElementPlus和Vue3都引入了Jinja2的模板中，由于不能使用.vue的文件进行开发，导致开发效率下降，在前端上面折腾了不少时间。

不得不说，现在前端框架还是完全跟后端分离的好。

ElemetPlus的组件使用非常方便，而且模板命名也很清晰，这在很多前端的功能上省了很多开发时间。

## 第四步：搭建自己项目架构

我把整个博客项目放入一个包中，然后该包有一个`__init__.py`文件，这个文件负责构造一个Flask实例并返回，在包的外部，也就是项目的根目录下，有一个`app.py`文件，是项目的入口（启动），会import我的博客项目包，实例化一个Flask实例。

项目配置在`configs.py`中，包括数据库配置、日志配置等，使用`.gitignore`文件忽略掉（但会保留一个`configs_example.py`，删除example并填写对应配置即可）。

项目采用Blueprint来进行模块化，每个模块一个Blueprint，然后对应各自的路由，在`__init__.py`中注册这些蓝图。

建立`model.py`文件，引入sqlalchemy，然后建立数据库模型，然后在`__init__.py`中初始化数据库。

在templates中建立前后台的`base_layout.html`文件，导入前后端的公共文件，定义好html、js、css的`{% block %}`。

## 第五步：实现具体业务逻辑

后台的管理员登录，以及简单的login_required装饰器，用于判断管理员是否登录。

分类中的子分类及父分类的关联问题。

文章的增删改查，使用了富文本编辑器WangEditor用于编辑文本内容，使用了el-upload组件上传图片，在模型层构建文章和分类的一对多关系。

前台和后台的分页功能，前台的分类文章列表，使用Markdown-CSS展示文章详情页。

在实现这些具体业务逻辑时，也遇到过一些问题，不过都借助AI和百度解决了。

## 第六步：总结

本次练手项目，在后端技能方面，掌握了Flask框架的基本使用，也了解了Flask-SQLAlchemy的简单使用方法，实现了完整的数据表的CRUD功能。

在前端技能方面，掌握了Vue3的基本使用方法，也了解了ElementPlus的简单使用方法。

Flask在开发这种项目，感觉结构清晰，代码简洁，开发效率是比较高的。
