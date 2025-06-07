[kali系统下多版本JDK共存_jdk kali-CSDN博客](https://blog.csdn.net/wuqixiufen2/article/details/135886624#:~:text=%E4%BD%BF%E7%94%A8update-alternatives%E5%91%BD%E4%BB%A4%E8%BF%9B%E8%A1%8C%E5%AE%89%E8%A3%85%E5%92%8C%E8%AE%BE%E7%BD%AEjdk%EF%BC%8C%E5%8F%AF%E4%BD%BF%E5%A4%9A%E4%B8%AA%E7%89%88%E6%9C%AC%E5%85%B1%E5%AD%98%EF%BC%8C%E5%85%88install%E5%86%8Dset%E3%80%82%20%E5%9C%A8install%E6%97%B6%E9%9C%80%E8%A6%81%E5%A1%AB%E5%86%99%E4%BC%98%E5%85%88%E7%BA%A7%EF%BC%8C%E5%A1%AB%E5%86%99jdk%E7%89%88%E6%9C%AC%E5%8F%B7%EF%BC%8Cjdk8%E7%9A%84%E5%8E%BB%E6%8E%89%E4%B8%AD%E9%97%B40%20%2Cjdk11%E5%85%A8%E9%83%A8%E6%8B%BC%E6%8E%A5%E4%B8%8A%EF%BC%8C%E7%9B%AE%E7%9A%84%E6%98%AF%E8%AE%A9%E4%BC%98%E5%85%88%E7%BA%A7%E7%9A%84%E4%BD%8D%E6%95%B0%E4%B8%80%E6%A0%B7%E3%80%82%20%E4%BB%A5%E5%AE%89%E8%A3%85jdk-8u191%E4%B8%BA%E4%BE%8B,%E5%A6%82%E6%9E%9C%E4%B8%8D%E8%A6%81%E8%AF%A5%E7%89%88%E6%9C%AC%E5%8F%AF%E7%94%A8%E4%BB%A5%E4%B8%8B%E5%91%BD%E4%BB%A4%E8%BF%9B%E8%A1%8C%E7%A7%BB%E9%99%A4%20%E5%88%87%E6%8D%A2%E5%85%B6%E4%BB%96%E7%89%88%E6%9C%AC%E6%97%B6%E5%8F%AF%E4%BD%BF%E7%94%A8%E4%BB%A5%E4%B8%8B%E5%91%BD%E4%BB%A4%20%23%20%E9%85%8D%E7%BD%AE%E5%AF%B9%E5%BA%94java%E6%96%87%E6%A1%A3%E7%89%88%E6%9C%AC%EF%BC%8C%E5%A6%82%E6%9E%9C%E6%B2%A1%E6%9C%89%E5%AE%89%E8%A3%85%E5%88%99%E4%B8%8D%E7%94%A8%E9%80%89%E6%8B%A9%EF%BC%8C%E8%B7%9Fjava%E5%90%8C%E6%97%B6%E6%93%8D%E4%BD%9C%20)


update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_202/bin/java 18202
update-alternatives --set java /usr/lib/jvm/jdk1.8.0_202/bin/java
update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_202/bin/javac 18202
update-alternatives --set javac /usr/lib/jvm/jdk1.8.0_202/bin/javac
![[Pasted image 20250606224818.png]]
```
jdk1.8.0_202                VMware-Tools-windows-12.4.5-23787635.zip
jdk-8u202-linux-x64.tar.gz

┌──(z0reverse㉿MiWiFi-RD04v2-srv)-[~/桌面]
└─$ mv jdk1.8.0_202 /usr/lib/jvm/
mv: 无法将 'jdk1.8.0_202' 移动至 '/usr/lib/jvm/jdk1.8.0_202': 权限不够

┌──(z0reverse㉿MiWiFi-RD04v2-srv)-[~/桌面]
└─$ sudo mv jdk1.8.0_202 /usr/lib/jvm/
[sudo] z0reverse 的密码：

┌──(z0reverse㉿MiWiFi-RD04v2-srv)-[~/桌面]
└─$ cd /usr/lib/jvm

┌──(z0reverse㉿MiWiFi-RD04v2-srv)-[/usr/lib/jvm]
└─$ ls
default-java  java-1.21.0-openjdk-amd64  java-21-openjdk-amd64  jdk1.8.0_202

┌──(z0reverse㉿MiWiFi-RD04v2-srv)-[/usr/lib/jvm]
└─$ update-alternatives
update-alternatives: 需要 --display, --query, --list, --get-selections, --config, --set, --set-selections, --install, --remove, --all, --remove-all 或 --auto

使用 update-alternatives --help 查看关于程序用法的信息。

┌──(z0reverse㉿MiWiFi-RD04v2-srv)-[/usr/lib/jvm]
└─$ update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_202/bin/java 18202
update-alternatives --set java /usr/lib/jvm/jdk1.8.0_202/bin/java
update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_202/bin/javac 18202
update-alternatives --set javac /usr/lib/jvm/jdk1.8.0_202/bin/javac
update-alternatives: 使用 /usr/lib/jvm/jdk1.8.0_202/bin/java 来在自动模式中提供 /usr/bin/java (java)
update-alternatives: 错误: 新建符号链接 /etc/alternatives/java.dpkg-tmp 时出错: 权限不够
update-alternatives: 错误: java 的候选项 /usr/lib/jvm/jdk1.8.0_202/bin/java 没有注册，不予设置
update-alternatives: 使用 /usr/lib/jvm/jdk1.8.0_202/bin/javac 来在自动模式中提供 /usr/bin/javac (javac)
update-alternatives: 错误: 新建符号链接 /etc/alternatives/javac.dpkg-tmp 时出错: 权限不够
update-alternatives: 错误: 无 javac 的候选项

┌──(z0reverse㉿MiWiFi-RD04v2-srv)-[/usr/lib/jvm]
└─$ sudo su
┌──(root㉿MiWiFi-RD04v2-srv)-[/usr/lib/jvm]
└─# update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.8.0_202/bin/java 18202
update-alternatives --set java /usr/lib/jvm/jdk1.8.0_202/bin/java
update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.8.0_202/bin/javac 18202
update-alternatives --set javac /usr/lib/jvm/jdk1.8.0_202/bin/javac

update-alternatives: 使用 /usr/lib/jvm/jdk1.8.0_202/bin/java 来在自动模式中提供 /usr/bin/java (java)
update-alternatives: 使用 /usr/lib/jvm/jdk1.8.0_202/bin/javac 来在自动模式中提供 /usr/bin/javac (javac)

┌──(root㉿MiWiFi-RD04v2-srv)-[/usr/lib/jvm]
└─# update-alternatives --config java                                         有 2 个候选项可用于替换 java (提供 /usr/bin/java)。

  选择       路径                                       优先级  状态
------------------------------------------------------------
  0            /usr/lib/jvm/jdk1.8.0_202/bin/java            18202     自动模式
  1            /usr/lib/jvm/java-21-openjdk-amd64/bin/java   2111      手动模式
* 2            /usr/lib/jvm/jdk1.8.0_202/bin/java            18202     手动模式

要维持当前值[*]请按<回车键>，或者键入选择的编号：2

┌──(root㉿MiWiFi-RD04v2-srv)-[/usr/lib/jvm]
└─# java -version
java version "1.8.0_202"
Java(TM) SE Runtime Environment (build 1.8.0_202-b08)
Java HotSpot(TM) 64-Bit Server VM (build 25.202-b08, mixed mode)

┌──(root㉿MiWiFi-RD04v2-srv)-[/usr/lib/jvm]
└─# update-alternatives --config javac
有 1 个候选项可用于替换 javac (提供 /usr/bin/javac)。

  选择       路径                               优先级  状态
------------------------------------------------------------
  0            /usr/lib/jvm/jdk1.8.0_202/bin/javac   18202     自动模式
* 1            /usr/lib/jvm/jdk1.8.0_202/bin/javac   18202     手动模式

要维持当前值[*]请按<回车键>，或者键入选择的编号：1

```