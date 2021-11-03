---
title: hexo搭建博客
date: 2021-10-29 14:14:50
tags:
---

##### 1. hexo介绍
（1）hexo时什么？
Hexo 是一个快速、简洁且高效的博客框架

（2）安装
```
npm install -g hexo-cli
```

（3）初始化一个网站项目
```
hexo init <folder>
cd <folder>
npm install
```
（3）项目文件目录
├── _config.yml
├── package.json
├── scaffolds
├── source
|   ├── _drafts
|   └── _posts
└── themes

（4）文件介绍
_config.yml 网站的配置信息
scaffolds   模版文件夹，当您新建文章时，Hexo 会根据 scaffold 来建立文件
source  资源文件夹是存放用户资源的地方
themes  主题 文件夹，Hexo 会根据主题来生成静态页面

##### 2. 搭建博客

##### 3. 关于Github Actions
（1）github actions是什么？
一种持续集成服务，持续集成由很多操作组成，比如登陆远程服务器，发布内容到第三方服务等，Github把这些操作称为actions

（2）基本概念
- workflow（工作流程）：持续集成一次运行的的过程，就是一个workflow
- job（任务）：一个 workflow 由一个或多个 jobs 构成，含义是一次持续集成的运行，可以完成多个任务
- step（步骤）：每个 job 由多个 step 构成，一步步完成
- action（动作）：每个 step 可以依次执行一个或多个命令（action）、

（3）workflow文件
GitHub Actions 的配置文件叫做 workflow 文件，存放在代码仓库的.github/workflows目录
配置字段
- name
name字段是 workflow 的名称

- on    
on字段指定触发 workflow 的条件，通常是某些事件

- on.<push|pull_request>.<tags|branches>
指定触发事件时，可以限定分支或标签
```
on:
  push:
    branches:    
      - master
```

- jobs.<job_id>.name
workflow 文件的主体是jobs字段，表示要执行的一项或多项任务
```
jobs:
  my_first_job:
    name: My first job
  my_second_job:
    name: My second job
```

- jobs.<job_id>.needs
needs字段指定当前任务的依赖关系，即运行顺序
```
jobs:
  job1:
  job2:
    needs: job1
  job3:
    needs: [job1, job2]
```

- jobs.<job_id>.runs-on
runs-on字段指定运行所需要的虚拟机环境。它是必填字段。目前可用的虚拟机如下
```
ubuntu-latest，ubuntu-18.04或ubuntu-16.04
windows-latest，windows-2019或windows-2016
macOS-latest或macOS-10.14
```

- jobs.<job_id>.steps
steps字段指定每个 Job 的运行步骤，可以包含一个或多个步骤。每个步骤都可以指定以下三个字段
```
jobs.<job_id>.steps.name：步骤名称。
jobs.<job_id>.steps.run：该步骤运行的命令或者 action。
jobs.<job_id>.steps.env：该步骤所需的环境变量。
```

##### 4. 部署到ECS