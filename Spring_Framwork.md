# :star: Spring Framwork 를 살펴보자



* 핵심 기술 : 스프링 DI 컨테이너 , AOP, 이벤트 ,기타
* 웹기술 :MVC , 스프링 WebFlux
* 데이터 접근기술 : 트랜잭션 , JDBC ,ORM 지원 XML 지원
* 테스트 : 스프링 기반 테스트 지원
* 언어 : 코틀린, 그루비



***



## :star: 스프링의 진짜 핵심!



* 스프링은 자바 언어 기반의 프레임워크다.
* 자바 언어의 가장 큰 특징 `객체 지향 언어` 
* 스프링은 **<u>객체 지향 언어가 가지고 있는 강력한 특징을 살려내는 프레임워크이다</u>**
* 스프링은 좋은 객체 지향 애플리케이션을 개발 할수 있도록 도와주는 프레임워크이다.



***



## :star: Spring Boot ?



* 스프링을 보다 편리하게 사용할수 있도록 지원을 한다 ,최근에는 기본적으로 사용을 하는 추세이다.
* 단독으로 실행할수 있는 Spring Application 을 쉽게 생성할수있다.
* Tomcat 같은 웹 서버를 내장해서 별도의 웹서버를 설치 하지않아도 된다.
* 손쉬운 빌드 구성을 위한 starter 종속성을 제공한다.
* 스프링과 3rd parth ( 외부 ) 라이브러리 를 자동으로 구성해준다.
* 메트릭, 모니터링, 외부구성 같은 프로덕션 준비기능을 제공한다.
* 관계에 의한 간결한 설정이 가능하다.



# :star_of_david: Polymorphism 다형성 이란?



## Sping 을 배우기전 자바 언어의 특징중 다형성을 알아보겠다.

* 자바 언어의 다형성 은 매우 핵심적인 특징중 하나이다.
* <u>스프링 프레임워크를 배우기전 다형성 에대한 개념을 다시한번 잡아야 스프링 프레임워크를 더 잘사용할수있다.!</u>



`다형성`

* 다형성을 실질적인 현실세계에 비유하여 예를 들어서 알아보자
  * 예) 자동차를 생각해보면 자동차의 `역할=Interface` 을 수많은 `자동차 종류=구현체`들이 있어도 `운전자=클라이언트` 는 자동차 면허가있거나,자동차를 운전하는 방법만 알고있다면 어떤 종류의 자동차든 운전을 할수있다 
  * 예2) 무대와 배우 를 생각해보자 , `로미오=역할`이 있다 . 로미오를 누가 연기할지 배우를 정하진않았지만 역할만 알고있다면 장동건이든 , 강동원이든 `배우=구현` 대체 가 가능하다 , 즉 변경이 가능하다
* 서버 ( 구현 ) 이 바뀐다하더라도 클라이언트 ( 역할 ) 에 영향을 주지않는다 이것이 올바른 다형성의 원칙이다
  * 클라이언트는 대상의 역할 ( 인터페이스 ) 만 알면된다
  * 클라이언트는 구현 대상의 내부 구조를 몰라도된다
  * 클라이언트는 구현 대상의 내부 구조가 변경되어도 영향을 받지 않는다
  * 클라이언트는 구현 대상자체를 변경해도 영향을 받지 않는다



:100: 객체를 설계할때는 역할과 구현을 생각하여 명확히 분리하여 설계하는것이 좋다 , 또한 인터페이스 를 먼저 부여 하고 (정의 ) 그 인터페이스를 수행하는 구현체 객체를 만들자!



* 객체 의 협력 관계 -
  * 혼자 있는 객체는 없다.
  * 클라이언트 = 요청 , 서버 = 응답,
  * 수많은 객체 클라이언트와 객체 서버 는 서로 협력 관계를 가진다.



### 정리해보자

* 다형성의 본질
  * 인터페이스를 구현한 객체 인스턴스를 실행 시점에 유연하게 변경이 가능해야한다.
  * 다형성의 본질을 이해하려면 협력이라는 객체사이의 관계에서 시작되어야 한다.
  * 클라이언트를 변경하지 않고 서버의 구현 기능을 유연하게 변경할수 있어야 한다.



## :star: 스프링과 객체지향 ?

* 스프링을 사용할때는 다형성이 가장 중요하다고 생각한다.
* 스프링은 다형성을 극대화해서 이용할수 있도로고 도와주기때문이다.
* 스프링에서 이야기하는 `제어의 역전(IoC)`  `의존관계주입(DI)`은 다형성을 활용해서 역할과 구현을 편리하게 다룰수 있도록 지원한다.



### :heavy_check_mark: SOLID 원칙에 대해 알아보자!

1. `SRP` (Single Responsibility Principle) = `단일 책임의 원칙`
   1. 한 클래스는 하나의 책임만 가져야한다
   2. 중요한 기준은 변경이다, 변경이 있을때 파급효과가 적으면 단일 책임 원칙을 잘 따른것이다.

1. `OCP` (Open Closed Principle) = 개방-폐쇄 원칙
   1. 소프트웨어 요소는 확장성은 열려있으나 ,변경에는 닫혀 있어야한다
   2. 다형성을 활용하자
   3. 인터페이스를 구현하는 클래스를 하나 만들어서 새로운 기능을 구현
   4. OCP 문제점
      1. 구현 객체를 변경하려면 클라이언트 코드를 변경해야한다.
      2. 분명 다형성을 사용했지만 OCP 원칙을 지킬수없다.
         1. 객체를 생성하고 , 연관관계를 맺어주는 별도의 조정,설정자가 필요하다 -> Spring 이 해결할수있다.
2. `LSP` (Liskov Subsitution Principle)
   1. 프로그램의 객체는 프로그램의 정확성을 깨뜨리지 않으면서 하위 타입의 인스턴스로 바꿀수 있어야 한다.
   2. 다형성에서 하위 클래스는 인터페이스 구약을 다지켜야 한다, 다형성을 지원하기위한 원칙, 인터페이스를 구현한 구현체를 믿고 사용하려면 이원칙이 필요한다.
      1. 예 ) 자동차 엑셀을 밟으면 앞으로 가야하는데, 뒤로가가 구현한다면 LSP 원칙을 위배한것이다. 엑셀을 밟아서 빠르거나,느리거나, 엑셀은 밟으면 앞으로 가야한다는 기본적인 규칙이 지켜져야한다.
3. `ISP` (Interface Segregation Principle)
   1. 특정 클라이언트를 위한 인터페이스는 여러개가 범용 인터페이스 하나보다 낫다.
   2. 특정 객체(클래스) 에 대한 책임을 덜어버리는것이 목표
   3. 기능을 쪼개고 쪼개서 클래스가 단하나의 책임 (SRP) 을 지니게 하는것을 돕는다.
   4. 예) 자동차 인터페이스 를 분리 
      1. 운전 인터페이스
      2. 정비 인터페이스
   5. 예 )사용자 인터페이스 를 분리
      1. 운전자 클라이언트
      2. 정비사 클라이언트
   6. 4,5번처럼 인터페이스를 분리하면 정비 인터페이스가 변하더라도 클라이언트에는 영향이 없다.
4. `DIP` (Dependency Inversion Principle)=의존관계 역전 원칙
   1. 프로그래머는 "추상화에 의존해야지 ,구현체에 의존하면 안된다" 의존성 주입은 이원칙을 따르는 방법중 하나이다.
   2. 구현 클래스를 의존하지말고, 인터페이스에 의존해라
   3. 다형성 Polymorphism 의 역할 ( Role ) 에 의존해야 한다는것 그래야 유연하게 구현체를 변경할수있다.
      1. 예 ) 무대와 배우 를 예를들자면
         1. 수많은 배우들이있고 역할은 하나이다 ( 로미오역할)
         2. 배우들이 누가될지몰라도 로미오 역할의 대본은 동일하고 로미오역할은 정해져있다.
         3. 배우가 바뀌더라고 로미오의 역할에 영향을 주면안된다
         4. 만약 배우들을 서포트하는 스타일리스트들이 있다고 해보자 스타일리스트가 바뀌었다고 배우가 역할을 못하겠다고하면 ? DIP 원칙이 깨진거다 스타일리스트라는 구현체때문에 배우라는 인터페이스가 영향을받게된거다. 또한 배우한테 역할은 로미오라는 인터페이스이다. 즉 저기아래 있는 연결되있는 스타일리스트라는 구현하나때문에 로미오 역할까지 영향을 주어서 설계하면안된다.
   4. 의존관계란 서로의 관계를 눈치채고 알고있다는것 자체가 의존관계 성립이다, 서로 아예 모르고있어야 의존관계가 없는거다



## :heavy_check_mark: 정리하자면

* 객체 지향의 핵심은 다형성이다
* 하지만 다형성 만으로는 유연하고 변경이 가능하게 개발하기가 쉽지는 않다
* 다형성 만으로는 구현 객체를 변경할때 클라이언트 코드도 함께 변경이 될수있다.
* 다형성만으로는 OCP , DIP 를 지킬수 없다
* 무언가 가 필요하다 그것이 Spring 이 나온 이유이기도하다
  * 스프링은 다음 기술로 다형성 + OCP + DIP 를 가능하게 지원한다
    * DI (Dependency Injection) 의존 관계, 의존성 주입
    * DI 컨테이너 제공
  * 클라이언트 코드의 변경없이 기능 확장이 가능하다
  * 쉽게 부품을 교체하듯이 개발할수 있게된다.



