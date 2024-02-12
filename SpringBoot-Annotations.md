# SpringBoot annotations 

**Starting Annotation**

```
@SpringBootApplication: 
It is a combination of three annotations 
```
```
1. @EnableAutoConfiguration: 
It auto-configures the bean that is present in the classpath and configures it to run the methods. The use of this annotation is reduced in Spring Boot 
```
```
2. @ComponentScan
```
```
3. @Configuration.
```
Stero Type Annotations : These annotations are used to create Spring beans automatically in the application context

@Service
@Repository
@Controller
@Component

Class Level Annotations

Bean/ Method level Annotations

You can create a controller without @Controller or @RestController annotations by annotating the Spring MVC Controller classes using the @Component annotation. In this case, the real job of request mapping to handler method is done using the @RequestMapping annotation.
