# 🔯 IoC 와 DI

## **IoC(Inversion of Control, 제어의 역전)**

오브젝트 생성, 관계설정, 사용, 제거 등 **오브젝트 전반**에 걸친 모든 **제어권**을 애플리케이션이 갖는게 아니라 **프레임워크의 컨테이너에게 넘기는 개념**을 말한다. 참고로 스프링 프레임워크 만의 개념이 아니다.

스프링에서는 저 '오브젝트'를 '빈(Bean)'이라고 칭한다.

 

💡 빈(Bean)에 대해서는 추후 여러번에 걸쳐 별도로 포스팅할테니 참고 바란다.

 

아래 코드를 보면 BestStar 생성자에서 Star 클래스와의 의존관계를 애플리케이션 단에서 직접 설정하고 있다.

 

**💡 의존관계**
서로 다른 객체간에 레퍼런스 참조가 되어 있다는 말이다. 

```
public class BestStar {

    private Star star;

    public BestStar()
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

 

💡 추후 @Autowired 어노테이션이 스프링에서 어떻게 추상화돼있고 그 내부에서 어떤 동작원리를 갖는지 디버깅 스택 트레이싱을 해보며 분석한 글을 포스팅 할테니 참고바란다.

먼저 궁금하신 분들은 Github에 토이프로젝트로 정리한 [이 링크](https://github.com/HwangWonGyu/news/pull/20#discussion_r566839551)를 참고바란다.

 

### **IoC가 필요한 이유? - 객체지향 원칙을 잘 지키기 위해**

객체를 관리해주는 프레임워크와 내가 구현 하고자 하는 부분으로 역할과 관심을 분리해 응집도를 높이고 결합도를 낮추며, 이에 따라 변경에 유연한 코드를 작성 할 수 있는 구조가 될 수 있기 때문에 제어를 역전한 것이다.

 

💡 추후 객체지향 3요소, 5원칙에 대해 별도로 포스팅 후 링크를 걸어둘테니 참고 바란다. 

------

## **DI(Dependency Injection, 의존관계 주입)**

**외부로부터 메모리에 올라가있는 인스턴스의 레퍼런스를 인터페이스 타입의 파라미터로 의존관계를 설정하는것**을 말한다. 스프링에선 IoC라는 용어만 가지고는 개념이 너무 추상적이라 그 핵심을 짚는 용어가 필요했는데, 이때 몇몇 사람들의 제안으로 만든 용어가 바로 DI인 것이다.

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

 


 
