## BeanFactory

* 스프링 컨테이너의 최상위 인터페이스다.
* 스프링 빈을 관리하고 조회하는 역할을 담당한다.
* `getBean()`  을 제공한다



## ApplicationContext

* BeanFactory 기능을 모두 상속받아서 제공한다.
* 빈을 관리하고 검색하는 기능을 BeanFactory 가 제공해주지만 차이가있다.
  * 애플리케이션을 개발할 때는 빈을 관리하고 조회하는 기능은 물론이고, 수 많은 부가기능이 필요하다
  * MessageSource   : 메시지 소스를 활용한 국제화 기능 (한국이면 한국어,영어권이면 영어로 출력)
  * 환경변수 : 이벤트를 발행하고 구독하는 모델을 편리하게 지원
  * 편리한 리소스 조회 : 파일, 클래스패스,외부 등에서 리소스를 편리하게 조회



:heavy_check_mark: 정리

* ApplicationContext 는 BeanFactory의 기능을 상속받는다
* ApplicationContext 는 빈 관리기능 + 편리한 부가 기능을 제공한다
* BeanFactory 를 직접 사용할 일은 거의 없다. 부가기능이 포함된 ApplicationContext 를 사용한다.
* BeanFactory나 ApplicationContext 를 스프링 컨테이너라 한다.
