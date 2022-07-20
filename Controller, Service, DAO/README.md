## Controller
> 사용자의 요청을 분류하여 service에 넘긴다. 
> Request URL에 맞는 Controller를 수신받는다.

ex)
<pre>
@Controller
public class Controllerprac {
    @GetMapping("/home") //home으로 Get요청이들어오면
    public String homepage(){
        return "home.html"; //home.html생성
    }
}
</pre>

@RestController도 있는데 주용도는 JSON/XML형태로 객체 데이터 반환을 목적으로 합니다.  

ex)
<pre>
@RestController // JSON으로 데이터를 주고받음을 선언합니다.
public class ProductRestController {

    private final ProductService productService;
    private final ProductRepository productRepository;

    // 등록된 전체 상품 목록 조회
    @GetMapping("/api/products")
    public List<Product> getProducts() {
        return productRepository.findAll();
    }
}
</pre>

## Service와 ServiceImpl
- Service = interface
- ServiceImpl = class

> Service는 알맞은 정보를 가공하여 Controller에게 데이터를 넘긴다. 
> Service가 비즈니스 로직을 수행하고 데이터베이스에 접근하는 DAO를 이용해서 결과값을 받아 옵니다.  

ex)
<pre>
@Controller
public class UserController {

	@Autowired
	private UserSerivce userService;
    
	@RequestMapping(value="/getUsers")
	public String getUsers(Model model) {
		model.addAttribute("users",userService.getUsers());
		return "user";
	}
}
</pre>

- @Service 라는 어노테이션으로 선언한 Class 를 사용하기위해서 <b>@Autowired 라는 어노테이션</b>을 사용해서 <b>해당 서비스를 스프링에 등록시켜줍니다.</b>  
- 잠.깐!!! 짚고 넘어가야할게 있죠?? 분명 @Service 로 등록한 Class 는 UserServiceImpl 이라는 클래스고 그럼 @Autowired 라는 어노테이션으로 UserServiceImpl 이라는 
객체를 묶어줘야하지 않나...?? 라는 생각이 드실텐데요
UserServiceImpl 은 UserService 라는 인터페이스의 구현체이기 때문에 스프링은 @Autowired 를 UserService 라는 인터페이스를 상속한 Class 를 자동으로 등록시켜줍니다.
출처: https://onlyformylittlefox.tistory.com/13 [Trace - 리다양의 개발 세상:티스토리]


## DAO, DTO, VO

1. DAO
> Data Access Object 의 약자로 데이터베이스의 data에 접근하기 위한 객체입니다.

2. DTO
> DTO(Data Transfer Object) 는 계층간(Controller, View, Business Layer, Persistent Layer 등) 데이터 교환을 위한 자바빈즈를 의미합니다. 
> getter와 setter 존재. 

3. VO
> VO(Value Object) 값 오브젝트로써 값을 위해 쓰입니다.
> getter기능만이 존재하여 불변의 성격을 가진다. 
