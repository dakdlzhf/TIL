# 🔯 IoC 와 DI

## **IoC(Inversion of Control, 제어의 역전)**

`IoC(Inversion of Control)`란 "제어의 역전" 이라는 의미로, 말 그대로 **메소드나 객체의 호출작업을 개발자가 결정하는 것이 아니라, 외부에서 결정되는 것을 의미**한다.

`IoC`는 **제어의 역전이라고 말하며, 간단히 말해 "제어의 흐름을 바꾼다"** 라고 한다.

객체의 **의존성을 역전시켜 객체 간의 결합도를 줄이고 유연한 코드를 작성**할 수 있게 하여 **가독성 및 코드 중복, 유지 보수를 편하게** 할 수 있게 한다.

기존에는 다음과 순서로 객체가 만들어지고 실행되었다.

1. 객체 생성
2. 의존성 객체 생성
   *클래스 내부에서 생성*
3. 의존성 객체 메소드 호출

하지만, 스프링에서는 다음과 같은 순서로 객체가 만들어지고 실행된다.

1. 객체 생성
2. 의존성 객체 주입
   *스스로가 만드는것이 아니라 제어권을 **스프링에게 위임하여 스프링이 만들어놓은 객체를 주입**한다.*
3. 의존성 객체 메소드 호출

**스프링이 모든 의존성 객체를 스프링이 실행될때 다 만들어주고 필요한곳에 주입**시켜줌으로써 **Bean들은 `싱글턴 패턴`의 특징**을 가지며,

**제어의 흐름을 사용자가 컨트롤 하는 것이 아니라 스프링에게 맡겨 작업을 처리**하게 된다.


 

아래 코드를 보면 BestStar 생성자에서 Star 클래스와의 의존관계를 애플리케이션 단에서 직접 설정하고 있다.

 

**💡 의존관계**
서로 다른 객체간에 레퍼런스 참조가 되어 있다는 말이다. 

```
public class BestStar {

    private Star star;

    public BestStar(){
        star = new Star();
        // BestStar 생성자에서 Star 클래스와의 의존관계를 애플리케이션 단에서 직접 설정하고 있다.
    }
}
```

그런데 스프링이 제공하는 @Autowired 어노테이션을 사용함으로써 개발자가 직접 의존관계를 설정해주는 코드가 사라지고 프레임워크에 BestStar, Star 오브젝트 의존관계의 제어권을 맡길 수 있게 된 것이다.

```
public class BestStar {

    @Autowired
    private Star star;

}
```




 

### **IoC가 필요한 이유? - 객체지향 원칙을 잘 지키기 위해**

객체를 관리해주는 프레임워크와 내가 구현 하고자 하는 부분으로 역할과 관심을 분리해 응집도를 높이고 결합도를 낮추며, 이에 따라 변경에 유연한 코드를 작성 할 수 있는 구조가 될 수 있기 때문에 제어를 역전한 것이다.

 

------

## **DI(Dependency Injection, 의존관계 주입)**

**외부로부터 메모리에 올라가있는 인스턴스의 레퍼런스를 인터페이스 타입의 파라미터로 의존관계를 설정하는것**을 말한다. 스프링에선 IoC라는 용어만 가지고는 개념이 너무 추상적이라 그 핵심을 짚는 용어가 필요했는데, 이때 몇몇 사람들의 제안으로 만든 용어가 바로 DI인 것이다.

`DI(Dependency Injection)`란 **스프링이 다른 프레임워크와 차별화되어 제공하는 의존 관계 주입 기능**으로,
**객체를 직접 생성하는 게 아니라 외부에서 생성한 후 주입 시켜주는 방식**이다.

**DI(의존성 주입)를 통해서 모듈 간의 결합도가 낮아지고 유연성이 높아진다.**

![img](https://velog.velcdn.com/images%2Fgillog%2Fpost%2F08489bda-549e-4dae-851b-8ae1734bf85e%2F21373937580AEF9B37.jpg)

첫번째 방법은 A객체가 B와 C객체를 New 생성자를 통해서 직접 생성하는 방법이고,

두번째 방법은 **외부에서 생성 된 객체를 setter()를 통해 사용하는 방법**이다.

이러한 두번째 방식이 의존성 주입의 예시인데,
`A 객체`에서 **`B, C객체`를 사용(의존)할 때** `A 객체`에서 **직접 생성 하는 것이 아니라** **`외부(IOC컨테이너)`에서 생성된 `B, C객체`를 조립(주입)시켜 `setter` 혹은 `생성자`를 통해 사용하는 방식**이다.

![img](https://velog.velcdn.com/images%2Fgillog%2Fpost%2F41f2eb24-fce2-4b7e-b9ac-d5c3ce97d213%2F22535642580C4AF12C.jpg)

**스프링에서는 객체를 `Bean`** 이라고 부르며, 프로젝트가 실행될때 사용자가 Bean으로 관리하는 객체들의 생성과 소멸에 관련된 작업을 자동적으로 수행해주는데 객체가 생성되는 곳을 스프링에서는 `Bean 컨테이너` 라고 부른다.

# 

------

### **의존관계 주입 방법**

#### **필드를 이용한 의존관계 주입 (Field Injection)**

```
@Service
public class StudentServiceImpl implements StudentService {

    @Autowired
    private CourseService courseService;

    @Override
    public void studentMethod() {
        courseService.courseMethod();
    }

}
```

 

#### **setter() 메서드를 이용한 의존관계 주입 (Setter Injection)**

```
@Service
public class StudentServiceImpl implements StudentService {

    private CourseService courseService;

    @Autowired
    public void setCourseService(CourseService courseService) {
        this.courseService = courseService;
    }

    @Override
    public void studentMethod() {
        courseService.courseMethod();
    }
}
```

 

 

#### **생성자를 이용한 의존관계 주입 (Constructor Injection)**

```
@Service
public class StudentServiceImpl implements StudentService {

    private final CourseService courseService;

    @Autowired
    public StudentServiceImpl(CourseService courseService) {
        this.courseService = courseService;
    }

    @Override
    public void studentMethod() {
        courseService.courseMethod();
    }
}
```
 
 


 
