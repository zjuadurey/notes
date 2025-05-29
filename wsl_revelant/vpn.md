# configure wsl2 to access the proxy of the windows host

<https://zhuanlan.zhihu.com/p/153124468>
- 方法一

打开clash中的局域网连接，设置端口（例如7890）

```bash
#!/bin/bash
host_ip=$(cat /etc/resolv.conf |grep "nameserver" |cut -f 2 -d " ")
export ALL_PROXY="http://$host_ip:7890"
#7890 改为clash中自定义的端口号
```

- 方法二

直接使用clash的tun模式
