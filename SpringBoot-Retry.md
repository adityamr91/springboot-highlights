# SpringBoot retry / failover scenario

**1. Import dependecy**
```
<dependency>
    <groupId>org.springframework.retry</groupId>
    <artifactId>spring-retry</artifactId>
    <version>2.0.0</version>
</dependency>
```

**2. Create a config class with for the setup**
```
@Configuration
@EnableRetry
public class AppConfig { ... }
```
*// now all retryable annotation will be availabe for the use

**3. Use Annotations in Service or Controller Class as per need**

```
@Service
public interface MyService { 

    @Retryable(retryFor = SQLException.class)
    void retryServiceWithRecovery(String sql) throws SQLException; 
    
    @Retryable(retryFor = SQLException.class, maxAttempts = 2, backoff = @Backoff(delay = 100))
    void retryServiceWithCustomization(String sql) throws SQLException;

    @Recover
    void recover(SQLException e, String sql); 
}
```


