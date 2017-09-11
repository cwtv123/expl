##S2-052（CVE-2017-9805）

struts2 052远程代码执行漏洞POC利用（影响版本：Struts 2.1.2 - Struts 2.3.33, Struts 2.5 - Struts 2.5.12） 官方介绍：https://cwiki.apache.org/confluence/display/WW/S2-052 此POC是在struts-2.5.12版本测试验证的。

## 测试环境搭建

```
docker-compose build
docker-compose up -d
```


##POC
http://10.160.11.191:8080/orders.xhtml

如果上述都顺利的话可以看到Orders可编辑界面，下面是POC测试过程。 点击编辑，进入到修改界面，点击"提交"抓包，然后修改Content-Type为application/xml格式，post数据替换为poc中data提交即可弹计算器了。
Notes:
Windows下关键字为：

<command><string>calc</string></command>
Mac下关键字为：

<command><string>/Applications/Calculator.app/Contents/MacOS/Calculator</string></command>
