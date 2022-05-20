# :rocket: JSP

### JSP 페이지 내장객체

| 내장객체    | 리턴타입                               | 설명                                                         |
| ----------- | -------------------------------------- | ------------------------------------------------------------ |
| request     | javax.servlet.http.HttpServletRequest  | 웹 브라우저의 요청 정보를 저장하는 객체                      |
| response    | javax.servlet.http.HttpServletResponse | 웹 브라우저의 요청에 대한 응답정보를 저장하고있는 객체       |
| out         | javax.servlet.jsp.jsp.jspWriter        | JSP 페이지에 출력할 내용을 가지고 있는 출력 스트림 객체      |
| sesseion    | javax.servlet.http.HttpSession         | 하나의 웹 브라우저의 정보를 유지하기위한 세션정보를 저장하는 객체 |
| application | javax.servlet.ServletContext           | 웹 어플리케이션에 대한 정보를 저장합니다.                    |
| config      | Javax.servlet.ServletConfig            | JSP 페이지에 대한 설정 정보를 저장합니다.                    |
| page        | javax.lang.Object                      | JSP페이지를 구현한 자바 클래스 인스턴스                      |
| exception   | javax.lang.Throwable                   | 익셉션 객체, 에러페이지에서만 사용됩니다.                    |

:heavy_exclamation_mark:	기본객체 중에서 exception 기본 객체를 제외한 나머지 8개 기본 객체는 모든 JSP페이지에서 사용할수 있으며, exception 기본 객체는 오직 에러 페이지에서만 사용할수 있다.


### JSP 내장 객체의 속성(attribute)과 관련된 메소드

| 메소드                                | 리턴타입              | 설명                                                         |
| ------------------------------------- | --------------------- | ------------------------------------------------------------ |
| setAttribute(String key,Object value) | void                  | 해당 내장 객체의 속성 값을 설정하는 메소드로,속성명에 해당하는 key 매개 변수에 속성값에 해당하는 value 매개 변수의 값을 지정 |
| getAttributeNames()                   | java.util.Enumeration | 해당 내장 객체의 속성 명을 읽어오는 메소드로 ,모든 속성의 이름을 얻는다 |
| getAttribute(String key)              | Object                | 해당 내장객체의 속성 명을 읽어오는 메소드로 , 주어진 key 매개 변수에 해당하는 속성명의 값을 얻는다. |
| removeAttribute(String key)           | void                  | 해당 내장 객체의 속성을 제거하는 메소드로 주어진key 매개 변수에 해당하는 속성명을 제거한다. |


	
* JSP 내부객체의 이해

  - 발자가 객체를 생성하지 않아도 jsp페이지가 서블릿 컨테이너(Tomcat)로 로딩되면 Tomcat등 서버가 자동으로 생성하는 객체이다.

  * 개발자는 반복적인 작업을 줄이고 필요한 작업만 할수 있다. 
  * jsp페이지는 Web서버 및 Servlet Container라고 하는 복잡한 환경에서 실행이  되기 때문에, 실행중에 여러가지 상태정보를 가지고 있어야 하는데,  이런 경우에 사용되는 객체들이 내부 객체들이다. 
  * 내부 객체로 인해 개발자는 좀더 쉽게 JSP 프로그래밍이 가능함. 


## 1) 스크립트릿

* 자바코드를 작성하는곳
  * 연산을하거나 
  * 기능적인 로직 정의



## 2) 표현식

* 값을 브라우저에 출력 ( 표시  )
  * 연산 x , 기능처리 x



## 3) 선언문

* 동작에 필요한 멤버 필드 , 멤버 메서드를 정의하는곳



### 자바,JSP 코드

* WAS (web Application Server ) 에서 처리 ( 동적 페이지 )

* 만약에 JSP 에서 에러코드가있다면 브라우저에서 500 error 가표시된다. 

* 이클립스에는 자체적인 내부프로세스가 동작하며 컴파일에러를 체크하는데 코드의 구문들을 검사하다가 처리가 잘못된 error 표시 가 표시되는것같으면 

* Ctrl + A  전체선택

  * Ctrl +X 잘라내기
    * Ctrl+S 저장하기
      * Ctrl +V 붙여넣기
        * Ctrl +S  

  했을때 이클립스 error 표시가 없어 진다면

  코드에 문제가 없는거다

  하지만 그래도 이클립스에 error 표시가 나오면 정말

  코드에 문제가있는거다.

:star: 주로 선언문보다는 스크립트릿 + 표현문 을 자주사용하게된다.

## :100: 요약 해보면

* 스크립트릿 은 자바코드를 사용할수있는 곳 ( 서버처리 )
* 표현식은 값을 출력 하여 브라우저 에 표기 할수있다. (브라우저 표시)

***

## :arrow_forward:  JSP 파일이 처리되는 과정 ( Life Cycle)



### 서비스 시작 및 최초 JSP 파일 요청 처리순서

1. 최상위 경로 Context Path 에 basic 이라는 요청이 들어간다

2. jsp 파일 요청을 받은 후 서버는 요청 한jsp 파일 을 찾는다

3. jsp 파일을 찾으면 톰캣은 JSP 파일을 JAVA 파일로 생성한다.

4. 만들어진 JAVA 파일을 Class 파일로 컴파일 한다.

5. Class 파일로 컴파일후에는 서버의 메모리에 Load 하게된다.(객체를 생성했다 생각하면된다 객체를 생성하면 메모리 할당이 이뤄지는것이니까)

6. 서버의 메모리에서는 톰캣이 JSPINIT ( ) 을 호출하여 초기값을 세팅한다. ( 객체의 생성자 다음에 동작되는 거라고 보면된다. )

7. jspService 함수가 동작이되면 이런저런 처리를하고 HTML 코드도 만들어내고 만들어진 내용은 결국 응답 ( HTTP Response 가 된다.)

8. Response 가 된 HTML 코드가 브라우저를 통해 해석이 되서 화면에 나온다

   * :heavy_exclamation_mark: 만약 같은 jsp 파일 요청이들어오면 이미 jsp 파일을 자바코드로 바꿔서 컴파일도 하고 메모리에도 올라가서 동작중인데 다시 컴파일하고 다시 객체를 생성할 필요가 없기때문에 :heavy_exclamation_mark: 이럴경우 에는 jspService () 메서드를 호출 후 내용을 처리하고 HTML 파일을 만들어서  HTTP Response 한다.

   * :heavy_exclamation_mark: 만약  변경사항이 있다면 해당 객체의 jspDestroy () 메서드를 호출하여 그 해당 파일을 다시 메모리에 올려야 되기 때문에 전 객체를 삭제해야한다.             이때 우선 jspDistroy () 메서드를 호출한 후 메모리에서 객체가 사라지게된다

     *  변경사항이 확인되면 동일하게 서블릿 객체 제거후 최초요청과 동일하게  진행을한다.

     ## :heavy_check_mark: 요약 정리

* ***JSP 파일에서 멤버변수,멤버 메소드 와 같이 생성한 값이 있다면  클라이언트의 jsp 파일 요청이 전과 비교를한다***



* ***변경 사항이 없으면 값은 유지가될것이고, 요청사항이 변경된게 있다면 메모리 에 jspDestroy 메서드 호출후 서버 메모리에 객체를 삭제 한후 다시 객체를 생성하기때문에 멤버 변수 의 값이 다시 초기화 셋팅 되기때문에 초기값으로 돌아간다.***
  * jspDestroy () 는 객체를 삭제하는 기능이 있는것이 아니라 !! 제거하기전에 정리해야 될 기능들을 갖게끔 오라이딩 해서 쓸수 있는 함수 다 (jspinit 도 마찬가지다
    * <u>오버라이딩해서 쓸수있는 놈들이다 !!</u>


1) **jsp 파일 확인후 java 파일로 생성 -> class 파일 로 컴파일** 
2) **서버 Memory 에 객체생성해서 .jspInit()함수 호출 **
3) **.jspService() 호출해서 response**



:boom:<u>**서버 종료시 톰캣이 갖고있던 인스턴스(서블릿)를 어떻게정리하는지까지 알아보았다.**</u>

***

## :star: JSP 태그종류

[ JSP 태그 ]

- HTML 기반의 JSP 코드 내에 JAVA 코드를 삽입할 수 있게 해주는 태그

|   `구분`   |            `JSP태그`            |              `용도`               |
| :--------: | :-----------------------------: | :-------------------------------: |
|   지시자   |             <%@  %>             |         페이지 속성 지정          |
|    주석    |            <%-- --%>            |             주석 처리             |
|    선언    |            <%!   %>             |        변수, 메소드의 선언        |
|   표현식   |             <%=  %>             |            결과값 출력            |
| 스크립트릿 |             <%   %>             |          JAVA 코드 삽입           |
|  액션태그  | <<jsp:action>> < </jsp:action>> | 페이지 삽입, 공유, 자바빈 사용 등 |





### 1. JSP 지시자(Directive)

[ 지시자 : <%@  %> ]

- JSP 페이지가 컨테이너에게 필요한 메세지를 보내기 위한 태그
- page : JSP 페이지의 전체적인 속성을 지정
- include : 다른 페이지를 현재 페이지에 삽입
- taglib : 태그라이브러리의 태그 사용
- 범위 : JSP 파일 전체 (클래스를 import 할 경우 파일 내 어디서든 접근할 수 있음)

* 지시자는 클라이언트의 요청에 JSP 페이지가 실행이 될 때 필요한 정보를
   JSP 컨테이너에게 알리는 역할한다.

* 지시자는 태그 안에서 @으로 시작하며, 3가지 종류가 있다.
   page, include, taglib	

```jsp
<%@page import="java.util.Arrays"%>
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
```



[ 선언 : <%!  %> ]

- 변수와 메소드를 선언함
- 범위 : 페이지 내 어디서나 접근할 수 있는 전역 변수 및 메소드

:star:변수는 클래스의 필드와 같은 역할입니다. 선언된 변수나 메소드는 어디서든 접근해서 사용 가능합니다. JSP는 HTML 기반이지만 JSP 태그만 간단히 쓸 때는 클래스를 작성할 때와 크게 다른 점은 없습니다. 표현식 <% %>에서 변수를 선언하는 것과 다르지 않지만 메소드를 작성할 수 있다는 점에서 다릅니다. 

```
	<%-- 변수 및 메소드 선언 --%> 
	<%! 
		int a; 
		int b;
		
		public int sum(int a, int b) {
		return a + b;
		}
	%>

	<%-- 자바 코드 삽입 --%>
	<% 
		a = 10;
		b = 20;
		out.println(sum(a, b));
	%>
```



[ 표현식 : <%=  %> ]

- 변수 또는 메소드의 결과값을 출력
- 자바 코드를 삽입하는 것보다 더 간단하게 출력 가능
- 변수나 메소드를 사용할 때 세미콜론(;)을 사용하지 않음

:star:위의 선언 태그 코드에서 sum() 메소드의 결과값을 출력하기 위해 out.println() 메소드를 사용했습니다. 출력에 대한 코드를 줄일 수 있는 태그가 표현식입니다. 아래와 같이 코드를 바꿀 수 있습니다. 

```:heavy_check_mark:
<%-- 변수 및 메소드 선언 --%> 
	<%! 
		int a; 
		int b;
		
		public int sum(int a, int b) {
		return a + b;
		}
	%>

	<%-- 자바 코드 삽입 --%>
	<% 
		a = 10;
		b = 20;
	%>
	
	<%-- 표현식을 사용해 출력 --%>
	<%= sum(a,b) %>
```

:heavy_check_mark: 위 코드의 예시만으로는 별 다른게 없어보이지만 아래와 같이 만약 HTML 코드 중간에 간단히 사용해야 하는 경우라면 코드를 짧게 사용할 수 있어 가시성도 좋아지고 편리하게 쓸 수 있습니다. 세미콜론을 사용해서 코드 간의 구분을 해줄 수 없기 때문에 하나의 변수나 메소드만 간단히 삽입할 때 사용합니다.

* 표현식 결과 = 30 / 스클립트릿 결과 = 30

```jsp
<%-- 변수 및 메소드 선언 --%> 
	<%! 
		int a; 
		int b;
		
		public int sum(int a, int b) {
		return a + b;
		}
	%>

	<%-- 자바 코드 삽입 --%>
	<% 
		a = 10;
		b = 20;
	%>
	
	<%-- 표현식을 사용해 출력 --%>
	표현식의 결과값은 <%= sum(a,b) %> 입니다. <br/>
	
	<%-- 스크립트릿(자바 코드 삽입)을 사용해 출력 --%>
	스크립트릿의 결과값은 <% out.println(sum(a,b)); %> 입니다.
```



[ 스크립트릿 : <%  %> ]

- 자바 코드를 삽입하기 위한 태그
- 기존 자바 언어를 동일하게 사용할 수 있음

위의 예시 코드에서 계속 나온대로 자바 코드를 삽입하는 태그입니다. 자바 언어를 사용해서 JSP를 구성하기 위해 가장 많이 쓰이는 태그입니다. 뷰 역할의 JSP에 자바 코드를 최대한 줄이기 위해 JSTL을 대신 사용하는 경우도 많습니다. JSTL은 별도로 다루도록 하겠습니다.

 

아래 코드와 같이 자바 코드와 HTML을 섞어서 사용할 수도 있습니다. 반복문 사이에 HTML 코드를 섞어서 사용한 예시입니다.



```jsp
<% 
		int i = 0;
		while (true) {
			
			out.println(i + " 번째 줄");
			i++;
		
	%>

	<br/>============== <br/>
	
	<%
		if (i > 5)
			break;
		}
	%>
```



:star:출력

0 번째 줄

=============

1 번째 줄

=============

2 번째 줄

=============

3 번째 줄

=============

.......



[ 액션태그 : <jsp:action> </jsp:action> ]

- <jsp:include> : 다른 페이지의 실행 결과를 현재 페이지에 포함시켜줌
- <jsp:forward> : 페이지 간의 제어를 이동시켜줌
- <jsp:useBean> : 자바빈(java bean)을 페이지에서 사용할 수 있게 해줌
- <jsp:setProperty> : Property 값을 세팅할 때 사용
- <jsp:getProperty> : Property 값을 가져올 때 사용
- <jsp:param> : include, forward 안에서 사용되며, 인자를 추가할 때 사용

액션 태그를 사용할 때는 바디가 따로 있는 경우는 </jsp:action>으로 닫아줘야 하고, 바디가 따로 없는 경우에도 <jsp:action ~~ /> 형태로 닫아줘야 합니다.

* <jsp:include> (지시자의 include 디렉티브와 액션태그 include의 차이)

 

:heavy_exclamation_mark:   지시자의 include 디렉티브는 위에서 설명했듯이 소스파일의 내용을 그대로 가져다 붙이는 방식입니다. 따라서 다른 페이지를 include 하게 되면 결과물인 HTML 코드만 합쳐지는게 아니라 그냥 JSP 파일의 코드가 합쳐진다고 생각하면 됩니다. include된 페이지의 자원을 가져다쓸 수 있다는 의미입니다. 아래 예시를 보시면 test.jsp 파일에는 "String str" 이라는 변수를 생성한 적이 없음에도 include.jsp 파일을 include 해줌으로써 해당 파일에 있는 변수를 사용할 수 있습니다. 즉, include.jsp의 코드가 그대로 붙어있어서 컴파일할 때 컨테이너가 처리해준다는 뜻입니다.

```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<%@ include file = "include.jsp" %>
	<% 
		out.println(str + "<br/>"); 
		str = "바꿀 수도 있다!";
		out.println(str + "<br/>"); 
	%>	
	
</body>
</html>
```



```jsp
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Insert title here</title>
</head>
<body>
	<%!
		String str = "나는 include 된 페이지다아~!";
	%>
	<% out.println(str + "<br/>"); %>
</body>
</html>
```



1. page 지시자
    \- jsp페이지에서 지원되는 속성들을 정의하는 것들이다.
    \- jsp페이지에서 JSP컨테이너에게 해당 페이지를 어떻게 처리할 것인가에
    대한 페이지 정보를 알려준다.

   * `info`
     * 페이지설명, jsp 페이지 제목을 붙이는 것과 같다.

   * `language`
     *  Jsp페이지의 스크립트 언어지정 기본값은 Java

   * `contentType`
     * jsp의 출력 형식 지정, 문자 셋을 지정합니다. 

```jsp
//형식: contentType="text/html; charset=UTF-8" 
  <%@ page contentType="text/html; charset=UTF-8" %> 

```

 \- JSP처리 결과가 HTML임으로 MIME Type을 'text/html'과 문자 코드(UTF-8)
  선언. 

 \- MIME Type: 브러우저가 출력하는 데이터의 종류를 나타낸 코드값, 

 예) image/jpg는 이미지가 출력됨 

 \- HTML 태그의 META태그도 일치시켜야함(브러우저용). 

 <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"> 

 <meta http-equiv="Content-Type" content="text/html; charset=EUC-KR"> 



* `import`

* 패키지의 import, 중복 사용가능 

    자바에서 패키지를 사용하겠다고 선언하는 것과 같다

```jsp
 <%@ page import="java.util.*" %>
```



2. include 지시자

*  여러 jsp페이지에서 공통적으로 포함하는 내용이 있을 때 이러한 내용을
    매번 입력하지 않고 파일에 저장한 후 JSP파일에 포함해서 실행한다.
* 처리 결과가 합쳐지는 것이 아니라 파일의 소스가 하나의 파일에 합쳐진
    다음 실행된다. 

### 2. 액션태그

* JSP 문법이다.

  * 액션태그의 종류는 include, forward, useBean, setProperty, getProperty
     등이 있다.
    * useBean, setProperty, getProperty
      자바빈즈(JavaBeans)와 통신을 위해서 구현한 액션태그 이다.
  * forward 
    * 다른페이지로 이동할 때 사용하는 태그이다

  예) 브라우저 요청 -> A.jsp 처리 forwar 액션 을사용하여 B.jsp 로 그대로넘긴다 -> B.jsp 에서 처리하고 ->브라우저로 응답

​			브라우저에 요청은 1번이지만 A.jsp ~ B.jsp 에서 처리처리 된다. B.jsp 에서 응답했지만 URL 을 보면 A.jsp 인것을 확인할수있다.


