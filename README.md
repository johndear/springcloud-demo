
# maven入门  

* setting.xml    
```
	<localRepository>D:\BrowerDownload\apache-maven-3.5.0\conf\local\repository</localRepository>  

  	<!-- Nexus 构件部署用户信息 -->
	<server>
      		<id>dev</id>
      		<username>admin</username>
      		<password>admin123</password>
    	</server>  
    
    	<!-- 不同环境配置，从不同库下载、上传, 并打包对应环境配置 -->
	<profile>
		<id>dev</id>
		<properties>
			<!-- 使用对应环境的配置文件 -->
			<package.environment>dev</package.environment>
			<!-- 以下对应distributionManagement参数值，是上传构建到远程私服配置，mvn deploy -->  
			<repository.id>dev</repository.id>
			<repository.name>ls-mvn-snapshots</repository.name>
			<repository.url>http://127.0.0.1:8081/nexus/content/repositories</repository.url><!-- 自动对应到snapshots和releases2个库 -->
		</properties>
		<!-- 只负责下载，不负责上传（上传使用上面distributionManagement配置） -->
		<repositories>
			<repository>
			  <id>dev</id>
			  <name>dev Repository</name>
			  <url>http://127.0.0.1:8081/nexus/content/repositories/snapshots</url>
			  <layout>default</layout>
			  <snapshots>
				<enabled>true</enabled>
			  </snapshots>
			</repository>
		  </repositories>
		  <pluginRepositories>
			<pluginRepository>
			  <id>dev</id>
			  <name>dev Repository</name>
			  <url>http://127.0.0.1:8081/nexus/content/repositories/snapshots</url>
			  <layout>default</layout>
			  <snapshots>
				<enabled>false</enabled>
			  </snapshots>
			  <releases>
				<updatePolicy>never</updatePolicy>
			  </releases>
			</pluginRepository>
		  </pluginRepositories>
	</profile>
	<activeProfiles>
		<activeProfile>dev</activeProfile>
	</activeProfiles>  
```
   
* pom.xml  
```   	
	<!-- 上传构建到远程私服配置，mvn deploy -->
	<distributionManagement>
		<snapshotRepository>
			<id>${repository.id}</id>
			<name>${repository.name}-snapshots</name>
			<url>${repository.url}/snapshots/</url>
		</snapshotRepository>  
	    <repository>  
	        <id>${repository.id}</id>  
	        <name>${repository.name}-releases</name>  
	        <url>${repository.url}/releases/</url>  
	    </repository> 
	</distributionManagement>
```
<img src="https://thumbnail0.baidupcs.com/thumbnail/c9c1a89f91defab8987072852eafebef?fid=3189207338-250528-475511094875812&time=1536418800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-CYdISTF5ZrnDffYsBQCx6rJk8yw%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5820791610589944698&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video" target="_blank" width = "100%" height = "270" alt="maven继承关系" align=center /> 


<img src="https://thumbnail0.baidupcs.com/thumbnail/b9b46592d707bf98e0fb0c00442b418e?fid=3189207338-250528-245902189525537&time=1536418800&rt=sh&sign=FDTAER-DCb740ccc5511e5e8fedcff06b081203-lzXzpHHun9%2FNaxavLuoSc%2F7oS6U%3D&expires=8h&chkv=0&chkbd=0&chkpc=&dp-logid=5820864608380701415&dp-callid=0&size=c710_u400&quality=100&vuk=-&ft=video" target="_blank" width = "100%" height = "270" alt="maven打包不同环境的配置文件" align=center /> 



    
    

