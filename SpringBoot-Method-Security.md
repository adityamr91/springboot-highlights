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
*//The prePostEnabled property enables Spring Security pre/post annotations.
*//The securedEnabled property determines if the @Secured annotation should be enabled.
*//The jsr250Enabled property allows us to use the @RoleAllowed annotation.

**3. Usage of method security annotations | @Secured & @RolesAllowed both are same anyone can be used**
```
@Secured("ROLE_VIEWER")
public String getUsername() {
    SecurityContext securityContext = SecurityContextHolder.getContext();
    return securityContext.getAuthentication().getName();
}

@Secured({ "ROLE_VIEWER", "ROLE_EDITOR" })
public boolean isValidUsername(String username) {
    return userRoleRepository.isValidUsername(username);
}

@RolesAllowed("ROLE_VIEWER")
public String getUsername2() {
    //...
}
    
@RolesAllowed({ "ROLE_VIEWER", "ROLE_EDITOR" })
public boolean isValidUsername2(String username) {
    //...
}
```

**4. Futher Security Checks**

*//The @PreAuthorize annotation checks the given expression before entering the method
*//The @PostAuthorize annotation verifies it after the execution of the method and could alter the result.

```
@PreAuthorize("hasRole('ROLE_VIEWER')")
public String getUsernameInUpperCase() {
    return getUsername().toUpperCase();
}

@PreAuthorize("#username == authentication.principal.username")
public String getMyRoles(String username) {
    //...
}

@PostAuthorize("#username == authentication.principal.username")
public String getMyRoles2(String username) {
    //...
}

@PostAuthorize
  ("returnObject.username == authentication.principal.nickName")
public CustomUser loadUserDetail(String username) {
    return userRoleRepository.loadUserByUserName(username);
}
```

*//Spring Security provides the @PreFilter annotation to filter a collection argument before executing the method:

```
@PreFilter("filterObject != authentication.principal.username")
public String joinUsernames(List<String> usernames) {
    return usernames.stream().collect(Collectors.joining(";"));
}

@PostFilter("filterObject != authentication.principal.username")
public List<String> getAllUsernamesExceptCurrent() {
    return userRoleRepository.getAllUsernames();
}
```

*//If we find ourselves using the same security annotation for every method within one class, we can consider putting that annotation at class level:
*//We can also use multiple security annotations on one method:
