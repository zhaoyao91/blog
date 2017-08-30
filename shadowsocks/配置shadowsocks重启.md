# 配置shadowsocks重启

前置条件：已正确安装Shadowsock服务，可参考[这篇文章](./搭建shadowsocks.md)。

首先，在服务器上创建shadowsocks配置文件，如/etc/shadowsocks.json。

然后，创建一键重启文件/root/restart-ss.sh，内容如下：

```
date
ssserver -c /etc/shadowsocks.json -d restart
```

然后，配置定时重启任务，输入crontab -e，然后在末尾添加一行：

```
0 0 * * * bash /root/restart-ss.sh >> /root/cron.log
```

运行`service cron restart`以确保定时任务已启动。

更进一步，可以修改`/etc/rc.local`来配置重启重启。在`exit 0`之前加一行`bash /root/restart-ss.sh`即可。