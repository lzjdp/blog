---
title: 三分钟了解Github Actions
date: 2021-12-1 14:48:44
tags:
---

##### 1. 何为Github Actions?
简单解释就是在Github中可以直接引用别人写好的集成脚本，使自己的项目快速实现持续集成

##### 2. 配置字段
- workflow （工作流程）：持续集成一次运行的过程，就是一个 workflow
- job （任务）：一个 workflow 由一个或多个 jobs 构成，含义是一次持续集成的运行，可以完成多个任务
- step（步骤）：每个 job 由多个 step 构成，一步步完成
- action （动作）：每个 step 可以依次执行一个或多个命令（action）

##### 3. 最佳实践
需求：每次触发更新机制后将代码自动打包并上传部署到服务器

```
name: deploy for dev
on:
    push: 
        branchs:
            - master
        paths:
            - '.github/workflows'
            - 'src/**'
jobs:
    test:
        runs-on: ubuntu-lastest
        steps:
            - users: actions/checkout
            - name: set ssh key
                run: |
                    mkdir -p ~/.ssh/
                    echo "${{secrets.MAC_LOCAL}}" > ~/.ssh/id_rsa
                    chmod 600 ~/.ssh/id_rsa
                    ssh-keyscan "39.100.253.134" >> ~/.ssh/known_hosts
            - name: deploy
                ssh carr@39.100.253.134
                cd /home/carr
                git remote add origin https://github.com:${{secrets.MAC_LOCAL}}@github.com/lzjdp/automation
                git pull origin master
                git remote remove origin
```