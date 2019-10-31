# springboot日志   
####  作者:coresu   
####  时间:2019-10-30  


##### 日志框架   
在开发大型系统的时候，system.out.println把所有的输出下入到一个文件中  
用来监听一下系统运行过程中的运行情况。   
框架与框架之间的升级转换，需要修改API这样很麻烦   
现在使用JDBC以数据为驱动写一个统一的接口，日志抽象层    


给项目中导入具体的日志就可以了。   



市面上的日志框架  
JUL、JCL、Jboss-logging、logback、log4j、log4j2、slf4j。。。。。  

日志门面《===》日志的抽象层   



右面要选一个的实现    


日志门面:SLF4j   
日志实现:   


SLF4j的使用，在使用的时候不应该调用实现类，而应该调用抽象层


SLF4j的使用：   

Logger logger = LoggerFactory.getLogger(getClass());
logger.trace();
logger.debug();   


springboot默认听提供的是info级别的日志输出。
logger.info();
logger.warn();
logger.error();
调整级别要在application.yml中改变
logging.level.com.firstlearn=trace
logging.path= 在控制台输出，并在当前项目下输出
输出方式为在根路径下创建spring文件夹和里面的log文件夹，使用spring.log作为默认文件   
logging.pattern.console=   
logging.pattern.file=




logging.file= 会输出到指定文件中去  


# web开发   
开发步骤：   
1）：创建springboot应用，选中需要的模块  
2）：springboot已经将某些场景需要的配置封装好了，仅需在配置文件中进行少量配置便可以使得项目运行起来。   
3) ： 自己编写业务逻辑代码   
























