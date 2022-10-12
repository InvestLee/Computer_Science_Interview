# 스프링

---
## 스프링

- 자바 오픈소스 애플리케이션 프레임워크 중 하나

- 스프링의 기본철학은 특정 기술에 종속되지 않고 객체를 관리할 수 있는 프레임워크를 제공하는 것

- 컨테이너로 자바 객체를 관리하면서 DI와 IOC를 통해 결합도를 낮추게 됨

---
## 의존성 주입(DI, Dependency Injection)

- 객체간의 의존관계를 미리 설정해두면 스프링 컨테이너가 의존관계를 자동으로 연결

- 직접 의존하는 객체를 생성하거나 검색해서 가져올 필요가 없어서 결합도가 낮아지는 장점이 있음

- Field Injection(필드 주입)

  - 생성자 or Setter가 없으므로 수동 의존성 주입이 필요한 테스트 불가능
  
  - 의존성이 프레임워크에 강하게 종속되는 문제점 발생

```
@Controller
public class MemberController {
	
	@Autowired
	private MemberService memberService;
}
```
   
- Setter Injection(수정자 주입)
 
  - 속성에 final를 작성할 수 없으므로 의존성 불변을 보장할 수 없음 

  - 런타임 중 setter를 다시 호출하여 이미 주입된 의존성 변경이 가능

  - 주로 런타임 중 의존성 수정하거나 선택적 의존성(의존성 주입이 반드시 필수가 아닌 것을 의미)에 사용   
```
@Controller
public class MemberController {
	private  MemberService memberService;
	
	@Autowired
	public void setMemberController(MemberService memberService) {
		this.memberService = memberService;
	}
}
```
  
- Construction Injection(생성자 주입)

  - 객체의 최초 생성 시점에 스프링이 모든 의존성을 주입

  - 생성자 호출 시 final에 의해서 의존성 주입이 최초 1회만 이루어짐

  - 생성자 주입은 의존관계 불변이므로 NullPointerException 방지(다른 방식은 직접 객체를 생성하여 방지)
```
@Controller
public class MemberController {
	private final MemberService memberService;
	
	@Autowired
	public MemberController(MemberService memberService) {
		this.memberService = memberService;
	}
}
```



---
## 제어의 역전(IoC, Inversion of Control)

- 제어권이 사용자에게 있지 않고, 프레임워크에 있어서 필요에 따라서 사용자의 코드를 호출하게 됨. 

- 스프링에서는 인스턴스의 생성부터 소멸까지 개발자가 아닌 컨테이너에서 대신 관리

---
## ORM(Object Relational Mapping)

- 관계형 데이터베이스를 객체 지향 언어로 변환해주는 기술

- 비즈니스 코드가 DB 테이블에 바로 접근하게 도와줌

---
## JPA(Java Persisitence API)

- ORM을 위해서 자바에서 제공하는 API

- 자바 객체와 DB테이블을 매핑

- 구현체로는 하이버네이트가 있음

---
## ORM, JPA, 하이버네이트 장단점

- 비즈니스 로직에 집중하고 객체 중심의 개발을 할 수 있게 됨

- 메소드를 호출하는 것만으로 쿼리를 수행해서 생산성이 향상되고 유지보수 비용이 줄어듬

- 특정 DB에 의존하지 않게 됨

- 직접 SQL을 호출하는 것보다는 조금 느리고 복잡한 쿼리 같은 것은 메소드로 처리하기 힘듬

