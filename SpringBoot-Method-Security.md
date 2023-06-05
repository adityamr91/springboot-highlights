# SpringBoot Method Security

**1. Import Dependency**
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```
**2. Create this class and do the settings**
```
@Configuration
@EnableGlobalMethodSecurity(
  prePostEnabled = true, 
  securedEnabled = true, 
  jsr250Enabled = true)
public class MethodSecurityConfig 
  extends GlobalMethodSecurityConfiguration {
}
```
**The prePostEnabled property enables Spring Security pre/post annotations.
**The securedEnabled property determines if the @Secured annotation should be enabled.
**The jsr250Enabled property allows us to use the @RoleAllowed annotation.

