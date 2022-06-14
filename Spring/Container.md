# :star: 스프링 컨테이너

* `ApplicationContext` 를 스프링 컨테이너라고 한다
* 기존에는 개발자가 `AppConfig` 를 사용해서 직접 객체를 생성하고 DI 를 했지만, 이제부터는 스프링 컨테이너를 통해서 사용한다
* 스프링 컨테이너는 `@Configuration` 이 붙은 `AppConfig` 를 설정(구성) 정보로 사용한다. 여기서 `@Bean` 이라 적힌 메서드를 모두 호출해서 반환된 객체를 스프링 컨테이너에 등록한다 . 이렇게 스프링 컨테이너에 등록된 객체를 스프링 빈 이라고 한다
* 스프링 빈은 `@Bean` 이 붙은 메서드의 명을 스프링 빈의 이름으로 사용한다.
* 이전에는 개발자가 필요한 객체를 `AppConfig` 를 사용해서 직접 조회했지만,이제부터는 스프링 컨테이너를 통해서 필요한 스프링 빈 (객체) 를 찾아야 한다. 스프링 빈은 `applicationContext.getBean()` 메서드를 사용해서 찾을수 있다.
* 기존에는 개발자가 직접 자바코드로 모든것을 했다면 이제부터는 스프링 컨테이너에 객체를 스프링 빈으로 등록하고 ,스프링 컨테이너에서 스프링 빈을 찾아서 사용하도록 변경되었다. 

***



### 스프링 컨테이너 생성

* new AnnotationConfigApplicationContext( 구성정보.class)
  * 스프링 컨테이너를 생성할때는 구성정보 를 지정해주어야 한다.



### 스프링 빈

* @Bean

  ```java
  @Configuration
  public class AppConfig {
  
      //@Bean 을 해놓으면 Spring 컨테이너에 등록을한다.l
      @Bean
      public MemberService memberService(){
          return new MemberServiceImpl(memberRepository());
      }
      @Bean
      public MemberRepository memberRepository(){
          return new MemoryMemberRepository();
      }
  
      @Bean
      public OrderService orderService(){
          return new OrderServiceImpl(memberRepository(),discountPolicy());
      }
  
      @Bean
      public DiscountPolicy discountPolicy(){
          return new RateDiscountPolicy();
      }
  
  }
  ```

  

  * 스프링 컨테이너는 파라미터로 넘어온 설정 클래스 정보를 사용해서 `스프링 빈`을 등록한다
    * 아래는 스프링 컨테이너 내부이다

  | 빈이름           | 빈객체                     |
  | ---------------- | -------------------------- |
  | memberService    | MemberServiceImpl@x01      |
  | orderSerivce     | OrderServiceImpl@x02       |
  | memberRepository | MemoryMemberRepository@x03 |
  | dicountPolicy    | RateDiscountPolicy@x04     |

​	

* 빈 이름은 메서드 이름을 사용한다.
* 빈이름을 직접 주여할수도 있다
  * @Bean(name="beanObject")
    * :heavy_check_mark: 주의:  `빈이름은 항상 다른 이름을 부여` 해야한다 .같은 이름을 부여하면, 다른 빈이 무시되거나,기존 빈을 덮어버리거나 설정에 따라 오류가 발생한다.
* `스프링 컨테이너는 ` 설정 정보를 참고해서 의존관계를 주입 `DI` 한다
* :heavy_check_mark: 스프링은 빈을 생성하고, 의존관계를 주입하는 단계가 나뉘어져 있다. 그런데 이렇게 자바 코드로 스프링 빈을 등록하면 생성자를 호출하면서,의존관계 주입도 한번에 처리된다. 

:heavy_exclamation_mark: 정리 : 스프링 컨테이너를 생성하고 ,설정(구성)정보를 참고해서 스프링 빈도 등록하고,의존관계도 설정한다



### 스프링 에 등록된 빈 정보를 출력

* 모든 빈 출력하기

  * 실행하면 스프링에 등록된 모든 빈 정보를 출력할수 있다.
  * `ac.getBeanDefinitionNames()` : 스프링에 등록된 모든 빈 이름을 조회한다.
  * `ac.getBean() `: 빈 이름으로 빈 객체(인스턴스) 를 조회한다

* 애플리케이션 빈 출력하기

  * 스프링이 내부에서 사용하는 빈은 제외하고 내가 등록한 빈만 출력할수있다.
  * 스프링이 내부에서 사용하는 빈은 `getRole()` 로 구분할 수 있다.
    * `ROLE_APPLICATION` :일반적으로 사용자가 정의한 빈
    * `ROLE_INFRASTRUCTURE`: 스프링이 내부에서 사용하는 빈

  ```java
  package hello.core.beanfind;
  
  import hello.core.AppConfig;
  import org.junit.jupiter.api.DisplayName;
  import org.junit.jupiter.api.Test;
  import org.springframework.beans.factory.config.BeanDefinition;
  import org.springframework.context.annotation.AnnotationConfigApplicationContext;
  
  public class AppicationContextInfoTest {
      AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);
  
      @Test
      @DisplayName("모든 빈 출력하기")
      void findAllBean(){
          String[] beanDefinitionNames = ac.getBeanDefinitionNames();
          for (String beanDefinitionName : beanDefinitionNames) {
              Object bean = ac.getBean(beanDefinitionName);
              System.out.println("name = " + beanDefinitionName + "object" + bean);
              
          }
      }
  
      @Test
      @DisplayName("애플리케이션 빈 출력하기")
      void findApplicationBean(){
          String[] beanDefinitionNames = ac.getBeanDefinitionNames();
          for (String beanDefinitionName : beanDefinitionNames) {
              BeanDefinition beanDefinition = ac.getBeanDefinition(beanDefinitionName);
  
              //Role ROLE_APPLICATION : 직접 등록한 애플리케이션 빈
              //Role ROLE_INDRASTRUCTURE : 스프링 내부에서 사용하는빈
  
              if(beanDefinition.getRole() == BeanDefinition.ROLE_APPLICATION){
                  Object bean = ac.getBean(beanDefinitionName);
                  System.out.println("name = " + beanDefinitionName + "object" + bean);
              }
  
          }
      }
  }
  
  ```
  

### 스프링 빈 조회 -기본

스프링 컨테이너에서`스프링 빈을 찾는 가장 기본적인 조회방법`

* `ac.getBean(빈이름,타입)`
* `ac.getBean(타입)`
* 조회 대상 스프링 빈이 없으면 예외 발생
  * `NoSuchBeanDefinitionException: No bean named 'xxxxx' avilable`



```java
package hello.core.beanfind;

import hello.core.AppConfig;
import hello.core.member.MemberService;
import hello.core.member.MemberServiceImpl;
import org.assertj.core.api.Assertions;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.NoSuchBeanDefinitionException;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;

import static org.assertj.core.api.Assertions.*;
import static org.junit.jupiter.api.Assertions.*;

public class ApplicationContextBasicFindTest {
    AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(AppConfig.class);

    @Test
    @DisplayName("빈 이름으로 조회")
    void findBeanByName(){
        MemberService memberService = ac.getBean("memberService", MemberService.class);
        assertThat(memberService).isInstanceOf(MemberServiceImpl.class);
    }

    @Test
    @DisplayName(" 이름없이 타입으로만 조회")
    void findBeanByType(){
        MemberService memberService = ac.getBean( MemberService.class);
        assertThat(memberService).isInstanceOf(MemberServiceImpl.class);
    }

    @Test   
    @DisplayName("구체 타입으로 조회") 

    void findBeanByName2(){
        MemberService memberService = ac.getBean("memberService", MemberServiceImpl.class);
        assertThat(memberService).isInstanceOf(MemberServiceImpl.class);
            //구체타입으로 조회를 하면 인터페이스에 의존하는게 아닌 구현에 의존하기에 유연성이 낮아진다
    }
 
    @Test
    @DisplayName("빈 이름으로 조회 실패")
    void fintBeanByNameX(){
        //ac.getBean("xxxxx",MemberService.class);

        assertThrows(NoSuchBeanDefinitionException.class,
                ()->ac.getBean("xxxxx", MemberService.class));
    }
}

```



### 스프링 빈 조회 - 동일한 타입이 둘 이상

* 타입으로 조회시 같은 타입의 스프링 빈이 둘 이상이면 오류가 발생한다. 이때는 빈 이름을 지정하자
* `ac.getBeansofType()` 을 사용하면 해당 타입의 모든 빈을 조회할 수있다. 

```java
package hello.core.beanfind;

import hello.core.AppConfig;
import hello.core.discount.DiscountPolicy;
import hello.core.member.Member;
import hello.core.member.MemberRepository;
import hello.core.member.MemoryMemberRepository;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

public class ApplicationContextSameBeanFindTest {
    AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(SameBeanConfig.class);

    @Test
    @DisplayName("타입으로 조회시 같은 타입이 둘 이상 있으면, 중복 오류가 발생한다.")
    void findBeanByTypeDuplication() {
        MemberRepository bean = ac.getBean(MemberRepository.class);
    }
    @Configuration
    static class SameBeanConfig{

        @Bean
        public MemberRepository memberRepository1(){
            return new MemoryMemberRepository();
        }

        @Bean
        public MemberRepository memberRepository2(){
            return new MemoryMemberRepository();
        }
    }
}


```



* 타입으로 조회시 동일한 타입이 둘이상 있다면 Exception 발생!
  * `NoUniqueBeanDefinitionException`



```java
package hello.core.beanfind;

import hello.core.AppConfig;
import hello.core.discount.DiscountPolicy;
import hello.core.member.Member;
import hello.core.member.MemberRepository;
import hello.core.member.MemoryMemberRepository;
import org.junit.jupiter.api.Assertions;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.NoUniqueBeanDefinitionException;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import java.util.Map;

import static org.assertj.core.api.Assertions.*;
import static org.junit.jupiter.api.Assertions.*;

public class ApplicationContextSameBeanFindTest {
    AnnotationConfigApplicationContext ac = new AnnotationConfigApplicationContext(SameBeanConfig.class);


    @Test
    @DisplayName("타입으로 조회시 같은 타입이 둘 이상 있으면, 중복 오류가 발생한다.")
    void findBeanByTypeDuplication() {
        //MemberRepository bean = ac.getBean(MemberRepository.class);

        assertThrows(NoUniqueBeanDefinitionException.class,
                ()->ac.getBean(MemberRepository.class));
    }

    @Test
    @DisplayName("타입으로 조회시 같은 타입이 둘 이상 있으면, 빈 이름을 지정하면된다")
    void findBeanByName(){
        MemberRepository memberRepository = ac.getBean("memberRepository1", MemberRepository.class);
        assertThat(memberRepository).isInstanceOf(MemberRepository.class);
    }

    @Test
    @DisplayName("특정 타입을 모두 조회하기")
    void findAllBeanByType(){
        Map<String, MemberRepository> beansOfType = ac.getBeansOfType(MemberRepository.class);
        for (String key : beansOfType.keySet()) {
            System.out.println("key = " + key +" value = " + beansOfType.get(key));
        }
        System.out.println("beansOfType = " + beansOfType);
        assertThat(beansOfType.size()).isEqualTo(2);
    }

    @Configuration
    static class SameBeanConfig{

        @Bean
        public MemberRepository memberRepository1(){
            return new MemoryMemberRepository();
        }

        @Bean
        public MemberRepository memberRepository2(){
            return new MemoryMemberRepository();
        }
    }
}


```



  
