# JNDIMonitor2.0.1

# 简介

随着Apache Log4j被打的越来越多，常见的dnslog平台估计会被屏蔽的越来越狠，而且对于一些流量监测设备，直接使用公开的dnslog平台无疑是自寻死路。

突然想到常用的Java jndi注入工具就有这功能，然后就删去了多余的代码，当一个`LDAP`请求监听器，摆脱`dnslog`平台。

# 使用

```shell
Usage: java -jar JNDIMonitor-1.0-SNAPSHOT.jar [options]
  Options:
  * -i, --ip       Local ip address  (default: 0.0.0.0)
    -l, --ldapPort Ldap bind port (default: 1389)
    -p, --ApiPort  Http api port (default: 3456)
    -h, --help     Show this help
```

# 2.0.1 更新

`2.0.1`版本新增`http API`接口，接口固定如下，支持返回全部日志记录。

日志记录新增`来源ip`和`触发时间`，`来源ip`获取的是监听主机的`bug`目前已知，正在解决。

添加防止重复内容写入功能。

```shell
http://ip:port/?api2=all
aaaaaa,127.0.0.1,2021-12-14 21:46:56 PM
bbbbbb,127.0.0.1,2021-12-14 21:47:01 PM
cccccc,127.0.0.1,2021-12-14 21:47:08 PM
```

# 2.0 更新

## 监听`LDAP`请求，以及开启 `http API` 服务

程序启动后会自行在当前目录创建`tmp.txt`文件，用来存放`LDAP`的请求记录。

![](./img/jndi1.png)

## curl请求API接口测试

`2.0`版本新增`http API`的接口，接口固定格式如下。

```shell
http://ip:port/?api=xxxxxx(长度无限制)
```

![](./img/jndi2.png)


## 参考

https://github.com/0x727/JNDIExploit/

![](https://starchart.cc/r00tSe7en/JNDIMonitor.svg)
