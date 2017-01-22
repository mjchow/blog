

## iptables初体验

1.查看iptables中已存在的规则

```shell
iptables -nL --line-number
```

2.删除规则

```shell
iptables -D INPUT 1
#删除上面那个命令显示出来的行号的规则
```

2.一个简单INPUT链的操作

```shell
iptables -A INPUT -s 127.0.0.1 -p tcp --dport 8080 -j ACCEPT #允许本机可以访问8080d端口
iptables -A INPUT -p tcp --dport 8080 -j DROP #禁止所有的ip访问8080端口 包括本机
#默认是对filter表操作[如果前面不加 -t filter 的话]
#貌似filter表中只要符合一条就不会进行下去了? 所以这里ACCEPT要放在前面才行，不然本机都无法访问8080端口
```

