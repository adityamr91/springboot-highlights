# Springboot profiles for multienvironments (DEV, TEST, QA, PROD)

**1. Create an Interface**
```
public interface EnvService {

    String env();

}
```
**2. Create env class which implements interface**
```
@Service
@Profile({"dev", "default"})
public class Dev implements EnvService {

    @Override
    public String getEnv() {
        return "Dev set!";
    }

}
```
```
@Service
@Profile("prod")
public class Prod implements EnvService {

    @Override
    public String getEnv() {
        return "Prod set!";
    }

}
```

**3. @SpringBoot Application class which takes argument from commandLine or setenv.sh in tomcat for env demand**

@SpringBootApplication
public class Application implements CommandLineRunner {

    @Autowired
    private EnvService envService;

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

    @Override
    public void run(String... args) {
        System.out.println(envService.getEnv());
    }

}

**4. app.properties**

```
application.properties

# default profile is 'default'
#spring.profiles.active=dev

logging.level.=error
spring.main.banner-mode=off
```

**5. Calling off particular env**

```
public class TestApplication {

    @Test
    public void testDefaultProfile() {
        Application.main(new String[0]);
        String output = this.outputCapture.toString();
        assertThat(output).contains("Dev set!");
    }

    @Test
    public void testRainingProfile() {
        System.setProperty("spring.profiles.active", "prod");
        Application.main(new String[0]);
        String output = this.outputCapture.toString();
        assertThat(output).contains("Prod set!");
    }
