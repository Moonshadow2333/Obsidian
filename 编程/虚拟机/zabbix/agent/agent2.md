```
cd C:\Program Files\Zabbix Agent 2
zabbix_agent2.exe --stop
ERROR: Failed to handle Windows service: failed to stop Zabbix Agent 2 service: failed to connect to service manager: Access is denied.


cmd 使用管理员权限运行，执行上述的即可
```

```
zabbix_get -s 192.168.56.101 -p 10050 -k "system.hostname"
zabbix_get -s 192.168.10.14 -p 10050 -k "system.hostname"
zabbix_get -s 192.168.10.14 -p 10050 -k 'agent.ping'
zabbix_get -s 192.168.56.101 -p 10050 -k 'agent.ping'
```


```
zabbix_agent2.exe --stop
ERROR: Failed to handle Windows service: failed to stop Zabbix Agent 2 service: failed to send stop request to service: The service has not been started.

提示的很明显，即 zabbix agent2 的服务未开启
但是我执行了 `zabbix_agent2.exe --start` 脚本，服务并未成功开启，后面搜了一下，应该时端口冲突导致的问题，之前已经安装过 zabbix_agent，已经使用过 10050，两个用用同一个端口，所以启动失败，关闭失败
```

[2 安装 - 10 Microsoft Windows下的Zabbix agent 2 - 《Zabbix 5.0 使用手册》 - 书栈网 · BookStack](https://www.bookstack.cn/read/zabbix-5.0-zh/5fa31139e601364d.md)