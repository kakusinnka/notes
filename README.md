# notes
## SpringBoot + URI + Base64
```
@RestController
public class TestController {
    
    @GetMapping("/{password}")
    public String test(@PathVariable("password") String password) {
        // Base64解码
        return new String(Base64.getDecoder().decode(password), StandardCharsets.UTF_8);
    }
}
```

