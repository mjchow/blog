

## ss搭建

安装shadowsocks

```shell
apt-get install python-pip #yum install python-pip #centos和ubuntu下不同的安装方式
pip install shadowsocks
```

增加配置文件[配置文件需要自己新建文件]

```bash
vi  /etc/shadowsocks.json
```

配置文件内容

```json
{
    "server":"0.0.0.0",
    "server_port":10000,
    "local_address": "127.0.0.1",
    "local_port":1080,
    "password":"password",
    "timeout":300,
    "method":"aes-256-cfb"
}
```

启动ss服务，并且使用刚才的配置启动

```shell
ssserver -c /etc/shadowsocks.json -d start  #start restart stop
```

客户端可能连不上的问题：

**1.服务器开启了防火墙 [遇到过一次 centos的防火墙开启了，直接把iptables中的规则都删除就可以正常访问]**

**2.查看ip 端口那些是否输入对了**

**3.有时候需要断开重新连接**

----

加速器serverSpeeder安装

单独用ss的话，速度会比较慢，YouTube视频1080P的几乎看不了，所以需要使用加速器

锐速加速器一键破解 https://github.com/91yun/serverspeeder