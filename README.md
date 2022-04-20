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

## Angular + SpringBoot + HTTP get Size limit
```
export class AppComponent implements OnInit {
  title = 'app';
  constructor(private http: HttpClient) { }
  ngOnInit() {
    let str = '';
    for (var i = 38; i <= 8000; i++) {
      str = str + '0';
    }
    this.http.get('http://localhost:8080/api/values?name=' + str, { responseType: 'text' }).subscribe(result => {
      console.log(result);
    }, error => console.error(error));
  }
}
```
```
@CrossOrigin
@RestController
public class TestController {

    @GetMapping("/api/values")
    public String get(@RequestParam(value = "name", required = false) String name) throws Exception {
        return "hello " + name;
    }
}
```
