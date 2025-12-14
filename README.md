# spring all annotations 

1. Spring Core Annotations
2. Spring Web Annotations
3. Spring Boot Annotations
4. Spring Scheduling Annotations
5. Spring Data Annotations
6. Spring Bean Annotations

**1. Spring Core Annotations**
DI-Related Annotations
1. @Autowired - Injects a Spring bean dependency automatically by type.
2. @Qualifier - Specifies which bean to inject when multiple beans of the same type exist.
3. @Primary - Marks a bean as the default choice when multiple candidates are available.
4. @Bean - Declares a method that produces a Spring-managed bean.
5. @Lazy - Delays bean initialization until it is first requested.
6. @Required - Ensures a property must be set during bean initialization (deprecated in newer Spring versions).
7. @Value - Injects values from properties files, environment variables, or expressions.
8. @Scope - Defines the lifecycle scope of a bean (singleton, prototype, request, session, etc.).
9. @Lookup - Instructs Spring to return a fresh bean instance from the container at runtime.

Context Configuration Annotations
1. @Profile - Activates a bean only when a specific Spring profile is enabled.
2. @Import - Imports additional configuration classes into the Spring context.
3. @ImportResource - Loads bean definitions from XML configuration files.
4. @PropertySource - Adds external properties files to the Spring Environment.
	
**2. Spring Web Annotations**
1. @RequestMapping
2. @RequestBody
3. @PathVariable
4. @RequestParam
5. @Controller
6. @RestController
7. @ModelAttribute - Binds request parameters to a model object and exposes it to the view in Spring MVC.
8. @CrossOrigin
   
Response Handling Annotations
1. @ResponseBody
2. @ExceptionHandler
3. @ResponseStatus
	
**3. Spring Boot Annotations**
1. @SpringBootApplication
2. @EnableAutoConfiguration
	
Auto-Configuration Conditions
1. @ConditionalOnClass, and. @ConditionalOnMissingClass
2. @ConditionalOnBean, and. @ConditionalOnMissingBean
3. @ConditionalOnProperty
4. @ConditionalOnResource
5. @ConditionalOnWebApplication and. @ConditionalOnNotWebApplication
6. @ConditionalExpression
7. @Conditional
	
**4. Spring Scheduling Annotations**
1. @EnableAsync - Enables Spring’s asynchronous method execution capability.
2. @EnableScheduling - Enables support for scheduled task execution in Spring.
3. @Async - Executes a method asynchronously in a separate thread.
4. @Scheduled - Schedules a method to run at fixed times or intervals.
5. @Schedules - Allows multiple @Scheduled annotations on a single method.
	
**5. Spring Data Annotations**
Common Spring Data Annotations
1. @Transactional
2. @NoRepositoryBean
3. @Param
4. @Id
5. @Transient
6. @CreatedBy,. @LastModifiedBy,. @CreatedDate,. @LastModifiedDate
	
Spring Data JPA Annotations
1. @Query
2. @Procedure
3. @Lock
4. @Modifying
5. @EnableJpaRepositories
	
Spring Data Mongo Annotations
1. @Document
2. @Field
3. @Query
4. @EnableMongoRepositories
	
**6. Spring Bean Annotations**
1. @ComponentScan
2. @Configuration
	
Stereotype Annotations
1. @Component
2. @Service
3. @Repository
4. @Controller



