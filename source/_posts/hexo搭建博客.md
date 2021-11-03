---
title: hexo搭建博客
date: 2021-10-29 14:14:50
tags:
---

##### 1. hexo介绍

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

- jobs.<job_id>.needs

- jobs.<job_id>.runs-on

- jobs.<job_id>.steps

##### 4. 部署到ECS