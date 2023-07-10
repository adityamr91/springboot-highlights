# spring all annotations 

1. Spring Core Annotations
2. Spring Web Annotations
3. Spring Boot Annotations
4. Spring Scheduling Annotations
5. Spring Data Annotations
6. Spring Bean Annotations

**1. Spring Core Annotations**
DI-Related Annotations
@Autowired
@Qualifier
@Primary
@Bean
@Lazy
@Required
@Value
@Scope
@Lookup, etc.
Context Configuration Annotations
@Profile
@Import
@ImportResource
@PropertySource, etc.

**2. Spring Web Annotations**
@RequestMapping
@RequestBody
@PathVariable
@RequestParam

Response Handling Annotations:
@ResponseBody
@ExceptionHandler
@ResponseStatus

@Controller
@RestController
@ModelAttribute
@CrossOrigin

**3. Spring Boot Annotations**
@SpringBootApplication
@EnableAutoConfiguration

Auto-Configuration Conditions :
@ConditionalOnClass, and @ConditionalOnMissingClass
@ConditionalOnBean, and @ConditionalOnMissingBean
@ConditionalOnProperty
@ConditionalOnResource
@ConditionalOnWebApplication and @ConditionalOnNotWebApplication
@ConditionalExpression
@Conditional

**4. Spring Scheduling Annotations**
@EnableAsync
@EnableScheduling
@Async
@Scheduled
@Schedules

**5. Spring Data Annotations**
Common Spring Data Annotations
@Transactional
@NoRepositoryBean
@Param
@Id
@Transient
@CreatedBy, @LastModifiedBy, @CreatedDate, @LastModifiedDate

Spring Data JPA Annotations
@Query
@Procedure
@Lock
@Modifying
@EnableJpaRepositories

Spring Data Mongo Annotations
@Document
@Field
@Query
@EnableMongoRepositories

**6. Spring Bean Annotations**
@ComponentScan
@Configuration

Stereotype Annotations:
@Component
@Service
@Repository
@Controller

