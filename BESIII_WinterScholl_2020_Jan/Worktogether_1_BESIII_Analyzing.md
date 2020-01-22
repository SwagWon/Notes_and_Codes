---
noteId: "1644db20391111eaa1b6717ab88a3cee"
tags: [BESIII_Worktogether_1]

---

# BESIII 分析新手入门

## BESIII 配置 BOSS（BESIII Offline Software System）的环境

课件： https://indico.ihep.ac.cn/event/11031/session/2/contribution/3/material/2/0.html

### 账号下的目录

账号下的目录有：

#### home主目录 
这个目录是登陆上服务器进入的默认目录，可以用下面的命令返回目录

```shell
#返回home目录
cd ~
#或
cd /afs/ihep.ac.cn/users/s/username
```

这个目录大小500M，有备份，无法提交作业

#### 算法存放目录

这个目录用于存放算法，目录地址是

```shell
#前往算法存放目录
cd /workfs/bes/username
```
5G，有备份，误删之后联系计算中心恢复代码

#### 数据盘

数据盘地址：
```shell
cd /besfs/user/username
```
50G,在此提交作业，做模拟，重建和分析，超出额度之后会锁盘

#### 暂存盘
暂存盘地址
```shell
cd /scratchfs/bes/songyx
```
500G，超出额度之后无法写入

### BOSS的配置方法
这里的配置以7.0.3版本为例，BOSS版本的选择由使用的data种类决定，具体参考Production：https://docbes3.ihep.ac.cn/~offlinesoftware/index.php/Production
这个地址给出了



