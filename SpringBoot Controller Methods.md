# springboot-controller-sample-methods

```

import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping(path="/begin")
public class AppController {
@CrossOrigin(origins = "http://localhost:4200")

**Simple Get Method**
//@GetMapping(path="/getExample", consumes = ""text/plain")
@GetMapping(path="/getExample", produces = "application/json")
public BindModel getExample() {
	BindModel test = new BindModel();
	test.setTesting("Hello");
	return test;
}

**Path Param Method**
@GetMapping(path="/getPathParamExample/{id}", produces = "application/json")
public BindModel getPathParamExample(@PathVariable String id) {
	BindModel test = new BindModel();
	test.setTesting(id);
	return test;
}

**Query Param Method**
@GetMapping(path="/getQueryParamExample", produces = "application/json")
public BindModel getQueryParamExample(@RequestParam(required = false) String id) {
	BindModel test = new BindModel();
	test.setTesting(id);
	return test;
}

**Post Body Method**
@PostMapping(path="/users")  
public BindModel createUser(@RequestBody BindModel testing)  
{  
	BindModel t1 = testing;
  return t1;    
}  
// request body to hit on post man
// Body = {"testing":"Hello"}
}
```
