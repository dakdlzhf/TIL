## JSON Parser 테스트 사이트

* JSON 파일이 잘못된건지 오타는 없는지 눈으로 확인하는것보다 아래 사이트에서 확인해보자
  * https://jsonparser.org/ <-- 사이트 에들어가서 왼쪽에 JSON 파일을 입력하고 JSON Parser 버튼!
  * JSON Parser 가 완료된 데이터를 다시 JSON 데이터로 (문자열) 변환  JSON Format 버튼!!

```javascript
{
  "code": "success",
  "data": {
    "member": [
      {
        "name": "홍길동",
        "id": "coder",
        "sno": "a01",
        "age": 20
      },
      {
        "name": "아로미",
        "id": "dev",
        "sno": "a02",
        "age": 50
      }
    ]
  }
}
```

JSON Parser 버튼을 누르면 !  :arrow_lower_left:

```javascript
	
	object		{2}
		
code	:	success
		
	data		{1}
		
	member		[2]
		
	0		{4}
		
name	:	홍길동
		
id	:	coder
		
sno	:	a01
		
age	:	20
		
	1		{4}
		
name	:	아로미
		
id	:	dev
		
sno	:	a02
		
age	:	50

```

JSON 데이터 관련 오류가 생겼을때 우선 JSON 데이터부터 확인해보자!!
