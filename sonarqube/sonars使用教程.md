<div id="topics">
	<div class = "post">
		<h1 class = "postTitle">
			<a id="cb_post_title_url" class="postTitle2" href="https://www.cnblogs.com/xingyunblog/p/9947854.html">SonarQube学习入门指南</a>
		</h1>
		<div class="clear"></div>
		<div class="postBody">
			<div id="cnblogs_post_body" class="blogpost-body"><h1>&nbsp;1. 什么是SonarQube?</h1>
<p>SonarQube 官网：<a href="https://www.sonarqube.org/" target="_blank">https://www.sonarqube.org/</a></p>
<blockquote>
<p><span><span>SonarQube&reg;</span></span><span><span>是一种自动代码审查工具，用于检测代码中的错误，漏洞和代码异味。</span></span>它可以与您现有的工作流程集成，以便在项目分支和拉取请求之间进行连续的代码检查。</p>
</blockquote>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181112165019689-150004404.png" alt="" /></p>
<h1>2. 使用前提条件</h1>
<p><strong>当前版本 SonarQube 7.4</strong></p>
<p>运行SonarQube的唯一先决条件是在您的计算机上安装Java（Oracle JRE 8或OpenJDK 8）。</p>
<blockquote>
<p><strong><span><span>注意：</span></span></strong>&nbsp;<em><span><span>在Mac OS X上，强烈建议安装Oracle JDK 8而不是相应的Oracle JRE，因为JRE安装未正确完全设置Java环境。</span></span></em></p>
</blockquote>
<h2>2.1 硬件要求</h2>
<blockquote><ol>
<li><span><span>SonarQube服务器的小型（个人或小团队）实例需要至少2GB的RAM才能有效运行，并且1GB的可用RAM用于操作系统。</span><span>如果要为大型团队或Enterprise安装实例，请考虑以下其他建议。</span></span></li>
<li><span><span>您需要的磁盘空间量取决于您使用SonarQube分析的代码量。</span><span>例如，</span></span><span><span>SonarClube</span></span><span><span>的公共实例SonarCloud拥有超过3.5亿行代码，有5年的历史。</span><span>SonarCloud目前在集群</span></span><span><span>Amazon EC2 m5.large</span></span><span><span>实例</span><span>上运行，</span><span>每个节点分配50 Gb的驱动器空间。</span><span>它处理19,000多个项目，大约有1400万个未解决的问题。</span><span>SonarCloud在PostgreSQL 9.5上运行，它为数据库使用了大约250Gb的磁盘空间。</span></span></li>
<li><span><span>SonarQube必须安装在具有出色读写性能的硬盘上。</span><span>最重要的是，&ldquo;data&rdquo;文件夹包含Elasticsearch索引，当服务器启动并运行时，将在其上完成大量I / O.&nbsp;</span><span>因此，良好的读写硬盘性能将对整个SonarQube服务器性能产生很大影响。</span></span></li>
</ol></blockquote>
<h2><span>2.2 企业硬件建议</span></h2>
<p><span><span>对于SonarQube的大型团队或企业级安装，需要额外的硬件。</span><span>在企业级别，监控SonarQube实例/实例管理/ java-process-memory是必不可少的，并且应该随着实例的增长引导进一步的硬件升级。</span><span>起始配置应至少包括：</span></span></p>
<ul>
<li><span>8个核心，允许主SonarQube平台与多个计算引擎工作者一起运行</span></li>
<li><span>16GB RAM有关数据库和ElasticSearch的其他要求和建议，请参阅硬件建议/要求/硬件建议。</span></li>
</ul>
<h2>2.3 支持的平台</h2>
<p><span><span>SonarQube Java分析器能够分析任何类型的Java源文件，无论它们遵循的Java版本如何。</span></span></p>
<p><span><span>但SonarQube分析和SonarQube服务器需要特定版本的JVM。</span></span></p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181114152858070-780612391.png" alt="" /></p>
<p>&nbsp;</p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181114101849722-1793733006.png" alt="" /></p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181114101935972-1602788349.png" alt="" /></p>
<h3><span>网页浏览器</span></h3>
<p><span>要获得SonarQube提供的完整体验，您必须在浏览器中启用JavaScript。</span></p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181114153022534-1486874054.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;参考资料：<a href="https://docs.sonarqube.org/latest/requirements/requirements/" target="_blank">https://docs.sonarqube.org/latest/requirements/requirements/</a></p>
<h1>3. SonarQube 如何下载安装配置？</h1>
<p>参考资料：<a href="https://docs.sonarqube.org/latest/setup/get-started-2-minutes/" target="_blank">https://docs.sonarqube.org/latest/setup/get-started-2-minutes/</a></p>
<p>收费价格标准如下：</p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181112161129269-2040407403.png" alt="" width="653" height="307" /></p>
<p>SonarQube 的社区版是免费的，其他版本是收费的</p>
<h2>3.1 <a href="https://www.sonarqube.org/downloads/" target="_blank">下载社区版</a>&nbsp;</h2>
<p><strong>3.1.1 比如我们解压缩到这个目录&nbsp;C:\Apps\sonar\sonarqube-7.4\bin\windows-x86-64\</strong></p>
<p><strong>3.1.2 以管理员身份按照上图顺序依次运行这三个文件</strong></p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181114102516778-1691031148.png" alt="" /></p>
<p>&nbsp;</p>
<p><strong>3.1.3&nbsp;<strong>登录&nbsp;<a href="http://localhost:9000/" target="_blank">http://localhost:9000/</a>&nbsp; 可以看到这个</strong></strong></p>
<p><strong><strong><strong><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115085943548-2062429505.png" alt="" /></strong></strong></strong></p>
<p><strong>3.1.4 使用系统默认的管理员凭据（admin / admin）登陆成功。</strong></p>
<p>更详细内容移步：<a href="https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+Maven" target="_blank">https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+Maven</a></p>
<h1>4.&nbsp;&nbsp;使用SonarQube扫描仪分析Maven</h1>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181114112207852-1824571751.png" alt="" /></p>
<blockquote>
<p>Tips:</p>
<p>Sonar 版本7.4</p>
<p>Maven 版本不可小于 3.x&nbsp;</p>
<p>能访问之前那个登陆页面并登陆成功,说明SonarQube已经安装好了。</p>
</blockquote>
<h1 id="AnalyzingwithSonarQubeScannerforMaven-InitialSetup"><span>初始设置</span></h1>
<h2 id="AnalyzingwithSonarQubeScannerforMaven-GlobalSettings"><span>全局设置</span></h2>
<p><span><span><span>1. 打开</span><span>位于</span><em><span>$ MAVEN_HOME / conf</span></em><span>或</span><em><span>〜/ .m2中</span></em><span>的&nbsp;&nbsp;</span></span><span><span>settings.xml文件</span></span><span><span>，</span></span></span></p>
<p><span><span><span>2. 找到&lt;pluginGroups&gt;节点，追加&nbsp;</span></span></span>org.sonarsource.scanner.maven&nbsp;这个插件</p>
<p><span><span><span>3. 找到以设置插件前缀和可选的SonarQube服务器URL。</span></span></span></p>
<p>Settings.xml 内容示例如下：</p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">settings</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">pluginGroups</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">pluginGroup</span><span style="color: #0000ff;">&gt;</span>org.sonarsource.scanner.maven<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">pluginGroup</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">pluginGroups</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">profiles</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">profile</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>sonar<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">activation</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">activeByDefault</span><span style="color: #0000ff;">&gt;</span>true<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">activeByDefault</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">activation</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">properties</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> Optional URL to server. Default value is http://localhost:9000 </span><span style="color: #008000;">--&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.host.url</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
                  http://myserver:9000
                </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.host.url</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">properties</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">profile</span><span style="color: #0000ff;">&gt;</span>
     <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">profiles</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">settings</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<h1><span>局部设置</span></h1>
<p><span>如果只是对单个项目需要配置，也可以采取局部设置服务器地址，即在自己项目的POM.xml 中配置如下：</span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">project </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="http://maven.apache.org/POM/4.0.0"</span><span style="color: #ff0000;">
    xmlns:xsi</span><span style="color: #0000ff;">="http://www.w3.org/2001/XMLSchema-instance"</span><span style="color: #ff0000;">
    xsi:schemaLocation</span><span style="color: #0000ff;">="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">modelVersion</span><span style="color: #0000ff;">&gt;</span>4.0.0<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">modelVersion</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>com.xingyun<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>SpringStaticFactoryPatternSample<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>0.0.1-SNAPSHOT<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 非必须中间的可删除 </span><span style="color: #008000;">--&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dependencies</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> https://mvnrepository.com/artifact/commons-logging/commons-logging </span><span style="color: #008000;">--&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>commons-logging<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>commons-logging<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>1.2<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> https://mvnrepository.com/artifact/org.springframework/spring-context </span><span style="color: #008000;">--&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>org.springframework<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>spring-context<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>5.1.2.RELEASE<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> https://mvnrepository.com/artifact/org.springframework/spring-core </span><span style="color: #008000;">--&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>org.springframework<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>spring-core<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>5.1.2.RELEASE<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> https://mvnrepository.com/artifact/org.springframework/spring-beans </span><span style="color: #008000;">--&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>org.springframework<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>spring-beans<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>5.1.2.RELEASE<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dependencies</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 非必须中间的可删除 </span><span style="color: #008000;">--&gt;</span>

    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">profiles</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">profile</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>sonar<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">activation</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">activeByDefault</span><span style="color: #0000ff;">&gt;</span>true<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">activeByDefault</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">activation</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">properties</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> Optional URL to server. Default value is http://localhost:9000 </span><span style="color: #008000;">--&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.host.url</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
                    http://localhost:9000
                </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.host.url</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">properties</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">profile</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">profiles</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">build</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">pluginManagement</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">plugins</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 配置编译插件 </span><span style="color: #008000;">--&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">plugin</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>org.apache.maven.plugins<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>maven-compiler-plugin<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>3.8.0<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">source</span><span style="color: #0000ff;">&gt;</span>1.8<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">source</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">target</span><span style="color: #0000ff;">&gt;</span>1.8<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">target</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">plugin</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">plugins</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">pluginManagement</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">build</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">project</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<h1 id="AnalyzingwithSonarQubeScannerforMaven-AnalyzingaMavenProject"><span>分析Maven项目</span></h1>
<h2><span>方法一：</span></h2>
<h2><span>使用Sonar 最新插件</span></h2>
<p><span><span><span>配置好后就可以开始分析Maven项目了，</span></span></span>在pom.xml文件所在的目录中运行Maven命令</p>
<div class="cnblogs_code">
<pre><span style="color: #000000;">mvn clean verify sonar:sonar
  
# In some situation you may want to run sonar:sonar goal as a dedicated step. Be sure to use install as first step for multi-module projects
mvn clean install
mvn sonar:sonar<br /></span></pre>
</div>
<p><span style="color: #000000;"><strong>这样当命令执行完毕后就可以在刚才的web 控制台看到刚才测试的项目了</strong></span></p>
<p><span style="color: #000000;"><strong>打开网址：<a href="http://localhost:9000/projects" target="_blank">http://localhost:9000/projects</a></strong></span></p>
<p><span style="color: #000000;"><strong><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115094658504-2126968295.png" alt="" /></strong></span></p>
<p>&nbsp;</p>
<h2><span style="color: #000000;"><strong>方法二：</strong></span></h2>
<h2><span style="color: #000000;"><strong>指定Sonar 插件版本</strong></span></h2>
<p><span style="color: #000000;"><strong>如果需要指定sonar-maven-plugin的版本而不是使用最新版本</strong></span></p>
<p><span style="color: #000000;"><strong>那么需要在项目的POM.xml 中指定版本如下：</strong></span></p>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">project </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="http://maven.apache.org/POM/4.0.0"</span><span style="color: #ff0000;">
    xmlns:xsi</span><span style="color: #0000ff;">="http://www.w3.org/2001/XMLSchema-instance"</span><span style="color: #ff0000;">
    xsi:schemaLocation</span><span style="color: #0000ff;">="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">modelVersion</span><span style="color: #0000ff;">&gt;</span>4.0.0<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">modelVersion</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>com.xingyun<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span><span style="color: #0000ff;">TestSample</span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>0.0.1-SNAPSHOT<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">profiles</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">profile</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>sonar<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">activation</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">activeByDefault</span><span style="color: #0000ff;">&gt;</span>true<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">activeByDefault</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">activation</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">properties</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> Optional URL to server. Default value is http://localhost:9000 </span><span style="color: #008000;">--&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.host.url</span><span style="color: #0000ff;">&gt;</span><span style="color: #000000;">
                    http://localhost:9000
                </span><span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.host.url</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">properties</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">profile</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">profiles</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">build</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">pluginManagement</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">plugins</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 配置编译插件 </span><span style="color: #008000;">--&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">plugin</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>org.apache.maven.plugins<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>maven-compiler-plugin<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>3.8.0<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">source</span><span style="color: #0000ff;">&gt;</span>1.8<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">source</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">target</span><span style="color: #0000ff;">&gt;</span>1.8<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">target</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">plugin</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 配置分析扫描插件 </span><span style="color: #008000;">--&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">plugin</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>org.sonarsource.scanner.maven<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>sonar-maven-plugin<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>3.5.0.1254<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">plugin</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">plugins</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">pluginManagement</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">build</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">project</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<h2>&nbsp;</h2>
<p><span><strong>然后执行如下命令：</strong></span></p>
<div class="cnblogs_code">
<pre><span># Specify the version of sonar-maven-plugin instead of using the latest. See also 'How to Fix Version of Maven Plugin' below.
mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.5.0.1254:sonar</span></pre>
</div>
<p><span><strong>这样当命令执行完毕后就可以在刚才的web 控制台看到刚才测试的项目了</strong></span></p>
<h2>&nbsp;</h2>
<p><span><strong>打开网址：<a href="http://localhost:9000/projects" target="_blank">http://localhost:9000/projects</a></strong></span></p>
<h2>&nbsp;</h2>
<p><span><strong><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115094658504-2126968295.png" alt="" /></strong></span></p>
<h2>&nbsp;</h2>
<h2><span style="color: #000000;"><strong>方法三：</strong></span></h2>
<p><span style="color: #000000;"><strong>要将JaCoCo作为Maven构建的一部分执行以生成JaCoCo&nbsp;的<strong>二进制格式，即在target 目录下生成jacoco.exec 文件</strong></strong></span></p>
<p><span style="color: #000000;"><strong><strong><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115095543977-1808626242.png" alt="" /></strong></strong></span></p>
<p><span style="color: #000000;"><strong>请使用以下命令：&nbsp;</strong></span></p>
<div class="cnblogs_code">
<pre>mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install sonar:sonar</pre>
</div>
<p><span style="color: #000000;"><strong>如果需要忽略测试失败</strong></span></p>
<div class="cnblogs_code">
<pre>mvn clean org.jacoco:jacoco-maven-plugin:prepare-agent install -Dmaven.test.failure.ignore=false sonar:sonar</pre>
</div>
<p>&nbsp;</p>
<p><strong>然后执行如下命令：</strong></p>
<p>&nbsp;</p>
<div class="cnblogs_code">
<pre># Specify the version of sonar-maven-plugin instead of using the latest. See also 'How to Fix Version of Maven Plugin' below.
mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.5.0.1254:sonar</pre>
</div>
<p>&nbsp;</p>
<p><strong>这样当命令执行完毕后就可以在刚才的web 控制台看到刚才测试的项目了</strong></p>
<p>&nbsp;</p>
<p><strong>打开网址：<a href="http://localhost:9000/projects" target="_blank">http://localhost:9000/projects</a></strong></p>
<p>&nbsp;</p>
<p><strong><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115094658504-2126968295.png" alt="" /></strong></p>
<p>&nbsp;</p>
<hr />
<p>&nbsp;</p>
<h1><strong>开启身份认证</strong></h1>
<p>不知道你有没有发现，我们直接执行命令后便将分析报告提交到web控制台了，没有加任何权限验证，这样是非常不安全的。</p>
<p>还记得之前我们登陆web控制台么？<strong><a href="http://localhost:9000/" target="_blank">http://localhost:9000/</a></strong></p>
<h3><span>默认管理员凭据</span></h3>
<p><span>安装SonarQube时，会自动创建具有&ldquo;管理系统&rdquo;权限的默认用户：</span></p>
<ul>
<li><span>登录：admin</span></li>
<li><span>密码：admin</span></li>
</ul>
<p><span>我们可以在项目中通过配置账号和密码方式来实现身份认证，但是这样仍然不是很安全，登陆密码容易泄露。</span></p>
<h2><span>开启Token 身份认证</span></h2>
<p><strong>1. 打开身份认证开关</strong></p>
<p><span>&nbsp;<strong>Administration &gt; Configuration &gt; General Settings &gt; Security</strong>, 然后设置&nbsp;<strong>Force user authentication</strong>&nbsp;属性为true</span></p>
<p><span><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115105108761-2099134999.png" alt="" /></span></p>
<p>2. 创建一个用户</p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115105424230-2093315158.png" alt="" width="972" height="317" /></p>
<p>点击创建后输入账号和密码,输入Email , 然后点击create 即可</p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115105525781-335579483.png" alt="" /></p>
<p>3.&nbsp;点击下图位置</p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115105938273-1154305026.png" alt="" /></p>
<p>弹出如下对话框</p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115105829984-1111079635.png" alt="" /></p>
<p>&nbsp;执行成功后如下所示：</p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115110139174-1256153251.png" alt="" width="841" height="145" /></p>
<p>点击sonar-users 下的图标，弹出如下图所示</p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115110639216-17313553.png" alt="" /></p>
<p>勾选后点击done 完成</p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115110737619-1023295267.png" alt="" /></p>
<p>将Execute Analysis 下对勾勾选，即可为该用户组添加分析执行权限</p>
<p><img src="https://img2018.cnblogs.com/blog/622489/201811/622489-20181115111527620-463742543.png" alt="" /></p>
<p>&nbsp;</p>
<p>&nbsp;由于我们创建的用户属于这两个用户组，所以给这个组赋予权限，那么我们的用户便也有权限了。</p>
<p>参考资料：<a href="https://docs.sonarqube.org/latest/instance-administration/security/" target="_blank">https://docs.sonarqube.org/latest/instance-administration/security/</a></p>
<h2 id="header-3"><span>恢复管理员访问权限</span></h2>
<p><span>如果您更改了</span><code>admin</code><span><span>密码</span><span>然后丢失了</span><span>密码，则可以使用以下查询重置密码：</span></span></p>
<div class="cnblogs_code">
<pre>update users set crypted_password = '$2a$12$uCkkXmhW5ThVK8mpBvnXOOJRLd64LJeHTeCkSuB3lfaR2N0AYBaSi', salt=null, hash_method='BCRYPT' where login = 'admin'</pre>
</div>
<p><span>如果您已删除</span><code>admin</code><span>并随后锁定具有全局管理权限的其他用户，则需要</span><code>admin</code><span><span>使用以下查询</span><span>重新授予</span><span>用户：</span></span></p>
<div class="cnblogs_code">
<pre>INSERT INTO user_roles(user_id, role) VALUES ((select id from users where login='mylogin'), 'admin');</pre>
</div>
<p>&nbsp;</p>
<hr />
<p>&nbsp;</p>
<pre><code>参考模板示例一：<br />pom.xml</code></pre>
<div class="cnblogs_code">
<pre><span style="color: #008000;"><span style="color: #0000ff;">&lt;project&gt;</span><br />&lt;!--</span><span style="color: #008000;"> 代码扫描步骤 </span><span style="color: #008000;">--&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">profiles</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">profile</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>sonar<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">activation</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">activeByDefault</span><span style="color: #0000ff;">&gt;</span>true<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">activeByDefault</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">activation</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">properties</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.jdbc.url</span><span style="color: #0000ff;">&gt;</span>jdbc:mysql://******:3306/sonar?useUnicode=true<span style="color: #ff0000;">&amp;amp;</span>characterEncoding=utf8<span style="color: #ff0000;">&amp;amp;</span>rewriteBatchedStatements=true<span style="color: #ff0000;">&amp;amp;</span>useConfigs=maxPerformance<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.jdbc.url</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.jdbc.driver</span><span style="color: #0000ff;">&gt;</span>com.mysql.jdbc.Driver<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.jdbc.driver</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.jdbc.username</span><span style="color: #0000ff;">&gt;</span>sonar<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.jdbc.username</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.jdbc.password</span><span style="color: #0000ff;">&gt;</span>sonar<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.jdbc.password</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.host.url</span><span style="color: #0000ff;">&gt;</span>http://172.*.*.*:9000<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.host.url</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.login</span><span style="color: #0000ff;">&gt;</span>ce57e****************4a8969<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.login</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.sourceEncoding</span><span style="color: #0000ff;">&gt;</span>UTF-8<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.sourceEncoding</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.sonar.test.inclusions</span><span style="color: #0000ff;">&gt;</span>.<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.sonar.test.inclusions</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.exclusions</span><span style="color: #0000ff;">&gt;</span>src/test/java/**<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.exclusions</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">properties</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">profile</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">profile</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>sonar-coverage<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">activation</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">activeByDefault</span><span style="color: #0000ff;">&gt;</span>true<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">activeByDefault</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">activation</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">build</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">pluginManagement</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">plugins</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">plugin</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>org.jacoco<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>jacoco-maven-plugin<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>0.7.9<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">plugin</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">plugins</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">pluginManagement</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">plugins</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">plugin</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>org.jacoco<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>jacoco-maven-plugin<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">append</span><span style="color: #0000ff;">&gt;</span>true<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">append</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">executions</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">execution</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>agent-for-ut<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">goals</span><span style="color: #0000ff;">&gt;</span>
                                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">goal</span><span style="color: #0000ff;">&gt;</span>prepare-agent<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">goal</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">goals</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">execution</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">execution</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>jacoco-site<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">phase</span><span style="color: #0000ff;">&gt;</span>verify<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">phase</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">goals</span><span style="color: #0000ff;">&gt;</span>
                                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">goal</span><span style="color: #0000ff;">&gt;</span>report<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">goal</span><span style="color: #0000ff;">&gt;</span>
                                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">goals</span><span style="color: #0000ff;">&gt;</span>
                            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">execution</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">executions</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">plugin</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">plugins</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">build</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">profile</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">profiles</span><span style="color: #0000ff;">&gt;<br />&lt;/project&gt;</span></pre>
</div>
<p>&nbsp;</p>
<pre><code>参考模板示例二:<br />pom.xml</code></pre>
<div class="cnblogs_code">
<pre><span style="color: #0000ff;">&lt;</span><span style="color: #800000;">project </span><span style="color: #ff0000;">xmlns</span><span style="color: #0000ff;">="http://maven.apache.org/POM/4.0.0"</span><span style="color: #ff0000;">
    xmlns:xsi</span><span style="color: #0000ff;">="http://www.w3.org/2001/XMLSchema-instance"</span><span style="color: #ff0000;">
    xsi:schemaLocation</span><span style="color: #0000ff;">="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">modelVersion</span><span style="color: #0000ff;">&gt;</span>4.0.0<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">modelVersion</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>com.xingyun<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>SpringStaticFactoryPatternSample<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>0.0.1-SNAPSHOT<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 非必须中间的可删除 </span><span style="color: #008000;">--&gt;</span>
    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dependencies</span><span style="color: #0000ff;">&gt;</span>

        <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> https://mvnrepository.com/artifact/commons-logging/commons-logging </span><span style="color: #008000;">--&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>commons-logging<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>commons-logging<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>1.2<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> https://mvnrepository.com/artifact/org.springframework/spring-context </span><span style="color: #008000;">--&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>org.springframework<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>spring-context<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>5.1.2.RELEASE<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> https://mvnrepository.com/artifact/org.springframework/spring-core </span><span style="color: #008000;">--&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>org.springframework<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>spring-core<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>5.1.2.RELEASE<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> https://mvnrepository.com/artifact/org.springframework/spring-beans </span><span style="color: #008000;">--&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>org.springframework<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>spring-beans<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>5.1.2.RELEASE<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dependency</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">dependencies</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 非必须中间的可删除 </span><span style="color: #008000;">--&gt;</span>

    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">profiles</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">profile</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>sonar<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">id</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">activation</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">activeByDefault</span><span style="color: #0000ff;">&gt;</span>true<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">activeByDefault</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">activation</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">properties</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> Optional URL to server. Default value is http://localhost:9000 </span><span style="color: #008000;">--&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.host.url</span><span style="color: #0000ff;">&gt;</span>http://localhost:9000<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.host.url</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 配置字符编码 </span><span style="color: #008000;">--&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.sourceEncoding</span><span style="color: #0000ff;">&gt;</span>UTF-8<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.sourceEncoding</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 该项目的独特关键。允许的字符是：字母，数字 - ， _ ， . 和 : ，与至少一个非数字字符。 </span><span style="color: #008000;">--&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.projectKey</span><span style="color: #0000ff;">&gt;</span>:<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.projectKey</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 包含源文件的目录的逗号分隔路径。 </span><span style="color: #008000;">--&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.sources</span><span style="color: #0000ff;">&gt;&lt;/</span><span style="color: #800000;">sonar.sources</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 将在Web界面上显示的项目的名称。 </span><span style="color: #008000;">--&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.projectName</span><span style="color: #0000ff;">&gt;</span>Custom Project<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.projectName</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 项目版本 </span><span style="color: #008000;">--&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.projectVersion</span><span style="color: #0000ff;">&gt;</span>V0.0.1<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.projectVersion</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">sonar.coverage.jacoco.xmlReportPaths</span><span style="color: #0000ff;">&gt;</span>target/site/jacoco/jacoco.xml<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">sonar.coverage.jacoco.xmlReportPaths</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">properties</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">profile</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">profiles</span><span style="color: #0000ff;">&gt;</span>

    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">build</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">pluginManagement</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">plugins</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #008000;">&lt;!--</span><span style="color: #008000;"> 配置编译插件 </span><span style="color: #008000;">--&gt;</span>
                <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">plugin</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>org.apache.maven.plugins<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">groupId</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>maven-compiler-plugin<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">artifactId</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>3.8.0<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">version</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">source</span><span style="color: #0000ff;">&gt;</span>1.8<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">source</span><span style="color: #0000ff;">&gt;</span>
                        <span style="color: #0000ff;">&lt;</span><span style="color: #800000;">target</span><span style="color: #0000ff;">&gt;</span>1.8<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">target</span><span style="color: #0000ff;">&gt;</span>
                    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">configuration</span><span style="color: #0000ff;">&gt;</span>
                <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">plugin</span><span style="color: #0000ff;">&gt;</span>
            <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">plugins</span><span style="color: #0000ff;">&gt;</span>
        <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">pluginManagement</span><span style="color: #0000ff;">&gt;</span>
    <span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">build</span><span style="color: #0000ff;">&gt;</span>
<span style="color: #0000ff;">&lt;/</span><span style="color: #800000;">project</span><span style="color: #0000ff;">&gt;</span></pre>
</div>
<p>&nbsp;</p>
<pre><code><br /><br /><br /></code></pre>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p>&nbsp;</p>
<p><span style="color: #ff0000;"><strong>&nbsp;</strong></span></p></div><div id="MySignature"></div>
<div class="clear"></div>
<div id="blog_post_info_block">
<div id="BlogPostCategory"></div>
<div id="EntryTag"></div>
<div id="blog_post_info">
</div>
<div class="clear"></div>
<div id="post_next_prev"></div>
</div>


		</div>
