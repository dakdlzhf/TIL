# :rocket: Servlet 

## Servlet ?

* servlet 은 HttpServlet 을 상속하여 만들어진것들을 Serveler 이라고 부른다.
* HttpServlet
  * 서블릿을 만들기 위해서 반드시 상속해야 할 필수 클래스
  * Servlet 인터페이스 >  GenericServlet 추상클래스 > HttpServlet 상속구조



  * 웹 클라이언트의 요청을 처리할 수 있는 클래스 (Java)

## Servlet


![servletimage](https://user-images.githubusercontent.com/80139780/170849376-8fed39b1-3157-43bf-9253-effd9a2c8e96.png)

1. Web Server는 HTTP request를 Web Container(Servlet Container)에게 위임한다.
   1. web.xml 설정에서 어떤 URL과 매핑되어 있는지 확인
   2. 클라이언트(browser)의 요청 URL을 보고 적절한 Servlet을 실행

2. Web Container는 service() 메서드를 호출하기 전에 Servlet 객체를 메모리에 올린다.
   1. Web Container는 적절한 Servlet 파일을 컴파일(.class 파일 생성)한다.
   2. .class 파일을 메모리에 올려 Servlet 객체를 만든다.

3. 메모리에 로드될 때 Servlet 객체를 초기화하는 init() 메서드가 실행된다.
   1. Web Container는 Request가 올 때 마다 thread를 생성하여 처리한다.
   2. 각 thread는 Servlet의 단일 객체에 대한 service() 메서드를 실행한다.


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

![servletlifecycle](https://user-images.githubusercontent.com/80139780/170849561-088f4f31-91b1-4a28-ac38-4b368358cc54.png)

클라이언트의 요청이 들어오면 WAS는 해당 요청에 맞는 Servlet이 메모리에 있는지 확인한다.

 \- 만약 메모리에 없다면 해당 Servlet Clas를 메모리에 올린 후 (Servlet 객체 생성) init 메서드 실행

  -> 이후 service 메서드를 실행

 \- 만약 메모리에 있다면 바로 service 메서드 실행

 

**`init()`**

 \- 한 번만 수행됨

 \- 클라이언트(browser)의 요청에 따라 적절한 Servlet이 생성되고 이 Servlet이 메모리에 로드될 때 init() 메서드가 호출

 \- 역할 : Servlet 객체를 초기화

 

**`service(request, response)`**

 \- 응답에 대한 모든 내용은 service() 메서드에 구현해야 함

 \- Servlet이 수신한 모든 request에 대해 service() 메서드가 호출됨

  \- HttpServlet을 상속받은 Servlet 클래스 (이하 하위 클래스) 에서 service() 메서드를 오버라이드 하지 않았다면,

   그 부모인 HttpServlet의 service()가 호출됨  

  \- service() 메서드는 request의 type(HTTP Method : GET, POST, PUT, DELETE 등)에 따라 적절한 메서드

   (doGet, doPost, doPut, doDelete 등)를 호출함

  \- 즉, 하위 클래스에서 doGet, doPost 등의 메서드를 오버라이드 해두면 HttpServlet의 service() 메서드가 요청에

   맞는 메서드(하위 클래스에서 오버라이드한 메서드)를 알아서 호출할 수 있게 되는 것

 \- 메서드가 return 하면 해당 thread는 제거됨

 

**`destory()`**

 \- 한 번만 수행됨

 \- Web Application이 갱신되거나 WAS가 종료될 때 호출됨

 \- 역할 : Servlet 객체를 메모리에서 제거

 

**HttpServletRequest request 객체**

 \- 사용자가 HTML Form에 입력한 내용(username과 password)을 request 객체에서 받아온다.
  즉, HTTP 프로토콜의 Request 정보를 Servlet에게 전달
 \- 헤더 정보, 파라미터, 쿠키, URI, URL, Body의 Stream 등을 읽어 들이는 메서드가 있다.
 \- getHeader(“원하는 헤더 이름”) : 이 메서드를 통해 원하는 헤더 정보를 확인할 수 있다.
 \- getParameter() : 이 메서드를 호출하여 form parameter 값을 가져온다.
  이런 parameter 값은 URL 또는 form의 input tag를 통해서 넘어올 수 있다.
 \- getParameterValues()
  form parameter가 두 번 이상 나타나고 여러 개의 값을 반환할 때 이 메서드를 호출한다. (Ex. checkbox)



**HttpServletResponse response 객체**
 \- 인자의 내용에 맞게 동적인 HTML 코드를 생성하여 response 객체에 담아 반환한다.
 \- getWriter() 메서드를 호출하여 PrintWriter 객체을 가져온 후 해당 객체에서 print, println 메서드를 실행한다.
 \- 즉, form data를 처리한 결과를 Web Page에 생성(view 생성)하여 반환한다.



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

