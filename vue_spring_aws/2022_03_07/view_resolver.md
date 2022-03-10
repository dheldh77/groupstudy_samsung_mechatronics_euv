# “index” View Resolver ??

## View Posting 에서

---

`DispatcherServlet` 에게 뷰 정보를 전달하는 방법은 두 가지가 있다

1. View type Object
2. String type View name

### String type View name을 전달하는 경우

---

이름으로부터 실제로 사용할 뷰 객체를 결정해주는 **View** **Resolver**가 필요하다

**View** **Object**를 넘겨주는 것 보다, View 이름을 넘겨주어 **View** **Resolver**를 사용하는 것이 성능 면에서 유리하다. **View** **Resolver**는 보통 **View** **Object** 를 **캐싱**하기 때문이다. 

**View** **Resolver** (이하 VR)는 View 이름으로부터 사용할 **View** **Object**를 **Mapping** 해준다. View 이름으로부터 View Object를 Mapping하는 방식도 여러가지가 있는데 선택해서 사용한다. 특정 VR을 `Bean`으로 등록하지 않으면 `DispatcherServlet`은 기본 VR인 `InternalResourceViewResolver`를 사용한다. 가장 기본적으로 **JSP**를 View로 사용할 때 `InternalResourceViewResolver`를 사용한다.

---

클라이언트로부터의 요청을 받으면 `DispatcherServlet`에서 `HandlerMapping`을 통해 `Controller`로 위임 처리하게 되는데 위임 처리 받은 `Controller`는 비즈니스 로직을 처리 후 View Resolver를 통해 View로 데이터를 전달하게 해준다. `Controller`가 View Object를 직접 return 할 수도 있지만 성능 면에서 View Resolver를 사용해 **String** type의 View name을 `Controller`가 return 하는 것이 유리하다. **모델과 View를 넘기면서 `Controller`의 책임은 끝나게 된다.**

> String으로 return 할 경우
> 

```java
@RequestMapping("/hello")
public String hello(@RequestParam String name, Model model) throws Exception {
	model.addAttribute("name", name);
	return "hello";
}
```

Model은 Parameter로 맵을 가져와 넣어주고 return 값은 View 이름을 String 타입으로 선언하는 방식이다. 

[String이 아니라 View Object를 return 하는 방식이 궁금하다면?](https://m.blog.naver.com/todoskr/220856216311)
