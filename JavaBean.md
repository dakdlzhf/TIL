## :star_of_david: Java Bean (useBean,setProperty,getProperty)



:star: MVC1 에서는 jsp 문법(액션태그)  useBean,setProperty,getProperty  사용을 권장한다.

:star: 코드의 가독성과 적은코드로 효율을 높일수 있다.



먼저 **useBean** **액션태그는** **특정한** **자바빈** **파일을 사용한다고** **명시**  할 때 사용된다. 형식은 아래와 같다.



* **`<jsp:useBean id="빈 이름" class="자바빈 파일의 패키지.클래스명" scope="유효범위" />`**
  *  **useBean 액션태그**는 [ **클래스 빈이름 = new 클래스();**] **와 동일한 의미**를 갖는다.  즉, id 속성은 객체명, class 속성명은 클래스(패키지 포함 기술)를 의미하며 import가 포함되어 있다. scope 속성은 유효범위를 의미하며 page(생성된 페이지 내), request(요청된 페이지 내), session(웹브라우저의 생명주기), application(어플리케이션의 생명주기)을  작성할 수 있으며, 기본값은 page이다.

 **setProperty 액션태그**는 자바빈 파일의 **setter 메서드를 사용**하기 위해, 즉 **데이터의 값을 설정할 때 사용**된다. 형식은 아래와 같다.



* **`<jsp:setProperty name="빈 이름" property="필드명" value="값" />`**
  * setProperty 액션태그는 setter 메서드와 같은 의미를 갖는다. **useBean** **액션태그로** **생성한** **자바빈** **객체에 대해서 프로퍼티(필드)에 값을 설정하는 역할**을 한다. 즉, [빈이름.set필드(값);] 과 같은 의미를 갖는다.
* **`<jsp:setProperty name="빈 이름" property="\*" />`**
  * **property 속성에 \* 를 사용하면 프로퍼티와 동일한 이름의 파라미터를 이용하여 setter 메서드를 생성한 모든 프로퍼티(필드)에 대해 값을 설정**할 수 있다.



:heavy_check_mark: jsp 액션태그중 useBean 에는 2개의 속성 id , class 를 꼭입력해야 사용이가능하다



아래코드는 useBean ,setProperty,getProperty 를 이용하여 자바빈에 객체의 값을 저장하고 출력하는 코드이다.

```jsp
<%@ page contentType = "text/html; charset=utf-8" %>                                             
<html> 
<head> 
</head> 
<body> 
     <jsp:useBean id="myUser" class="com.dololak.servlet.User" scope="request"/> 
     <jsp:setProperty name="myUser" property="name" value="kim dololak"/> 
     <jsp:setProperty name="myUser" property="age" value="28"/> 
     <jsp:setProperty name="myUser" property="address" value="seoul"/> 
     
     
      이름 : <jsp:getProperty name="myUser" property="name"/><br> 
      나이 : <jsp:getProperty name="myUser" property="age"/><br> 
      주소 : <jsp:getProperty name="myUser" property="address"/><br> 
</body> 
</html>
```



아래의 코드처럼 property 에 * 을 넣는다면 현재page 의 form 의 모든 name 을 myUser 자바빈 에 모두 setter 하겠다는의미다. 

```jsp
  <jsp:setProperty name="myUser" property="*"/> 
```



:heavy_check_mark: 주의

<u>form 에 input 에 값을 입력받는다면 input 에 속성 name="변수명" 과 bean 객체의(myUser) 필드명(property) , 이 동일해야[myUser객체의.set필드명] 으로 적용이 된다</u>



<u>form 의 name 과 서블릿으로 값을 받을때 request.getParameter("name") 명이 같은것도 기억하자</u>

******

​	
