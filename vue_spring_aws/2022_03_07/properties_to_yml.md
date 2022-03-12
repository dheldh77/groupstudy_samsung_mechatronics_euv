# [application.properties](http://application.properties) → .yml

### **[스프링부트 (11)] SpringBoot YAML 적용하기(properties vs yaml)**

안녕하세요. 갓대희 입니다. 이번 포스팅은 **[ Spring Boot Properties 대신 YAML적용하기 ]** 입니다. : )

![https://blog.kakaocdn.net/dn/eArVYH/btqCrOaSNlP/FtnlW7Ej4BSQvPWSqRV8qk/img.png](https://blog.kakaocdn.net/dn/eArVYH/btqCrOaSNlP/FtnlW7Ej4BSQvPWSqRV8qk/img.png)

> 1. YAML이란?
> 

### **▶ YAML (YML Ain't Markup Language)**

- 자세한 내용은 위키 참조(위키를 참조하여 간략히 정리 하였다.) : [https://ko.wikipedia.org/wiki/YAML](https://ko.wikipedia.org/wiki/YAML)

- XML, C, 파이썬, 펄, RFC2822에서 정의된 e-mail 양식에서 개념을 얻어 만들어진 '사람이 쉽게 읽을 수 있는' 데이터 직렬화 양식. - YAML은 모든 데이터를 리스트, 해쉬, 스칼라 데이터의 조합으로 적절히 표현할 수 있다는 믿음을 가지고 만들어졌다.문법은 상대적으로 이해하기 쉽고, 가독성이 좋도록 디자인되었으며, 고급 컴퓨터 언어에 적합하다.또한 들여쓰기 및 XML의 특수기호를 사용하기 때문에, XML과 거의 비슷 핟. - JSON은 yaml의 일종이다.

### **▶ 사용방법 및 Properties와 비교시 이점**

> 1. 가독성이 좋다.
> 

계층구조로 표현하여 가독성이 좋다. 또한 불필요한 소스의 중복도 제거 할 수 있다.들여쓰기, 띄어쓰기로 구분하여 보기 편하다.

ex) properties

```xml
spring.datasource.driverClassName=net.sf.log4jdbc.sql.jdbcapi.DriverSpy
spring.datasource.url=jdbc:log4jdbc:mariadb://localhost:3306/test?characterEncoding=UTF-8&serverTimezone=UTC
spring.datasource.hikari.username=root
spring.datasource.hikari.password=qlalfqjsgh
spring.datasource.hikari.maximum-pool-size=10
```

ex) yaml

```yaml
spring:
  datasource:
    driverClassName: net.sf.log4jdbc.sql.jdbcapi.DriverSpy
    url: jdbc:log4jdbc:mariadb://localhost:3306/test?characterEncoding=UTF-8&serverTimezone=UTC
    hikari:
      username: root
      password: qlalfqjsgh
      maximum-pool-size: 10
```

> 2. 리스트 표현
> 

- 여러 줄에 쓸 때에는 하이픈(-)으로 시작하는 한 줄에 하나의 요소를 표현한다. - 한 줄에 모아 쓸 때에는 대괄호([])를 이용하며 쉼표로 각 요소를 구분한다.

ex) properties

```xml
my.servers[0]=dev.example.com
my.servers[1]=another.example.com
```

ex) yaml(1) - 여러줄 표현

```yaml
my:
servers:
-dev.example.com-another.example.com
```

ex) yaml(2) - 한줄 표현

```yaml
my:
  servers: [dev.example.com, another.example.com]
```

> 3. 주석
> 

- 주석은 #으로 표시하며, 한 줄이 끝날 때까지 유효하다.

ex)

```yaml
spring:
  datasource:#db 접속 정보driverClassName: net.sf.log4jdbc.sql.jdbcapi.DriverSpy
    url: jdbc:log4jdbc:mariadb://localhost:3306/test?characterEncoding=UTF-8&serverTimezone=UTC
    hikari:#hikari 설정 정보username: root
      password: qlalfqjsgh
      maximum-pool-size: 10
```

> 4. SpringBoot Profile적용이 용이하다. (with "--- " 구분자)
> 

- 한 파일 내에서 여러 파일을 사용하는 것처럼 분리가 가능하다.

- application.yml 파일 하나로 여러개의 yml을 생성 한것과 같이 처리 가능

**1) properties**

- application-{profile}.properties 형식으로 다음과 여러개의 파일을 생성하여 사용했다.

ex) application-{profile}.propertiesapplication-local.propertiesapplication-dev.propertiesapplication-prod.properties

![https://blog.kakaocdn.net/dn/dbYkp2/btqCoQHxO4a/Kk77Hef35sxRw3sBPNlfz0/img.png](https://blog.kakaocdn.net/dn/dbYkp2/btqCoQHxO4a/Kk77Hef35sxRw3sBPNlfz0/img.png)

출처:

[https://goddaehee.tistory.com/213](https://goddaehee.tistory.com/213)

[갓대희의 작은공간

> 참고 준혁 yml
```yaml
spring:
  jpa:
    show_sql: true
    properties:
      hibernate:
        - dialect: org.hibernate.dialect.MySQL57Dialect
        - dialect:
            storage_engine: innodb
  datasource:
    hikari:
      jdbc-url: jdbc:h2:mem:testdb;MODE=MYSQL
      username: sa
  h2:
    console:
      enabled: true
# yaml 파일은 / 를 그대로 쓰면 Parsing Error가 발생한다. 따라서 "", ''로 감싸줘야 한다.
```
