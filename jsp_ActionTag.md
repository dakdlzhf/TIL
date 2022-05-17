## :star2:Forward 사용할때  jsp action 태그를 이용하면 편하다

* jsp 에 action 태그를  알기전까진 이렇게 포워딩 코드를 작성했다.
  * RequestDispatcher 객체는 브라우저의 요청을 제어할수있는 객체이다.

```jsp
	RequestDispatcher dispatcher = request.getRequestDispatcher(url);
	dispatcher.forward(request,response);
```

* 코드를 최적화 하여 체이닝하여 사용하여도 아래와같다.

```jsp
request.getRequestDispatcher("경로").forward(request,response)
```



* jsp 에 action 태그를 사용해보자 나중에 MVC 패턴을 이용하기전까진 jsp 에서 짱!

```jsp
<jsp:forward page=" 경로 "/>
```

RequestDispatcher 객체를 이용한 포워딩 보다 훨씬 간결하고 편하니까 사용해 보자!!

