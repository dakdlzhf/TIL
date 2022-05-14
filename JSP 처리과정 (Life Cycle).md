# :star: JSP 라이프 사이클 (처리 과정)



* jsp 파일에 코드를 작성하고 클리어언트의 .jsp파일 요청시 톰캣의 서비스 과정을 알아보겠다.

1) 브라우저에서 jsp요청이 들어온다 ex01.jsp 파일 보여줘!

2) 톰캣은 브라우저의 요청 파일 ex01.jsp 파일을 찾은후 있다면 처리한다.

   1) 이때 !! jsp 파일을 ->   톰캣 이  .java 파일로 생성하고 -> java 파일을 다시 컴파일하여  .class 파일로 만들면 컴파일된 .class 파일로 눈에보이지는 않지만 new ex01.jsp() 처럼 객체를 생성했다고 생각하면된다 .  이 생성된 객체 안에는 jspInit () , jspDestroy() 같은 함수를 사용할수있다 , 

   2) <u>jspInit() 함수는 최초에 한번실행되고 초기값을 셋팅한후 메모리상에 제거되기전까지는 계속 상주하고 있는 메서드 !</u>

   3) 이때 브라우저가 새롭게 또 요청이 들어오면 이미 객체가 있기때문에, jspService () 라는 함수가 브라우저에게 응답만 해준다!

   4) 동일하지않은 요청이 들어오면 jspDestroy () 함수는 객체가 제거될때 호출이 된다.!

      

***



* :100: 결국 ! jsp 파일은 java 파일로 생성이된다!

* jspService ( ) 함수에 내부에는 스크립트릿  <%  %>  , java 코드가 들어 있는데,  스크립트릿 에 작성된 java 코드가 jspService 내부에서 작동된다.

## :rocket: 요약

이클립스 jsp 파일 -->  톰캣이  java 파일 생성 --> 컴파일 된 class 파일 --> new 객체 생성 

--> 객체안에 있는 jspinit() 메서드 호출 1) 동일한요청이들어오면 jspService () 메소드 가 호출되고 처리 2) 동일하지 않은 요청이나 ,jsp 파일이 수정이 될경우 jspDstroy () 메소드 호출뒤 객체 제거 

이때 jsp 파일이 수정되면 톰캣은 다시 jsp 파일을 java 파일로 만들고 class 파일로 컴파일!!

-->동일한 과정으로 다시 객체 생성 후 jspInit() 호출뒤 jspService () 동작 하여 스크립트릿 부분을 처리 후 메모리에 상주!

:star: HTML 코드는 그대로 브라우저에 응답

:star: JSP 코드는 톰캣 서버에서 Life Cycle 을 통해 처리된후 브라우저에 응답

:star: **선언문 에서 작성된 변수는 객체 안에 멤버 변수라 jsp 가 수정되기전까진 값 유지!**

:star: **스크립트릿 에서 작성된 변수는 jspService () 함수내에 지역변수라 호출시마다 값이 초기화!**

### 직접 코드를 살펴보자

```javascript
<body>
	<%! // class 파일이생성되면 메모리에 객체를 생성 이때 객체의 멤버변수 ,멤버메서드 를 정의하는 선언문
    
	private int num1 = 0; //객체 내부 전역변수( 멤버변수 )

	public void jspInit() { //오버라이딩

		System.out.println("jspInit() 호출됨");
	}

	public void jspDestroy() { //오버라이딩
		System.out.println("jspDestroy() 호출됨");
        
	}%>

	<% // 생성된 객체의 jspServic ( ) 함수 내부 코드 스크립트릿 
	
	int num2 = 0; // 함수 내부 지역변수
	num1++;
	num2++;
	
	
	%>
        
	<ul>
		<li>num1 : <%= num1 %> </li> <!-- 표현식 --> 
		<li>num2 : <%= num2 %> </li>
	</ul>

</body>
```

* 톰캣서버를 동작하여 jsp 요청 을 하면 num1 의 값은 증가하고 num2 의값은 증가하지않는다
  * 다만 jsp 파일이 수정된다면 객체를 제거후 다시 생성하기떄문에 멤버변수인 num1 도 초기화된다.

