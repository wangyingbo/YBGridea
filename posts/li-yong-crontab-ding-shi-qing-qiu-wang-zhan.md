---
title: '利用crontab定时请求网站'
date: 2021-11-22 15:36:08
tags: [GitHub]
published: true
hideInList: false
feature: /post-images/li-yong-crontab-ding-shi-qing-qiu-wang-zhan.png
isTop: false
---
# ybproxy-auto-request

[GitHub 地址：https://github.com/wangyingbo/ybproxy-auto-request](https://github.com/wangyingbo/ybproxy-auto-request)

## 脚本作用

- 利用github actions 自动访问请求herokuapp和netlify免费服务器的网址；实现herokuapp和netlify免费账号能一直保活。
- 会把更新时间插入到recordtime.txt文件里，根据最新时间倒序排列；

## 使用

如果你有一台Linux主机，或者你有一台不经常关机的Mac，那么你可以利用系统自带的`crontab`定时任务命令来执行定时任务。

在终端输入`crontab -e` 命令，可以进入crontab定时任务编辑页，我们可以在这个文本里利用vim添加一条定时任务`crontab.sh`，添加完毕用`wq`保存退出；

![](https://hiwyb.github.io/post-images/1637566962477.png)

添加成功以后，可利用`crontab -l`命令查看添加的任务；

![](https://hiwyb.github.io/post-images/1637566978330.png)

添加成功以后，需要重启cron进程：

```
service crond restart
```

可查看crontab的执行日志：

```
cat /var/log/cron

```

## crontab.sh脚本如下：

```
#!/bin/bash
# author wangyingbo

cd /root/Desktop/Projects/ybproxy-auto-request
git pull --rebase
DATE=`date +%Y%m%d%H%M%S`
echo "current git push time: $DATE"
# 插入到最后一行
# echo $DATE >> ./recordtime.txt
# 插入到第一行
sed -i "1i$DATE" ./recordtime.txt
git add recordtime.txt
git commit --allow-empty -m " update auto request ybproxy"
git push 
sleep 1
echo -e "\033[33;40m  ($0) ${TIME}: this shell script execution duration: ${SECONDS}s  \033[0m"
echo "😊😊😊😊😊😊success excute shell😊😊😊😊😊😊"

```