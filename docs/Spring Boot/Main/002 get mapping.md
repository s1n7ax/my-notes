# Get Mapping

## Method 1

```java
@RestController
public class HelloWorld {

 @RequestMapping(method = RequestMethod.GET, path = "/hello-world")
 public String greet() {
  return "Hello World!";
 }
}
```

## Method 2

```java
@RestController
public class HelloWorld {

 @GetMapping("/hello-world")
 public String greet() {
  return "Hello World";
 }
}
```
