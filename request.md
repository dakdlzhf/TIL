

# :rocket:request 객체

* 브라우저에서 요청이 들어오면 request 객체와 response 객체가 함께 생성된다.

## :star:request.getParameter( )

* HTML 에 form 태그에 값을 입력하고 서버에 요청을하면  서버에 Requset 객체에 getParameter 를 통해 form 에 정의된 name 값에 접근할수 있다.



## :star:request.getParameterValue( )



* form 태그에 동일한 name 으로 여러개의 값이 전달되었을경우

  ```html
  <form action="경로" method="post">
  
  <input type="checkbox" name="pet" value="dog">강아지 
  <input type="checkbox" name="pet" value="cat">고양이
  <input type="checkbox" name="pet" value="tiger">호랑이 
  
  <input type="submit" value="전송">
  </form>
  ```



## :star: request.getParameterNames( )



* request 객체의 getParameterNames ( ) 는 name 들을 모두 선택할수있다.
  * 찾은 name 들을 String [] names = request.getParameterNames( ); 하여 배열에 넣고 반복문 을 사용할수 있다. 



## :star: request.getParameterMap( )

* request 객체의 getParameterMap( ) 은 key,value map 구조이다

```jsp
<%
Map paramap = request.getParameterMap();
	String[] paramName = (String[])paramMap.get("pet")  // key 를 찾아볼수있다.
for(String param : paramName){
	System.out.println("param: "+ param);
}
%>
```



## :star: request.getHeaderNames( )

* 브라우저가 서버에 요청할때의 header 에 들어있는 정보를 확인할수 있다.
  * Cookie , Host ,Connection ,Accept 등등..



*  name 들을 String [] names = request.getParameterNames( ); 하여 배열에 넣고 반복문 을 사용할수 있다. 



* :arrow_up: 위와같이 checkbox 를 이용 할경우는 스크립트릿 에서 배열로 받아서 처리할수 있다.

  ```jsp
  <%
  String[] pets = request.getParameterValues("pet");
  
  for(String pet : pets){
  	System.out.println("pet" + pet);
  }
  %>
  ```

  

String 타입 배열 pets 에 request 객체를통해 name 이 pet 인 데이터를 배열레 담아서 반목문으로 출력하고있다.



### :star:request 객체의 데이터 정보가 알수없는 글자로 깨저 나온다면 인코딩문제이다

* request.setCharacterEncoding("utf-8"); 설정을 해주면 request 객체의 데이터 정보가 한글화된다.



***

***



## :star2: response.sendRedirect( ) 활용

* 브라우저에서 요청을 받고  다른 위치로 이동시켜준다. (  응답할 데이터 가 없고,  다른위치로 이동시켜 줄때 주로 사용)
* sendRedirect ( )를 사용하면 개발자도구 ->network 에 Response Headers 부분에 Location : https://www.naver.com/ 라고나온다

```jsp
<%
	response.sendRedirect("https://www.naver.com");
%>
```

* response 객체는 응답할 데이터를 담고있는 그릇일뿐 실제 데이터를 내보내주는 ***out 이라는 객체를 통해 println 되는것이다***

```jsp
<%
(HttpServletRequest)pageContext.getOut().println( '브라우저로 내보내는 데이터 !' )
%>
```

### :star:HttpServletRequest :vs: HttpServletResponse  ? ?

**WAS가 웹브라우저 로부터 Servlet요청을 받으면** 

1. 요청을 받을 때 전달 받은 정보를 HttpServletRequest객체를 생성하여 저장
2. 웹브라우져에게 응답을 돌려줄 HttpServletResponse객체를 생성(빈 객체)
3. 생성된 HttpServletRequest(정보가 저장된)와 HttpServletResponse(비어 있는)를 Servlet에게 전달

**HttpServletRequest**

1. Http프로토콜의 request 정보를 서블릿에게 전달하기 위한 목적으로 사용
2. Header정보, Parameter, Cookie, URI, URL 등의 정보를 읽어들이는 메소드를 가진 클래스
3. Body의 Stream을 읽어들이는 메소드를 가지고 있음

**HttpServletResponse**

1. Servlet은 HttpServletResponse객체에 Content Type, 응답코드, 응답 메시지등을 담아서 전송함

   

## :heavy_exclamation_mark: HttpServeketRequest 인터페이스는 내부적으로 ServletRequest 인터페이스를 상속받고 있다.

* 따라서 request 객체의 메소드를 사용하는것은 SevletRequest 혹은 HttpServletRequest 인터페이스의 멤버이다.

  * 그중 몇가지 메소드들을 확인해보면

    1. **getServerPort()**

    2. **getLocalAddr()**

    3. **getMethod()**

    4. **getHeaderNames()**

    5. **getPathInfo()**

    6. **getQueryString()**

    7. **getRemoteUser()**

    8. **getRequestURL()**

    9. **getRequestURI()**

    10. **getServletPath()**

        .......등 이있다.

***


```jsp
<%
       String protocol = request.getProtocol();
       String serverName = request.getServerName();
        int serverPort = request.getServerPort();
        String remoteAddr = request.getRemoteAddr();
        String remoteHost = request.getRemoteHost();
        String method = request.getMethod();
        StringBuffer requestURL = request.getRequestURL();
        String requestURI = request.getRequestURI();
        String useBrowser = request.getHeader("User-Agent");
        String fileType = request.getHeader("Accept");
%>

```

```jsp
<body>
프로토콜 : <%=protocol%>
서버의 이름 : <%=serverName%>
서버의 포트 번호 :<%=serverPort%>
사용자 컴퓨터의 주소 : <%=remoteAddr%>
사용자 컴퓨터의 이름 : <%=remoteHost%>
사용 method : <%=method%>
요청 경로(URL) : <%=requestURL%>
요청 경로(URI) : <%=requestURI%>
현재 사용하는 브라우저 : <%=useBrowser%>
브라우저가 지원하는 file의 type : <%=fileType%>
</body>
```



