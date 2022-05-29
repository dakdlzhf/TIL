# :rocket: Servlet 

## Servlet ?

* servlet 은 HttpServlet 을 상속하여 만들어진것들을 Serveler 이라고 부른다.
* HttpServlet
  * 서블릿을 만들기 위해서 반드시 상속해야 할 필수 클래스
  * Servlet 인터페이스 >  GenericServlet 추상클래스 > HttpServlet 상속구조



  * 웹 클라이언트의 요청을 처리할 수 있는 클래스 (Java)

* JSP 와 Servlet 의 차이점? 

  * 브라우저 입장에서 봤을때는 JSP 파일을 요청 하는것과
  * 서블릿을 만들어서 브라우저가 서블릿으로 직접 요청을 할수있게 만들어놓는것

* 여기서 간단하게 모델 1 과 모델 2 라고 불리는 차이점은 ?

  * 브라우저의 요청이 JSP 파일이고 , 브라우저의 응답해주는 파일도 JSP  로 동일할때 모델1
  * 브라우저의 요청은 Servlet이 받아서 처리하고 처리된 결과를 JSP 파일이 응답할때 모델2 ( MVC 패턴 )
    * Model , View , Controller 

*  Java Servlet  즉 Java 파일을 만든후  Web.xml 에 매핑 설정까지 해주어야한다.

  * 등록 , 경로매핑  을해줘야 기본적인 요청과 응답을 할수있다

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" version="4.0">
      <display-name>servlet0</display-name>
    	
    	<!-- 서블릿 등록 -->
    	<servlet>
    		<servlet-name>loginServlet</servlet-name>
    		<servlet-class>servlet0.LoginServlet</servlet-class> 
    	</servlet>
    	<!-- 서블릿 경로 매핑 (브라우저에서 요청할경로)-->
      	<servlet-mapping>
      		<servlet-name>loginServlet</servlet-name>
      		<url-pattern>/login00</url-pattern>
      	</servlet-mapping>
      
    </web-app>
    ```

* xml 파일을 보면 url-pattern 으로 경로를 매핑했는데 /login00 으로 브라우저가 요청하게되면 loginServlet 이라는 서블릿이 등록되있는 class --> servlet0.LoginServlet 임으로 즉 LoginServlet 이 대응 한다는 것이다. 

## Servlet Life cycle







Servlet 에 있는 메소드 들은 모두 콜백함수이다


:heavy_check_mark: Servlet 과 JSP 파일을 목적에 맞게 구분하여 사용한다면 코드의 확장이 용이하고 유지보수면에서도 편할것이다.



:star: ***HttpServlet 에서 제공되는 주요 메소드***

| 메소드                                 | 설명                                                         |
| -------------------------------------- | ------------------------------------------------------------ |
| void init ( )                          | 서블릿의 객체가 생성 될때 최초 한번 호출되는 메소드          |
| void destroy ( )                       | 서블릿의 객체가 메모리에서 사라질때 호출되는 메소드 ( 변경된요청 이올때도 작동된다) |
| void         Service(request,response) | 서블릿의 요청이 있을때 호출되는 메소드                       |
| void doGet(request,response)           | html 에서 form 의 메소드가 get일 때 호출되는 메소드          |
| void doPost(request,response)          | html 에서 form 의 메소드가 post 일 때 호출되는 메소드        |





* HttpServletRequest
  * 클라이언트가 데이터를 입력하거나 클라이언트의 정보에 대한 요청 값을 가지고있다.

| 메소드                            | 설명                                                         |
| --------------------------------- | ------------------------------------------------------------ |
| String getParameter(name)         | name 에 할당된 값을 반환하며 지정된 파라미터 값이 없으면 null 값을 반환한다 |
| String[] getParmeterValuese(name) | name 의 모든 값을 String 배열로 반환한다                     |
| Enumeration getParameterNamese()  | 요청에 사용된 모든 파라미터 이름을 java.util.Enumeration 타입을반환한다 |
| void setCharacterEncoding(env)    | post 방식으로 요청된 문자열의 character encoding 을 설정한다 |

:star:***HttpServletRequest 에서 제공되는 주요 메소드***

