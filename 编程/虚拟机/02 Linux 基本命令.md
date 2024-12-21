---
aliases:
  - Linux
  - 命令
date: 2024-11-12
---

# 服务

查看服务端口号

[Ubuntu 查看服务及其对应的端口号_乌班图 查看端口 所在服务-CSDN博客](https://blog.csdn.net/noricky/article/details/80032180)

```
sudo netstat -ap | grep zabbix_agent
```

查看服务是否启动

```
systemctl status zabbix-agent
```

# 查看端口号

```
netstat -tuln
```

# 统计指定文件夹的总大写

```
du -sh temp/
```

> [!note] 参考资料
> [Linux下du命令详解 -- 查看文件和目录大小、文件夹大小 - jack_Meng - 博客园](https://www.cnblogs.com/mq0036/p/14784188.html)