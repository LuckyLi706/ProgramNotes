# SpringBoot

## 请求

### 注解

+ @RestController注解是@controller和@ResponseBody的合集，表示这个控制器

```java
@Controller
@ResponseBody
//以上两个注解等同于@RestController注解
@RequestMapping(path = "/test")   //给整个类设置个url路径
public class ControllerTest {

}
```

+ @RequestMapping注解是一个用来处理请求地址映射的注解，可以用在类和方法上
+ @RequestBody和@RequestParam注解
  - @RequestBody注解（可以用来解析json字符串（还可以解析xml）,并将字符串映射到对应的实体中，实体字段名和json中的键名要对应，post请求参数）
  - @RequestParam注解（即接收请求头参数，也就是在url中，格式为xxx?username=123&password=456，get请求参数）

+ @GetMapping和@PostMapping
  - @PostMapping：组合注解，是@RequestMapping(method = RequestMethod.PUT)的缩写
  - @GetMapping：组合注解，是@RequestMapping(method = RequestMethod.GET)的缩写

### GET请求

```java
    //该注解表示url映射（访问地址就是ip:port/index）
    @RequestMapping(path = "/index", method = RequestMethod.GET)
    public String test() {
        return "Hello,Spring Boot";
    }
```

```java
    //使用两个路径
    @RequestMapping(path = {"/hi", "/hello"}, method = RequestMethod.GET)
    @GetMapping(path = {"/hi", "/hello"})  //等同于以上注解
    public String test1() {
        return "Hello,Spring Boot";
    }
```

```java
    //请求携带参数
    @RequestMapping(path = "/hi/{id}", method = RequestMethod.GET)
    public String test2(@PathVariable("id") Integer id) {    //通过PathVariable注解来获取入参
        System.out.println(id);
        return "id:" + id;
    }
```

```java
    //获取gei请求携带的参数
    //形如地址：http://127.0.0.1:8081/test/value?id=100
    @RequestMapping(path = "/value", method = RequestMethod.GET)
    public String test3(@RequestParam("id") Integer id) {    //通过RequestParam注解来获取入参
        return "id:" + id;
    }
```

```java
    //get请求多个入参
    //形如地址：http://127.0.0.1:8081/test/login?userName=%22lijie%22&pass=%22123455%22
    @RequestMapping(path = "/login", method = RequestMethod.GET)
    public String test4(@RequestParam("userName") String name, @RequestParam("pass") String pass) {    //通过RequestParam注解来获取入参
        return "userName:" + name + "," + "pass:" + pass;
    }
```

### POST请求

```java
    //获取post请求的参数值
    @PostMapping(path = "/demo1")
    public void demo1(@RequestBody Map<String, String> person) {
        System.out.println(person.get("name"));
    }
```

```java
    //@RequestBody注解表示json数据,后面跟的对象实体（客户端请求的时候要在请求头指定content-type为application/json charset=utf-8）
    @RequestMapping(path = "/test", method = RequestMethod.POST)
    public String test(@RequestBody Data data) {
        return data.getType();
    }
```

