title: 使用Maven管理第三方的JAR包
---

## 情景描述

基于 maven 管理的项目中，引用了第三方直接打包好的 jar，此时应该如何管理这些 jar 包。  
参考问题及相关答案 ：[Go to stackoverflow](http://stackoverflow.com/a/31023523/4134671)

## 解决办法

参考代码：[com-gansuer-algorithm](https://github.com/FrankBian/Java-Utils-Collection)

+ 在 webapp 目录下新加一个目录 lib(专门用来存放项目中用到的第三方 jar 文件)
+ 在该 module 的 pom.xml 中声明这个 dependency ：

```
		<!--此处的groupId 和 artifactId 根据自己喜好随便起-->	
		<dependencies>
			<dependency>
				<groupId>com.mylib</groupId>
				<artifactId>com-mylib-stdlib</artifactId>
				<version>1.0.0</version>
			</dependency>
		</dependencies>
```
+ 导入 maven-install 插件，将上面的第三方jar 安装到本地仓库 ：

```
    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-install-plugin</artifactId>
                <version>2.5.2</version>
                <executions>
                    <execution>
                        <id>install-external</id>
                        <phase>clean</phase>
                        <configuration>
                            <file>${basedir}/src/main/webapp/lib/stdlib.jar</file>
                            <repositoryLayout>default</repositoryLayout>
                            <groupId>com.mylib</groupId>
                            <artifactId>com-mylib-stdlib</artifactId>
                            <version>1.0.0</version>
                            <packaging>jar</packaging>
                            <generatePom>true</generatePom>
                        </configuration>
                        <goals>
                            <goal>install-file</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
```  

+ 配置完成之后，运行 ``` maven clean ```，第三方jar 包即被安装到本地仓库