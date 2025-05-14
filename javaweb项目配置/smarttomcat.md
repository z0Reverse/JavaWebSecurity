1. Tomcat server - **内容**：选择已安装并配置好的Tomcat版本，图中是 `Apache Tomcat/11.0.6` 。若未配置，点击右侧 `Configure...` 按钮，在弹出窗口指定Tomcat安装目录完成配置。
 2. Catalina base - **内容**：通常是Tomcat安装目录，也可指定自定义工作目录。图中路径类似用户自定义路径，指向当前项目相关目录（`users\x0Reverse\.SmartTomcat\ofcms-V1.1.3\ofcms-admin` ），一般保持默认或根据项目需求调整
 3. Deployment directory - **内容**：项目部署目录，图中 `ofcms-V1.1.3/ofcms-V1.1.3/ofcms-admin/src/main/webapp` 是Maven项目标准Web应用资源存放目录，用于放置Web相关资源（如HTML、CSS、JavaScript文件等），保持默认指向项目正确的Web资源路径即可。
 4. Use classpath of module - **内容**：选择项目中对应的模块，图中 `ofcms-admin` 是当前要部署和运行的模块，选择正确的项目模块保证能加载对应代码和资源。
 5. Context path - **内容**：Web应用的上下文路径，图中是 `/ofcms-admin` ，即访问项目时URL中跟在域名和端口后的部分，如 `http://localhost:8080/ofcms-admin` ，可按需修改，注意不能与其他应用冲突
 6. Server port - **内容**：Tomcat服务器监听的端口，图中是 `8080` ，是Tomcat默认端口，若该端口被占用，可修改为其他未被占用端口（如 `8081` 等）
 7. SSL port - **内容**：若项目需要通过HTTPS访问，配置SSL加密通信的端口，一般不启用HTTPS时可留空
 8. Admin port - **内容**：Tomcat管理界面监听端口，图中是 `8005` ，用于管理Tomcat服务器，如关闭Tomcat等操作，可按需修改，但要避免端口冲突。
 9. VM options - **内容**：用于设置Java虚拟机参数，如调整堆内存大小（`-Xmx512m -Xms256m` 等设置最大堆内存和初始堆内存）、启用垃圾回收器参数等，根据项目性能需求配置，若无特殊要求可先留空
 10. Environment variables - **内容**：设置运行时环境变量，可添加项目运行依赖的自定义环境变量，如数据库连接配置相关变量等，没有相关需求可留空
 11. Extra JVM classpath - **内容**：添加额外的类路径，若项目运行需要加载非项目依赖路径下的类库，可在此指定路径，多个路径用 `;` （Windows）或 `:` （Linux、Mac）分隔，无需求可留空。
 12. Before launch - **内容**：可配置在启动前执行的任务，如编译项目（`Build` ）等，图中已有 `Build` ，一般保留此默认配置保证项目启动前代码是最新编译状态，也可根据需要添加其他任务。