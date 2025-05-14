# 安装tomcat9
```
wget https://archive.apache.org/dist/tomcat/tomcat-9/v9.0.91/bin/apache-tomcat-9.0.91.tar.gz --no-check-certificate  

tar -zxvf apache-tomcat-9.0.91.tar.gz 

sudo mv apache-tomcat-9.0.91 /usr/local/tomcat/
```


# tomcat可以被idea远程连接调试的配置
```
1. 修改 `catalina.sh` 文件
	在Linux系统中，Tomcat的启动脚本位于 `/usr/local/tomcat/bin/catalina.sh
	
	sudo vi /usr/local/tomcat/bin/catalina.sh
	找到以下行（通常在文件顶部）：
	# OS specific support.  $var _must_ be set to either true or false.
	
	在这行之前添加以下内容：
	CATALINA_OPTS="-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=*:8000"
	- `-agentlib:jdwp`: 启用Java Debug Wire Protocol。
	- `transport=dt_socket`: 使用套接字传输。
	- `server=y`: 表示此JVM是调试服务器。
	- `suspend=n`: JVM启动时不等待调试器连接。
	- `address=*:8000`: 监听所有网络接口上的8000端口。

2. 配置防火墙规则
确保您的ECS实例的安全组规则允许外部访问8000端口。

3. 重启Tomcat服务

完成上述配置后，重启Tomcat服务以使更改生效。
sudo /usr/local/tomcat/bin/shutdown.sh 2sudo /usr/local/tomcat/bin/startup.sh

4. 配置IntelliJ IDEA进行远程调试 IntelliJ IDEA。
	菜单栏中的 **Run** -> **Edit Configurations...**。
	左上角的 **+** 按钮，选择 **Remote JVM Debug**。
	以下参数：
    - **Name**: 输入一个名称，例如 "Tomcat Remote Debug"。
    - **Host**: 输入您的ECS实例公网IP地址。
    - **Port**: 输入8000（与上面配置的端口一致）。
    - **Command line arguments for remote JVM**: 默认生成的内容应该与您在 `catalina.sh` 中添加的参数一致。

5. 开始调试
	1. 在IntelliJ IDEA中设置断点。
	2. 点击 **Debug** 按钮开始远程调试。
```









