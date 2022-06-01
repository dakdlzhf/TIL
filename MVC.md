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

***


## :star_of_david:  JSP 에서 MVC 패턴을 구현하는 방법



### :star: **서비스 하는 기능마다 서블릿을 정의하고 등록한다**

:rainbow: MVC 패턴 적용 이전구현방식 ( 기능마다 서블릿을 구현하고 mapping 해야했다.)

* 요청마다 서블릿을 만들고 매핑되는 URL 패턴을 설정한다.
* URL요청 -> 서블릿에서 처리-> 직접응답
* web.xml 서블릿 등록(Servlet 3.0 부터 어노테이션으로도 서블릿 등록,mapping 을 한줄로 할수있다)



:rainbow:  Front Controller 패턴이고도불린다.  MVC 패턴이다 

* 모든 요청을 받는 서블릿을 정의하고 등록한다

* URL 매핑에 / 를 이용하여 하나의 서블릿이 모든요청을 받게한다.
* 요청 URL or Parameter 로 전달된 명령을 이용하여 처리할 비즈니스 로직을 Model 부분( DAO ,Service , Action , Handler 라고 불리우는 것들) 선택한다 
* FrontController 에서 요청을 분석하고 비즈니스 로직 처리 수 브라우저에 응답 또는 적절한 View 를 선택하여 응답하게 한다.



***나중에 프레임워크 를 사용하게되면 Spring MVC  에는 편한구조를 기본적으로 제공해주기때문에그전까지는 MVC 패턴구조를 직접 만들어서 사용해야한다.***






