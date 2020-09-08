# spring boot 总结
## 基础搭建
1. 配置
2. 集成
3. [全局异常处理](https://www.javadevjournal.com/spring-boot/spring-boot-whitelabel-error-page/)

## 基础原理
### [spring boot autoconfiguration 原理](https://www.jianshu.com/p/346cac67bfcc)
1. 读取META-INF/spring.factories配置实现
   1. SpringFactoriesLoader loadFactoryNames 加载 META-INF/spring.factories
   2. org.springframework.boot.autoconfigure.EnableAutoConfiguration 指定自动配置属性
2. [自定义 starter 配置](https://www.jianshu.com/p/85460c1d835a)
   1. 参考 org.springframework.boot.autoconfigure spring.factories
   2. @EnableConfigurationProperties,@Configuration
   3. 按条件加载 @ConditionalOnWebApplication,@ConditionalOnClass,@ConditionalOnProperty
3. endpoint
   1. 可以理解为一个admin，包含对服务的描述、界面、交互（业务信息的查询）
4. health indicator：该starter提供的服务的健康指标

## 问题
1. spring boot configuration lowercase sensetive?
2. DependencyManagement & Dependencies different
   - Maven会沿着父子层次向上走，直到找到一个拥有dependencyManagement元素的项目，然后它就会使用在这个dependencyManagement元素中指定的版本号
   - dependencies即使在子项目中不写该依赖项，那么子项目仍然会从父项目中继承该依赖项（全部继承）
   - dependencyManagement里只是声明依赖，并不实现引入，因此子项目需要显示的声明需要用的依赖。
   - 如果不在子项目中声明依赖，是不会从父项目中继承下来的；只有在子项目中写了该依赖项，并且没有指定具体版本，才会从父项目中继承该项，并且version和scope都读取自父pom;
   - 另外如果子项目中指定了版本号，那么会使用子项目中指定的jar版本。
