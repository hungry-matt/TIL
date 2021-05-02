# Spring Model
- @Controller의 메서드는 Model이라는 타입의 객체를 파라미터로 받음
- JSP Servlet으로 애플리케이션 구현시 request나 session 내장객체에 정보를 담아 jsp에 넘겨주는 반면 Spring에서는 Model을 통해 전달
- `request.setAttribute()` 와 비슷한 역할

###Servlet
```java
request.setAttribute("time", new java.util.Date());
ReqeustDispatcher dispatcher = request.getRequestDispatcher("url");
dispatcher.forward(request, response);
```

###Spring
```java
public String home(Model model) {
    model.addAttribute("time", new java.util.Date());
    return "home";
}
```

- 직접 Model을 생성 할 필요가 없으며 파라미터 선언만 하면 스프링에서 자동으로 생성
- 스프링 MVC Controller는 기본적으로 `Java Beans` 규칙에 맞는 객체는 자동으로 view로 전달 해줌
- 전달할 때는 클래스명의 앞글자를 소문자로 처리하여 전달

>Java Beans의 규칙<br>
>1.생성자가 없거나 빈 생성자<br>
>2.getter/setter를 가진 클래스의 객체

- 그러나 기본자료형은 파라미터로 선언되었더라도 화면에 자동 전달 되지 않음

### 전달되지 않는 경우
```java
public String ex04(int page) {
    return "ex04";
}
```

```jsp
<h2>page : ${page}</h2>
```

### 그러면 어떻게 view에 전달할까?
1) 파라미터에 Model 선언후 addAttribute()로 전달
2) @ModelAttribute 어노테이션 사용

```java
public String ex04(@ModelAttribute("mypage") int page) {
    return "ex04";
}
```

```jsp
<h2>page : ${mypage}</h2>
```

## Controller 메서드의 리턴타입
- String: jsp파일의 이름을 나타탬
- void: 호출하는 URL과 동일한 이름의 jsp를 나타냄
- VO, DTO: 주로 json타입의 데이터를 만들어서 반환하는 용도
- ResponseEntity: response할때 HTTP 헤더 정보와 내용을 가공
- Model, ModelAndView: Model로 데이터를 반환하거나 화면까지 지정
- HttpHeaders: 응답에 내용없이 HTTP 헤더 메세지만 전달하는 용도

자주 사용되는 void, String은 servlet-context.xml의 ViewResolver 설정과 맞물려 작동

```xml
<!-- Resolves views selected for rendering by @Controllers to .jsp resources in the /WEB-INF/views directory -->
<beans:bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
	<beans:property name="prefix" value="/WEB-INF/views/" />
	<beans:property name="suffix" value=".jsp" />
</beans:bean>
```

- String은 상황에 따라 다른 화면을 보여줄 필요가 있을 경우 유용 (if~else 처리)
- String 리턴타입에서 return문에 특별한 키워드를 붙일 수 있음
    - redirect
    - forward (생략시 기본)