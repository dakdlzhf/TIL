# :rocket: JSP



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

## :star: JSP 지시자 (Diractive)

* JSP 지시자(Directive)
  * 지시자는 클라이언트의 요청에 JSP 페이지가 실행이 될 때 필요한 정보를
     JSP 컨테이너에게 알리는 역할한다.
  * 지시자는 태그 안에서 @으로 시작하며, 3가지 종류가 있다.
     page, include, taglib	



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

  


