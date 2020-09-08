# java 基础知识
## 环境搭建
1. 开发工具
   1. [idea 使用](https://github.com/judasn/IntelliJ-IDEA-Tutorial)
2. jdk 
   1. ![体系图](https://simple-images.oss-cn-beijing.aliyuncs.com/19-1-10/25967434.jpg)
## java.lang
1. java 基础类型(primitive type) 
    - int,bool,byte,char,string,float,double,short
    - 与引用类型 interge 之间由编译器默认box,unbox
    - List<Interge> 而不是 List<int>
2. lambda expression
    - ()->{}  Class::method Interge[]::new
3. java reflction
    - package [org.reflections](https://github.com/ronmamo/reflections)
    - 获取 泛型类型 
        1. 作为参数传递
        ``` java
        public class GenericClass<T> {
            private final Class<T> type;

            public GenericClass(Class<T> type) {
                this.type = type;
            }

            public Class<T> getMyType() {
                return this.type;
            }
        }
        ```
4. java string equals
   - **use equals,not ==**
5. String,StringBuilder,StringBuffer
    1. String is immutable,StringBuilder and StringBuffer is mutable
    2. StringBuilder isn't thread safe,but StringBuffer is,because synchronized
6. String.format 格式说明
    1. %s %d %f %tx [总结](https://blog.csdn.net/lonely_fireworks/article/details/7962171)
7. annotation
    1. 用源注解 定义 自定义注解  
    @Target：指明这个注解可以用在哪些语言元素上，例如方法，类型，函数参数等。  
    @Retention：指明注解的存储方式，分别是 SOURCE（只存在于代码中，编译完成后被丢弃），  CLASS（存储在生成的 class 文件中，但是会被 VM 在运行期丢弃），RUNTIME（存储在 class 文件中，并且 VM 在运行期间也会保留，因此可以使用反射获得），默认的存储方式是 CLASS。  
    @Documented：指明使用了这个注解的代码，其生成的 Javadoc 中会把此注解展示出来  
    @Inherited：这里没有使用，它是用于标记 Target 是 Class 的 Annotation 的，在其他类型的 Annotation 上使用不起作用。它标记对于父类的注解，会被子类做继承，默认行为是不继承。  
8. [volatile](https://www.cnblogs.com/dolphin0520/p/3920373.html)
   1. 原子性,只有基本的赋值操作具有原子性, 例 int i=0;
   2. 可见性,不同高速缓存中,对变量修改后的可见性
   3. 有序性,在保证结果相同的前提下,jvm 对代码执行顺序进行重排,多线程模型下的共享变量的访问可能会出现问题
   4. volatie 保证了可见性,无法保证原子性和可见性,synchronized & lock 保证了1,2,3,但是效率低于volatie
9. [RuntimeException and Exception](https://stackoverflow.com/questions/2190161/difference-between-java-lang-runtimeexception-and-java-lang-exception)
   1. RuntimeException 是在运行时才会抛出的错误,不需要显式 catch 或者 signture
   2. Exception 需要显式 catch 或者 signture,否则编译不通过
   3. 如何选择使用哪种 Exception ?
      1. 可以通过程序内部来避免出现的异常使用RuntimeException,例如 NullPointerException
      2. 如果可能由于外部硬件导致的未知错误,使用 Exception,例如 IOException

## 多线程（multiple thread）
1. [executor](http://wiki.jikexueyuan.com/project/java-concurrency/executor.html)
   1. execute（Runnable command）,直接执行某个runnable实现
   2. ExecutorService，四种默认实现 newCachedThreadPool，newFixedThreadPool，newScheduledThreadPool，SingleThreadExecutor
   3. Callable 实现 async 返回结果，通过 Funture<?> 轮询，获取返回结果
   4. ThreadPoolExecutor 自定义线程池
   5. IDEL timeout,线程闲置时间，以此作为线程回收标准
   6. ThreadPool 的排队策略，直接提交、无界队列、有界队列

## java.generic
1. generic type erasure (泛型类型消除),对于泛型,在多态场景下,同一泛型类 不同泛型类型会被认为是同一参数类型(链接)[https://stackoverflow.com/questions/1998544/method-has-the-same-erasure-as-another-method-in-type]
``` java
// compilation error Method add(Set) has the same erasure add(Set) as another method in type Test.
class Test{
   void add(Set<Integer> ii){}
   void add(Set<String> ss){}
}
```

## [class loader](https://juejin.im/post/5c4c1957f265da61285a7592?utm_source=gold_browser_extension)
- 类加载过程, 加载->连接(验证,准备,解析)->初始化->使用->卸载(GC回收)
- 双亲委派模型 (启动类加载->扩展类加载->应用程序类加载->自定义加载)
- 破坏双亲委派模型 (1.兼容jdk1.2 2.jdbc,jndi等外部实现类 3.热部署,osgi 改为网状模型加载)
- tomcat 加载模式
  - web application 相互隔离
  - 相同版本 jar 使用相同方法区
  - web container 和 web application 隔离
  - 支持 jsp 的 web 容器,需要热部署

## 配置
### properties 文件
1. [配置读取](https://crunchify.com/java-properties-file-how-to-read-config-properties-values-in-java/)
2. 在 jvm 初始化时默认加载 properties文件,System.initProperties()?
3. spring 通过 PropertyPlaceholderConfigurer,ResourceLoaderAware 在初始化时完成 properties 加载

## 核心概念
1. (Servlet)[https://www.zhihu.com/question/21416727]
    - 一组定义服务从 init 到 destroy 的接口
    - 需要 servlet container 才能驱动服务,如 jboss,tomcat,jetty,resin,glassfish
    - [容器对比 Tomcat、JBoss、Resin、Glassfish 对比](https://www.cnblogs.com/wangpei/p/7060375.html)
    - 可以实现多种服务类型 socket,rpc, 但是更多的还是 http
    - (web 服务器)[https://www.cnblogs.com/aspirant/p/9088995.html] , servlet container 可以单独运行,也可以结合 web 服务器运行,如 apache,nginx
    - IIS = apache/ngnix, servlet = asp.net 区别在于 java 开源,各方可定制, .net 闭源,只能用官方实现
2. [Bean](https://www.jianshu.com/p/e6e9762cd8e8)
    - bean是一个由默认规范定义的类,由于 Java 语言欠缺属性、事件、多重继承功能,只能手写胶水代码,例如 getXXX(),setXXX() 等规范
        - 必须是个公有(public)类
        - 有无参构造函数
        - 用公共方法暴露内部成员属性(getter,setter)
    - (spring 简单解析)[https://www.zhihu.com/people/rong-ma-jun/posts]
3. 约定优于配置(Convention over configuration)
    1. spring 默认约定
    2. (maven 默认约定)[https://juvenshun.iteye.com/blog/293975][https://blog.csdn.net/u012152619/article/details/51510757]
    3. (tomcat 默认约定)[]

## [java web](https://skyline75489.github.io/Heart-First-JavaWeb/)

## 开发规范
### 注释
1. javadoc 格式,以便于生成文档

## stream api
参考
1. [Java 8 中的 Streams API 详解](https://www.ibm.com/developerworks/cn/java/j-lo-java8streamapi/index.html)
目的
> 利用 lamda expression 实现流式变成,提高程序可读性  
> stream api 内部封装多线程和并行任务,提高程序效率
概念
- Intermediate 数据处理中间状态  
  map (mapToInt, flatMap 等)、 filter、 distinct、 sorted、 peek、 limit、 skip、 parallel、 sequential、 unordered
- Terminal 数据完成状态  
  forEach、 forEachOrdered、 toArray、 reduce、 collect、 min、 max、 count、 anyMatch、 allMatch、 noneMatch、 findFirst、 findAny、 iterator
- Short-circuiting 对于集合 条件符合即返回  
  anyMatch、 allMatch、 noneMatch、 findFirst、 findAny、 limit

自定义 stream 实现
- 核心: 实现 Supplier<?> 类型
- 清单 22. 生成 10 个随机整数
``` java
Random seed = new Random();
Supplier<Integer> random = seed::nextInt;
//todo why can Integer[]::new convert   IntFunction<A[]> generator
return Stream.generate(random).limit(size).toArray(Integer[]::new);
//Another way
IntStream.generate(() -> (int) (System.nanoTime() % 100)).
limit(10).forEach(System.out::println);
```

## 设计模式
### 分类
1. 构造型
2. 动作型
    1. 状态模式 - 自动售货机模型
        1. [找零算法](http://wangxin93.top/algorithm/2018/06/03/dynamic-programming.html)
3. 结构型

## 打包部署
### 手工部署tomcat
1. tomcat 默认文件结构 WEB-INF , META-INF
2. WEB-INF > .xml , classes , lib

### spring boot , jar 包一键启动

## component
### 日志
1. (slf4j 兼容 commons-logging,log4j,logback)[https://www.slf4j.org/legacy.html]
2. (常用日志库对比)[https://www.cnblogs.com/jingmoxukong/p/5910309.html]
