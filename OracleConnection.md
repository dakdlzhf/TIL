## java 와 oracle db 연동

* **`Driver`**

  * 오라클에 db를 사용하려면 java프로그램과 오라클에서 이미 java 언어로 만들어놓은 driver (사용방법) 인터페이스를 이용해야한다.
  * java 에 객체지향 상속,다형성 개념을 통해서 프로젝트에 포함된 Driver 정의되어 있는 그런 데이터베이스 연동하는 클래스를 활용해서 사용할 프로그램 코드에 적용만하면 Driver 를 통해서 이기능들을 오라클 데이터베이스에 접근하고 쿼리를 보내고 결과를 얻어올수 있다.
    * 자르파일이 필요하다 (ojdbc6-11.2.0.3.jar 를 프로젝트에 포함시켜야한다.)
      * 많이사용하는 메이븐이라고 하는 빌드도구 가 필요한 의존 라이브러리프로그램들을 관리해주고 빌드해준다. 그때 리모트(Remote) 리포지토리라고(원격 저장소) 하는곳이 있는데, 여기에 가보면 오라클 데이터베이스를 사용하기위한 jdbc Driver 를 제공하고 있다. (공식홈페이지 에서 찾아서 다운로드해도 되지만 복잡해서 ) 이곳링크에서 받기를 권한다 https://repo1.maven.org/maven2/com/oracle/database/ 
      * 현재 프로젝트 JDK 버전과 Oracle 버전에 따라 jdbc 버전도 다른걸 사용할수 있게된다.
  * :star2: **Build Path 에 jdbc 자르파일 추가하기**
    * java 프로젝트를 만들고 -> build path -> configure build path -> Add Jars 클릭 다운받은 ~~.jar 추가 Apply 해주거나,
    * lib 패키지를하나만들고 넣어둔 jdbc.jar 파일 우클릭 build path -> Add to Build Path 눌러도 된다.

  :star_of_david: 자바 프로젝트에서 Driver 를 포함시키고 사용하면된다.

  ```java
  public class ExamDriveroLoad {
  	public static void main(String[] args) {
  
  		try {
  			Class.forName("oracle.jdbc.OracleDriver"); // Driver 클래스 하나를 로딩해줘야한다.
  			System.out.println("클래스 로딩성공!");
  		} catch (ClassNotFoundException e) {
  
  			e.printStackTrace();
  		}
  
  	}
  
  }
  ```

  

  :star2:**실행했을때 문제없이 클래스 로딩성공이 출력되면 성공! 하지만 ClassNotFoundException 이발생되면 Build Path 에 문제!**

  :star2: **만약 Oracle DBMS 를 사용하지않고 다른 DBMS 를사용한다면 .jar 파일과 Driver 클래스가 다를수있다.**
  
  ***
  
  

### :rocket: Step 2

자바와 DB 연동이 끝났으면 이제는 데이터베이스 연동을 컨넥션 해야한다.

* 접속 계정/비밀번호/접속url ( "jdbc:oracle:thin:@localhost:1521:xe" ) Oracle 접속 Url 은 정해져있다.
  * 현재는 localhost 라서 @localhost 인데, 로컬이아니라면 사용할 해당 ip 주소가 필요하다.

