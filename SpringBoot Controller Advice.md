# SpringBoot Controller Advice and Exception Handler

**Create Custom Exception Classes**

1. Custom Exception Class A

```
package com.tutorialspoint.demo.exception;
public class ProductNotfoundException extends RuntimeException {
   private static final long serialVersionUID = 1L;
}
The Controller Advice class to handle the exception globally is given below. We can define any Exception Handler methods in this class file.
```

2. Custom Exception Class B

```
package com.tutorialspoint.demo.exception;
public class ServiceNotfoundException extends RuntimeException {
   private static final long serialVersionUID = 1L;
}
The Controller Advice class to handle the exception globally is given below. We can define any Exception Handler methods in this class file.
```

**Create a Single ControllerAdvice Class and Put All Custom Exceptions in it**

```
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;

@ControllerAdvice
public class ProductExceptionController {
   @ExceptionHandler(value = ProductNotfoundException.class)
   public ResponseEntity<Object> exception(ProductNotfoundException exception) {
      return new ResponseEntity<>("Product not found", HttpStatus.NOT_FOUND);
   }
   
   @ExceptionHandler(value = ServiceNotfoundException.class)
   public ResponseEntity<Object> exception(ServiceNotfoundException exception) {
      return new ResponseEntity<>("Service not found", HttpStatus.NOT_FOUND);
   }
}

```
The Product Service API controller file is given below to update the Product. If the Product is not found, then it throws the ProductNotFoundException class.


**Controller Class Throwing custom exception**

Import all the custom exceptions into contolller class and throw the exception and the controller advice class will take care of handling of proper exception
```
import com.tutorialspoint.demo.exception.ProductNotfoundException;
import com.tutorialspoint.demo.exception.ServiceNotfoundException;
import com.tutorialspoint.demo.model.Product;

@RestController
public class ProductServiceController {
   private static Map<String, Product> productRepo = new HashMap<>();
   static {
      Product honey = new Product();
      honey.setId("1");
      honey.setName("Honey");
      productRepo.put(honey.getId(), honey);
      
      Product almond = new Product();
      almond.setId("2");
      almond.setName("Almond");
      productRepo.put(almond.getId(), almond);
   }
   
   @RequestMapping(value = "/products/{id}", method = RequestMethod.PUT)
   public ResponseEntity<Object> updateProduct(@PathVariable("id") String id, @RequestBody Product product) { 
      if(!productRepo.containsKey(id))throw new ProductNotfoundException();
      productRepo.remove(id);
      product.setId(id);
      productRepo.put(id, product);
      return new ResponseEntity<>("Product is updated successfully", HttpStatus.OK);
   }
}
```
