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

