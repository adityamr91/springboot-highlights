# SpringBoot JPA

**Create Enity Class for DB Table**
```
@Entity
@Table
public class Employee {
   @Id
   @Column
   private int id;

   @Column
   private String name;
 }
```

**Create Repository Interface Passing Entity Object to Extended CrudRepo Interface**

```
@Repository
public interface EmployeeRepository extends CrudRepository<Employee, Integer>  {

**Custom Methods**
   public List<Employee> findByName(String name);	
   public List<Employee> findByAge(int age);

**Custom Query**
  @Query(value = "SELECT e FROM Employee e ORDER BY name")
   public List<Employee> findAllSortedByName();
}
```

**Create Service Class to Create Objects of Repository Class to be used by Controller Class**

```
@Service
public class EmployeeService {
   @Autowired
   EmployeeRepository repository;

   public Employee getEmployeeById(int id) {
      return repository.findById(id).get();
   }
   public List<Employee> getAllEmployees(){
      List<Employee> employees = new ArrayList<Employee>();
      repository.findAll().forEach(employee -> employees.add(employee));
      return employees;
   }
   public void saveOrUpdate(Employee employee) {
      repository.save(employee);
   }
   public void deleteEmployeeById(int id) {
      repository.deleteById(id);
   }
   
   #Custom Method
   public Employee getEmployeeByName(String name) {
      return repository.findByName(id).get();
   }
   
   #Custom Query
    public List<Employee> getEmployeeById() {
      return repository.findAllSortedByName.get();
   }
}
```
**Controller Class Doing DB Updates using Repo Objects**

```
@RestController
@RequestMapping(path = "/emp")
public class EmployeeController {
   @Autowired
   EmployeeService employeeService;

   @GetMapping("/employees")
   public List<Employee> getAllEmployees(){
      return employeeService.getAllEmployees();
   }
   @GetMapping("/employee/{id}")
   public Employee getEmployee(@PathVariable("id") int id) {
      return employeeService.getEmployeeById(id);
   }
   @DeleteMapping("/employee/{id}")
   public void deleteEmployee(@PathVariable("id") int id) {
      employeeService.deleteEmployeeById(id);
   }
   @PostMapping("/employee")
   public void addEmployee(@RequestBody Employee employee) {
      employeeService.saveOrUpdate(employee);   
   }
   @PutMapping("/employee")
   public void updateEmployee(@RequestBody Employee employee) {
      employeeService.saveOrUpdate(employee);
   }	
}
```

**CrudRepo default methods (No need to describe these methods inside EmplyeeRepo Interface)**
```
count(): long
delete(Employee entity): void
deleteAll():void
deleteAll(Iterable< extends Employee > entities):void
deleteAll(Iterable< extends Integer > ids):void
existsById(Integer id):boolean
findAll():Iterable< Employee >
findAllByIds(Iterable< Integer > ids):Iterable< Employee >
findById(Integer id):Optional< Employee >
save(Employee entity): Employee
saveAll(Iterable< Employee> entities): Iterable< Employee>
```
