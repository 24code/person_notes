# maven 使用总结
## 作用
## 原理
## 技术名词
- 周期(lifecycle)
  - clean,default(build),site
- 阶段(phase)
  - validate,compile,test,package,verify,install,deploy
- [依赖(dependence)](https://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html)
  - 传递依赖(Transitive Dependencies)
  - [依赖范围(dependency scope)](https://blog.csdn.net/kimylrong/article/details/50353161)
    - compile 默认,整个打包,测试,部署都会包含
    - test 仅在test阶段包含
    - runtime 不参与complie,会包含在 test,deploy 阶段,用在服务用第三方提供,例如 jdbc
    - provided 参与 complie,test 不会包含在 deploy
    - system 从参与度来说，也provided相同，不过被依赖项不会从maven仓库抓，而是从本地文件系统拿，一定需要配合systemPath属性使用
  - 依赖管理(dependency management)
    - 冲突(conflict)

## 插件
- (maven 自动打包构建 war)[https://blog.csdn.net/github_26672553/article/details/79003090]
``` xml
    <build>
        <finalName>springdemo</finalName>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <version>3.2.2</version>
            </plugin>
        </plugins>
    </build>
```
- [maven 自动化构建](http://www.runoob.com/maven/maven-deployment-automation.html)
  - 配置 scm 代码库
  - 配置 distributionManagement maven 包管理工具

## API
- (maven 默认约定)[https://juvenshun.iteye.com/blog/293975][https://blog.csdn.net/u012152619/article/details/51510757]

## [常用命令](https://www.cnblogs.com/adolfmc/archive/2012/07/31/2616908.html)
- 创建一个简单的Java工程：mvn archetype:create -DgroupId=com.mycompany.example -DartifactId=Example
- 创建一个java的web工程：mvn archetype:create -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-webapp -DgroupId=com.mycompany.app -DartifactId=my-webapp
- 打包：mvn package
- 编译：mvn compile
- 编译测试程序：mvn test-compile
- 清空：mvn clean
- 运行测试：mvn test
- 生成站点目录: mvn site
- 生成站点目录并发布：mvn site-deploy
- 安装当前工程的输出文件到本地仓库: mvn install
- 安装指定文件到本地仓库：mvn install:install-file -DgroupId=<groupId> -DartifactId=<artifactId> -Dversion=1.0.0 -Dpackaging=jar -Dfile=<myfile.jar>
- 查看实际pom信息: mvn help:effective-pom
- 分析项目的依赖信息：mvn dependency:analyze 或 mvn dependency:tree
- 跳过测试运行maven任务： mvn -Dmaven.test.skip=true XXX
- 生成eclipse项目文件: mvn eclipse:eclipse
- 查看帮助信息：mvn help:help 或 mvn help:help -Ddetail=true
- 查看插件的帮助信息：mvn <plug-in>:help，比如：mvn dependency:help 或 mvn ant:help 等等。
