## Servlet 

Servlet 에 있는 메소드 들은 모두 콜백함수이다

* HttpServlet
  * 서블릿을 만들기 위해서 반드시 상속해야 할 필수 클래스
  * Servlet 인터페이스 >  GenericServlet 추상클래스 > HttpServlet 상속구조



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

