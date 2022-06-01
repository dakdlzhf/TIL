## JSP 에서 MVC 패턴 흐름



:rocket: **MVC 패턴의 흐름을 알아보겠다.**

* 사용자 인터페이스로부터 비즈니스 로직을 분리할수 있는 장점이있다 ( 결합도를 낮춘다 )
  * 애플리케이션의 시각적 요소가 그이면에서 실행되는 비즈니스 로직을 <u>서로 영향 없이 고칠수있는</u> 애플리케이션을 만들수있다.
* `Model` : 애플리케이션의 정보 ( 데이터 ) 를 나타낸다.
* `View` : 텍스트 , 체크박스 , 항목등등 사용자 인터페이스 요소를 나타낸다.
* `Controller` : 데이터와 비즈니스 로직 사이의 상호동작을 관리한다.

***





:star:**`Model`**

:one: Controller의 요청을 받는다.

:two: 비즈니스 로직 처리 (외부자원 사용 DB) 를 한다

:three: 처리한 결과를 Controller 에 return 한다.



:star:**`View`**

:one: Controller 에 선택받은 JSP 파일을 Tomcat 이 해석하여 .java 코드로 생성 (자바 서블릿)

:two: java 코드 파일을 컴파일하여 .class 파일로 변환후 메모리에 올리며 서블릿 객체를 생성

:three: request or session 에 담겨있는 데이터를 표현식 <%= %> 에 세팅하여 response 데이터를 생성 (     	HTML/CSS/JS/XML/JSON 등)



:star:**`Controller`**

:one: Http 요청을 받는다

:two: 요청 분석

:three: 비즈니스로직처리 ( Model 사용)

:four: 결과 데이터를 필요하다면 request 객체 or session 객체에  저장한다.

:five: 알맞는 View 를 선택하여 forward or redirect 한다.







