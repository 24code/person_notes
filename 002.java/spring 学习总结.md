# spring 学习总结
## 基础架构
1. [spring 模块依赖解析](http://www.cnblogs.com/ywlaker/p/6136625.html)
2. [spring 项目解析](https://segmentfault.com/a/1190000011334873)
3. [spring 注解大全](https://blog.csdn.net/weixin_37490221/article/details/78406810)
4. [spring boot 项目结构最佳实践](http://blog.didispace.com/springbootproject/)
## spring boot
1. [spring boot 日志配置](https://www.jianshu.com/p/f67c721eea1b)
2. [spring boot live reload](https://dzone.com/articles/spring-boot-application-live-reload-hot-swap-with)
   - 配置修改无法 live reload
   - swagger2 annotation 修改后无法 live reload
## 常见问题
1. (NoSuchBeanDefinitionException)[https://juejin.im/entry/58aa8dda8ac247006e604025]
2. (JdbcTemplate could not be found)[https://stackoverflow.com/questions/28902140/how-to-use-springs-jdbctemplate-to-connect-to-a-simple-mysql-database]
## j2ee vs spring vs spring boot
1. 配置
   1. spring 通过 @PropertySource @value 注解注入,属于主动声明,不支持 yml 格式
   2. spring boot @ConfigurationProperties(prefix = "canal"),@EnableConfigurationProperties   
   注入属于默认约定,声明的 bean 符合规则都会被注入  
   支持多环境配置,多种配置文件格式
   3. j2ee 待补充
## 配套工具
### maven
1. [基础教程](http://www.runoob.com/maven/maven-tutorial.html)
2. [传递依赖冲突](https://blog.csdn.net/lkforce/article/details/62429998)
   - `mvn -Dverbose -Doutput=*.txt dependency:tree`
   - [Maven依赖分析](https://www.cnblogs.com/ywjy/p/7892018.html)
3. 
## 组件
1. [swagger2](https://juejin.im/post/5afe490ff265da0b8c253411)
  - 代码即文档,配合简单的测试功能,前后端能够及时沟通API
  - 配合 yapi,通过用例完美覆盖接口测试
