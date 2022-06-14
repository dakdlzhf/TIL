## 다양한 설정 형식지원 - 자바 코드,XML

* 스프링 컨테이너는 다양한 형식의 설정 정보를 받아드릴 수 있게 유연하게 설계되어 있다.
  * 자바코드 ,XML ,Groovy 등등



### :star: 어노테이션 기반 자바 코드 설정사용

* `new AnnotationConfigApplicationContext(AppConfg.class)`
* `AnnotationConfigApplicationContext` 클래스를 사용하면서 자바 코드로된 설정 정보를 넘기면 된다.



### :star: XML 설정 사용

* 최근에는 스프링 부트를 많이 사용하면서 XML 기반의 설정은 잘 사용하지않지만,아직 많은 레거시 프로젝트 들이 XML 로 되어있고, XML 을 사용하면 컴파일 없이 빈설정 정보를 변경할수 있는 장점도 있다.
* `GenericXmlApplicationContext` 를 사용하면서 `xml` 설정 파일을 넘기면 된다.
* xml 기반의 appconfig.xml 스프링 설정 정보와 자바 코드로 된 AppConfig.java 설정 정보를 비교해보면 거의 비슷하다는 것을 알수있다 (xml 를 사용하는것보다 자바 코드사용이 편리하다)
* xml 기반으로 설정하는 것은 최근에 잘 사용하지 않는 추세이다.



### :star: 스프링 빈 설정 메타 정보  BeanDefinition (Interface)

* 스프링은 어떻게 이런 다양한 설정 형식을 지원할까?	
  * 그 중심에는 BeanDefinition 이라는 추상화가 있다.
  * 쉽게 이야기해서 **`역할과 구현을 개념적으로 나눈것 이다.`**
    * XML 읽어서 BeanDefinition 을 만들면 된다
    * 자바 코드를 읽어서 BeanDefinition 을 만들면된다
    * 스프링 컨테이너는 자바 코드인지 XML 인지 몰라도 된다 (구현체 ) 오직 BeanDefinition (역할 ) 만 알면된다
  * `BeanDefinition` 을 빈 설정 메타 정보라고 한다
    * `@Bean` , `<bean>`  당 각각 하나씩 메타 정보가 생성된다
  * 스프링 컨테이너는 이 메타정보를 기반으로 스프링 빈을 생성한다.
* AppConfig.class 를  **`AnnotatedBeanDefinitionReader`** 가 읽어서 `BeanDefinition` 빈 메타정보를 생성하고 AnnotationConfigApplicationContext 를 통해서 ApplicationContext 스프링 컨테이너가 스프링 빈을 생성한다.
* appConfig.xml 설정 정보를 XmlBeanDefinitionReader 를 사용해서 읽고 `beanDefinition` 메타정보를 생성후 GenericXmlApplicationContext 를 통해서 ApplicationContext 스프링 컨테이너가 스프링 빈을 생성한다 .



:heavy_check_mark: 정리

* BeanDefinition 을 직접 생성해서 스프링 컨테이너에 등록할 수 도 있다. 하지만 실무에서 BeanDefinition 을 직접 정의하거나 사용할 일은 거의 없다.
* BeanDefinition 에 대해서는 너무 깊이 있게 이해하기보다는, 스프링이 다양한 형태의 설정 정보를 BeanDefinition 으로 추상화 해서 사용하는 것 정도만 이해 하면된다
* 가끔 스프링 코드나 스프링 관련 오픈 소스의 코드를 볼때,BeanDefinition 이라는 것이 보일 때가 있다. 이때 이러한 메커니즘을 기억하자 

