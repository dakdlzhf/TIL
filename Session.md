## :star: Session ?

`session` 은 기본객체이다 ( 브라우저를 식별하기 위해서 이미 자동으로 만들어지고있다.)

### 세션의 기본적인 동작에대한 설명을 하겠습니다.



* jsp 파일에 directive (지시자 <%@ page language="java" contentType="text/html charset=UTF-8 ;"%>) 에 표기되어 있지는 않지만 session="true" 라는 값이 기본값으로 되어있다.

* 크롬과 엣지 제각각 다르게 sessionInfo.jsp 요청을 하게된다면 각 브라우저의 JSESSIONID 는 다를것이다 
  * 클라이언트가 브라우저에서 요청을 하게되면 요청정보 안에 들어있는  Request Header 에 Cookie 에들어있는 `JSESSIONID `가있는지 서버에서 확인하고 session 값이 있다면 그값과 동일한 session 객체가 있는지  브라우저를 식별하게된다. 



* :heavy_exclamation_mark: ***만약 만료되거나 없는 세션이라면 서버에서는 새로 세션을 생성해서 쿠키에 응답해줄거다.***
* JSESSIONID 값이없는 최초의 브라우저에서 요청이 서버에들어오면  JSESSIONID 가 없는것을 확인후 session 값이 없는 브라우저에 기본적으로 자동생성하여  브라우저에게 Response Header JSESSIONID 를 저장하라고 알려준다 이때까지는 현재 브라우저의 Request Header 에 Cookie에는 JSESSIONID 의값이 들어있지않다. 하지만 개발자도구 application 에 쿠키를 확인하면 JSESSIONID 의 값이 저장되있다. :heavy_exclamation_mark: <u>이말은 최초브라우저에서의 요청시 서버에서 Response객체에 Header 에 JSESSIONID 을 저장하라고 알려는줬지만~</u>!   `현재 Request 객체에 Header Cookie 에는 JSESSIONID는 없는거다`
* JSESSIONID 값을 브라우저 쿠키에 저장한 브라우저에서  재요청을 한경우에는 Request Header 에 Cookie 를 살펴보면 JSESSIONID 값을 확인할수있다.  `최초요청시에만 Request Header Cookie 에 JSESSIONID 가없지 재요청시에는 요청시마다Requqest Header Cookie 에 JSESSIONID 를 포함시켜  보낸다` 



### Session 을 생성하여 생성된 Session 아이디와 생성된 시점의 시간과  마지막으로 접근한 시간을 보는 코드를 만들어보았다.

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ page session="true" %>
<%@ page import="java.util.Date" %>
<%@ page import="java.text.SimpleDateFormat" %>
<%
	Date CreatonTime = new Date();
	SimpleDateFormat formatter = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
	
	CreatonTime.setTime(session.getCreationTime()); //브라우저가 최초로 서버에 요청하여 session 이 생성된 시간
	
	Date lastAccessedTime = new Date();
	lastAccessedTime.setTime(session.getLastAccessedTime()); //마지막으로 해당브라우저에 접근했던시간
%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
세션:ID <%= session.getId() %><br>
최초세션 생성시간 <%= formatter.format(CreatonTime) %><br>
마지막세션 접근시간 <%= formatter.format(lastAccessedTime) %><br>

</body>
</html>
```



:star: ***세션의 유효시간을 설정해보자***	

* `session.setMaxInactiveInterval( )`

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<%@ page session="true" %>
<%@ page import="java.util.Date" %>
<%@ page import="java.text.SimpleDateFormat" %>
<%
	// 세션의 유효시간을 10초로 설정후 10초가지난 후에 새로고침을하면 session의 아이디가 재생성된걸 확인할수 있다.
	session.setMaxInactiveInterval(10);	
	
	Date CreatonTime = new Date();
	SimpleDateFormat formatter = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
	
	CreatonTime.setTime(session.getCreationTime()); 
	
	Date lastAccessedTime = new Date();
	lastAccessedTime.setTime(session.getLastAccessedTime()); 
%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
<title>Insert title here</title>
</head>
<body>
세션:ID <%= session.getId() %><br>
최초세션 생성시간 <%= formatter.format(CreatonTime) %><br>
마지막세션 접근시간 <%= formatter.format(lastAccessedTime) %><br>

</body>
</html>
```



:heavy_exclamation_mark: **session.setMaxInactiveInterval( 10 )** 를 입력하면 초단위 즉 10초 동안 의시간이 지나면 세션이 무효가 되어 10초후에 새로고침을하면 세션ID 가 다시 재생성되어 다른것을 확인할수 있다. 10초안에 새로고침을하면 다시 10초 연장되니까 확인하려면 10초뒤에 해야됨.



### Cookie 와 Session 의 차이점 에대해 설명하겠습니다.

Cookie 는 브라우저가 기억하고있다.

Session은 서버에서 생성해준다

만약 로그인을 유지하기위해 Cookie 에  ID ,Password 같은 민감한 정보를  담아서 준다면 좋지않을거다.

서버쪽에서 Session 에 저장해둔다면 훨씬 좋을거다.

***

### 톰캣에 session 유지시간 설정해보기

다이나믹 프로젝트 생성 -> Context Path 후로의 페이지요청 설정

* web.xml 을 생성후 

  ```xml
  <?xml version="1.0" encoding="UTF-8"?>
  <web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://xmlns.jcp.org/xml/ns/javaee" xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd" version="4.0">
    <display-name>jspEx1</display-name>
    <welcome-file-list>
      <welcome-file>index.html</welcome-file>
      <welcome-file>index.htm</welcome-file>
      <welcome-file>index.jsp</welcome-file>
      <welcome-file>default.html</welcome-file>
      <welcome-file>default.htm</welcome-file>
      <welcome-file>default.jsp</welcome-file>
    </welcome-file-list>
    <!--모든페이지의 디폴트값이된다 분단위 세션 유효시간 설정(설정파일 변경시 서버 재시작이 필요하다) -->
    	<session-config>
    		<session-timeout>1</session-timeout>
    	</session-config>	
  </web-app>
  ```

  web-app 안에` <session-config>`  안에 `<session-timeout>`  분단위정수 `</session-timeout> `

  값을 주면 모든 페이지에 기본세션유지값으로 설정이된다

  위에 코드는 1분동안 기다렸다가 다시새로고침을 해서 sessionID 를 확인해보면 바뀐걸알수있다.

  1)  web.xlm 에 도 세션의 유지시간 설정을하고,
  2) jsp 파일을 만든후 해당 jsp 파일에서 session.setMaxInactiveInterval(10) 설정을한다면?

​	답은 jsp페이지 에서 설정한 세션유지시간 10초가 덮어씌어져서 적용된다, 모든페이지의 기본값이 1분이지만 직접설정을한다면 값을

​	바꿀수있다.  	

## :star:session 에 데이터를 저장해보자



* 서버에서 session 이라는 객체에 session 이 유효한 기간동안 해당 session 에 데이터를 저장할수 있다.
  1. form 에서 데이터를 입력하고 jsp 요청을한다
  2. jsp 페이지에서 파라미터로 form데이터를 꺼내서 변수에 담는다 
  3. 변수에 담은데이터를 세션에 저장한다 `session.setAttribute("saveData", data)`
  4. 세션에 데이터를 꺼내본다. `session.getAttribute("saveData")`



sessionData.html

```html
<body>
<form action="sessionSave.jsp">
<input type="text" name="data" />
<input type="submit" value="전송" />
</form>
</body>
```



sessionSave.jsp

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>

    <%
    	String data =request.getParameter("data");
    	session.setAttribute("saveData", data); //세션에 저장
    	
    	response.sendRedirect("sessionInfo.jsp");
    %>
```

sessionInfo.jsp

```jsp
세션의 저장된 데이터 <%= session.getAttribute("saveData") %>
```

