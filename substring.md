## :rocket:  JavaSciprt ( substing ( ) )





* substring() 메소드는 string 객체의 시작 인덱스 부터 종료 인덱스 전! 까지의 문자열의 부분 문자열을

  반환 한다

```javascript
str.substring(indexStart[, indexEnd])  	
```

* indexStart = 반환 받을 문자열의 시작 인덱스

* indexEnd = 반환 받을 문자열의 종료 인덱스

  

```javascript
	<script>
        document.write(str.substring(0, 3) + '<br>');
        // 0 index 부터 index 3 전까지 반환
        document.write(str.substring(3, 6) + '<br>');
        //3 index 부터 index 6 전까지 반환
        document.write(str.substring(7) + '<br>');
        // 7 index 부터 문자열 끝까지 반환
        document.write(str.lastIndexOf('가나다') + '<br>');
    </script>

```

### :star:  substring() 메소드를 이용한 빈문자열 제거하기!



```javascript
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <script>
        function trimSpace(f) {
            let str = f.txtData.value;
            console.log(str);
            for (let i = 0; i < str.length; i++) {
                if (str.charAt(i) == ' ' ) {
                    str = str.substring(0, i) + str.substring(i + 1);
                }
            }
            f.txtData2.value = str;
        }
    </script>
</head>

<body>
    <form name="myform">
        원본 문자열 : <input name="txtData" type="text" size="60" maxlength="60">
        <a href="javascript:trimSpace(myform)"><b>문자열 공백지우기</b></a>
        <br><br>
        공백 제거 문자열:<input name="txtData2" type="text" size="60" maxlength="60">
    </form>
</body>

</html>
```



* substring ( ) 메서드를 이요하여 input 태그에 입력된 value 값을 a 태그를 클릭했을때

​       trimSpace()  가 동작하여 input 의 value 값을 str 에 저장후 for 반복문을통해 str을 charAt 으로

​	   한글자씩 "  " 공백문자를 찾아서

``` javascript
 str = str.substring(0, i) + str.substring(i + 1);
```

* str 문자열에 0 부터 i 전까지 의 문자열과 + 공백문자열이 위치한 i 뒤의 문자열을 합치기위해  i + 1 을해줬다.
  * str 에 공백문자열이 제거된 문자열이 다시저장되어 str을 name 이 txtData2 의 value에 넣어준다.

