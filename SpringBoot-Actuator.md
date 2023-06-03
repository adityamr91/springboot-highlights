#  SpringBoot Actuator

**Import Dependency**
```
<dependency>  
    <groupId>org.springframework.boot</groupId>  
    <artifactId>spring-boot-starter-actuator</artifactId>  
    <version>2.2.2.RELEASE</version>  
</dependency>  
```

**End Points**
```
actuator	It provides a hypermedia-based discovery page for the other endpoints. It requires Spring HATEOAS to be on the classpath.	
auditevents	It exposes audit events information for the current application.	
autoconfig	It is used to display an auto-configuration report showing all auto-configuration candidates and the reason why they 'were' or 'were not' applied.	
beans	It is used to display a complete list of all the Spring beans in your application.	
configprops	It is used to display a collated list of all @ConfigurationProperties.	
dump	It is used to perform a thread dump.	
env	It is used to expose properties from Spring's ConfigurableEnvironment.	
flyway	It is used to show any Flyway database migrations that have been applied.	
health	It is used to show application health information.	False
info	It is used to display arbitrary application info.	False
loggers	It is used to show and modify the configuration of loggers in the application.	
liquibase	It is used to show any Liquibase database migrations that have been applied.	
metrics	It is used to show metrics information for the current application.	
mappings	It is used to display a collated list of all @RequestMapping paths.	
shutdown	It is used to allow the application to be gracefully shutdown.	
trace	It is used to display trace information.	
```

