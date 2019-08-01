# sonarqube代码质量检测
## SonarQube 介绍
~~~
SonarQube 是一个用于管理源代码质量开放平台，它可以从多个维度检测代码质量，可以快速的定位代码中潜在的或者明显的 Bug、错误。它支持包括 Java、Python、Php、C/C++、C#、HTML、JavaScript、PL/SQL、Objective C 等二十多种编程语言的代码质量管理与检测。可作为我们日常开发中检测代码质量的重要工具。
~~~
## 环境、软件准备
- **本次演示环境，centos，以下是安装的软件及版本**
~~~
SonarQube：version 6.7
Jdk：version 1.8.0_161
Maven：version 3.6.1
Mysql： version 5.7
~~~
## 安装过程
- **下载链接 本文选择sonarqube-6.7**
~~~
https://binaries.sonarsource.com/Distribution/sonarqube/
~~~
- **下载.zip文件 解压**
~~~
bin 用来启动 SonarQube 服务，这里已经提供好了不同系统启动 | 停止脚本了，目前提供了  linux-x86-32、linux-x86-64、macosx-universal-64、windows-x86-32、windows-x86-64
conf 用来存放配置文件，若需要修改配置，修改 sonar.properties 文件即可。
data 用来存放数据，SonarQube默认使用 h2 数据库存储，同时支持其他如Mysql、Orace、Mssql、Postgresql数据库存储。
extensions 用来存放插件 jar 包，以后我们需要安装插件就放在这里。
lib 用来存放各种所依赖的 jar 包，包括上边各数据库驱动包 (默认已提供一个版本，如果版本不匹配，则在这里手动更新下)。
logs 用来存放各日志信息
web 用来提供 SonarQube web 网页服务。
~~~
- **启动**
~~~
环境启动 | 停止 | 重启 | 查看状态 SonarQube 服务命令：<install_dir>/bin/macosx-universal-64/sonar.sh start | stop | restart | status。成功启动后，访问本地 http://localhost:9000，SonarQube 初始管理员账号为 admin，默认密码为 admin，登录后可修改密码。
~~~
- **修改默认数据库**
~~~
1、修改 sonar.properties
sonar.jdbc.username=sonar
sonar.jdbc.password=sonar
sonar.jdbc.url=jdbc:mysql://localhost:3306/sonar?useUnicode=true&characterEncoding=utf8&rewriteBatchedStatements=true&useConfigs=maxPerformance&useSSL=false

2、本地 Mysql 创建数据库
CREATE DATABASE sonar CHARACTER SET utf8 COLLATE utf8_general_ci;

3、本地 Mysql 创建用户并分配权限
CREATE USER 'sonar' IDENTIFIED BY 'sonar';
GRANT ALL PRIVILEGES ON *.* TO 'sonar'@'%' IDENTIFIED BY 'sonar' WITH GRANT OPTION;
GRANT ALL PRIVILEGES ON *.* TO 'sonar'@'localhost' IDENTIFIED BY 'sonar' WITH GRANT OPTION;
FLUSH PRIVILEGES;
修改完成重启
~~~
# 安装失败
<p>sonar插件地址：https://docs.sonarqube.org/display/PLUG/Plugin+Library</p>
<p>坑一&nbsp;</p>
<p>6.7版本sonar要求jdk比较高，必须1.8以上，多以修改sonar启动项配置，修改文件/sonarqube-6.7/conf/wrapper.conf</p>
<div class="cnblogs_code">
<pre>#wrapper.java.command=/data/install/jdk1.8.0_161/bin/java
#wrapper.java.command=java
wrapper.java.command=/data/install/jdk1.8.0_161/bin/java  //加入1.8jdk作为启动jdk</pre>
</div>
<p>&nbsp;</p>
<p>坑二</p>
<p>由于6.7版本加入了elasticsearch，遇到不能以root用户启动，报错信息如下：</p>
<div class="cnblogs_code">
<div class="cnblogs_code_toolbar"></div>
<pre>java.lang.RuntimeException: can not run elasticsearch as root
    at org.elasticsearch.bootstrap.Bootstrap.initializeNatives(Bootstrap.java:106) ~[elasticsearch-5.6.2.jar:5.6.2]
    at org.elasticsearch.bootstrap.Bootstrap.setup(Bootstrap.java:195) ~[elasticsearch-5.6.2.jar:5.6.2]
    at org.elasticsearch.bootstrap.Bootstrap.init(Bootstrap.java:342) [elasticsearch-5.6.2.jar:5.6.2]
    at org.elasticsearch.bootstrap.Elasticsearch.init(Elasticsearch.java:132) [elasticsearch-5.6.2.jar:5.6.2]
    at org.elasticsearch.bootstrap.Elasticsearch.execute(Elasticsearch.java:123) [elasticsearch-5.6.2.jar:5.6.2]
    at org.elasticsearch.cli.EnvironmentAwareCommand.execute(EnvironmentAwareCommand.java:67) [elasticsearch-5.6.2.jar:5.6.2]
    at org.elasticsearch.cli.Command.mainWithoutErrorHandling(Command.java:134) [elasticsearch-5.6.2.jar:5.6.2]
    at org.elasticsearch.cli.Command.main(Command.java:90) [elasticsearch-5.6.2.jar:5.6.2]
    at org.elasticsearch.bootstrap.Elasticsearch.main(Elasticsearch.java:91) [elasticsearch-5.6.2.jar:5.6.2]
    at org.elasticsearch.bootstrap.Elasticsearch.main(Elasticsearch.java:84) [elasticsearch-5.6.2.jar:5.6.2]</pre>
<div class="cnblogs_code_toolbar"></div>
</div>
<p>解决方案：</p>
<p>因为安全问题elasticsearch 不让用root用户直接运行，所以要创建新用户，用新用户启动</p>
<div class="cnblogs_code">
<pre>groupadd sonar
useradd sonar -g sonar -p elasticsearch</pre>
</div>
<p>坑三</p>
<p>由于sonar需要用新用户启动，所以sonar需要用到的所有资源必须属于新用户（包括jdk，坑3会讲到），不然会有权限问题</p>
<div class="cnblogs_code">
<pre>chown -R sonar /sonarqube-6.7 //把sonar资源分配给用户sonar
chgrp -R sonar /sonarqube-6.7 //把sonar资源分配给组sonar
chown -R sonar /jdk1.8 //把jdk资源分配给用户sonar
chgrp -R sonar /jdk1.8 //把jdk资源分配给组sonar</pre>
</div>
<p>坑四</p>
<p>如果忘记以新用户启动，而是以root启动，elasticsearch会在/sonarqube-6.7.5/temp里会加载一些配置文件，如果这些文件初次加载则是属于root用户的，启动也会失败，报权限问题</p>
<p>所以记住一定要以新用户启动sonar</p>
<p>坑五</p>
<p>6.7.5不兼容低版本插件，例如sonar-web插件版本低于2.5则sonar启动不了。（插件位置/sonarqube-6.7.5/extensions/plugins）,必须要找到合适的插件版本</p>
<p>坑六</p>
<p>因为高版本sonar使用jdk1.8，如果在做sonar扫描的时候运行jdk不是1.8也会报jdk版本问题</p>
<div class="cnblogs_code">
<pre>Caused by: java.lang.UnsupportedClassVersionError: org/sonar/api/utils/SonarException : Unsupported major.minor version 52.0</pre>
</div>
<p>所以不过用ant或者maven运行代码扫描的时候 必须要用jdk1.8</p></div><div id="MySignature"></div>
<div class="clear"></div>
<div id="blog_post_info_block">
<div id="BlogPostCategory"></div>
<div id="EntryTag"></div>
<div id="blog_post_info">
</div>
<div class="clear"></div>
<div id="post_next_prev"></div>
</div>