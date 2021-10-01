# Docker

## 一、docker常用命令

* images
* build

## 二、docker打包springboot项目

1、项目pom.xml加入

```text
<!-- 使用Maven插件直接将应用打包为一个Docker镜像 -->
            <plugin>
                <groupId>com.spotify</groupId>
                <!-- 这里使用新版dockerfile-maven-plugin插件 -->
                <artifactId>dockerfile-maven-plugin</artifactId>
                <executions>
                    <execution>
                        <id>default</id>
                        <goals>
                            <goal>build</goal>

                        </goals>
                    </execution>
                </executions>

                <version>1.4.3</version>
                <configuration>
                    <!-- Dockerfile目录指定，指定时会包imagid错误，不知道为什么 -->
<!--                <dockerfile>src/main/docker/Dockerfile</dockerfile>-->
                    <repository>a9805943/${project.artifactId}</repository>
                    <!-- 生成镜像标签 如不指定 默认为latest -->
                    <tag>${project.version}</tag>
                    <buildArgs>
                        <!-- 理论上这里定义的参数可以传递到Dockerfile文件中，目前未实现 -->
                        <JAR_FILE>target/${project.build.finalName}.jar</JAR_FILE>
                    </buildArgs>
                </configuration>
            </plugin>
```

2、根目录下加入Dockerfile

```text
#基础镜像，如果本地仓库没有，会从远程仓库拉取
FROM openjdk:8-jdk-alpine
#容器中创建目录
RUN mkdir -p /usr/local/pasq
#编译后的jar包copy到容器中创建到目录内
COPY target/springboot-log4j2.jar /usr/local/pasq/app.jar
#指定容器启动时要执行的命令
ENTRYPOINT ["java","-jar","/usr/local/pasq/app.jar"]
```

3、点击maven install 或mavn install

4、执行docker images查看打包后的镜像，上传至dockerhub上。

