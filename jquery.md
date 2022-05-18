## 🌠 Jquery

설치

* jQuery 다운로드 : https://jquery.com/download/

  * 설치시

    ```javascript
       <script src="../scripts/jquery-3.6.0.js"></script>
    ```

  * cnd 사용시

    ```javascript
    <script src="https://code.jquery.com/jquery-3.5.0.js"></script>
    ```

    

*  vs code 에서 jquery 를 사용시 
  * 환경설정에서 html 입력후 html.json 내용을이렇게바꾸면 !! + 엔터 누르면 jquery세팅이된다

```json
{
	// Place your snippets for html here. Each snippet is defined under a snippet name and has a prefix, body and 
	// description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
	// $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the 
	// same ids are connected.
	// Example:
	"!!": {
		"prefix": "!!",
		"body": [
				"<!DOCTYPE html>",
				"<html lang='ko'>",
				"<head>",
				"<meta charset='UTF-8'>",
				"<meta name='viewport' content='width=device-width, initial-scale=1.0'>",
				"<title>$1</title>",
				"<style>$2</style>",
				"<script src='https://code.jquery.com/jquery-3.5.0.js'></script>",
				"<script>",
				"$(function () {",
				"$3",
				"});",
				"</script>",
				"</head>",
				"<body>",
				"$4",
				"</body>",
				"</html>",
	 	],
	 	"description": "Log output to console"
	 }
}
```



### 기본적인 class , id 를 추가하고 삭제하는 방법

1. `class` 추가하기

```javascript
// 문법
$('#element').addClass('[class 명]');

// 예시
$el.addClass('prd_select');
```

1. `class` 삭제하기

```javascript
// 문법
$('#element').removeClass('[class 명]');

// 예시
$el.removeClass('prd_select');
```

1. `id` 추가하기

```javascript
// 문법
$('#element').attr('id', '[id 명]');

// 예시
$el.attr('id', 'wrapBackground');
```

1. `id` 삭제하기

```javascript
// 문법
$('#element').removeAttr('id', '[id 명]');

// 예시
$el.removeAttr('id', 'wrapBackground');
```

***

### :star: $("태그 :empty")

* 태그에 text 가 비어있는 element 에 css 로 style을 변경하고 text 를 추가해보자



```javascript
<!DOCTYPE html>
<html lang='ko'>
<head>
<meta charset='UTF-8'>
<meta name='viewport' content='width=device-width, initial-scale=1.0'>
<title></title>
<style></style>
<script src='https://code.jquery.com/jquery-3.5.0.js'></script>
<script>
$(function () {
    $("td:empty").text("Was empty").css("background","rbg(255,200,200)");
});
</script>
</head>
<body>
    <table>
        <tr>
            <td>TD #0</td>
            <td></td>
        </tr>
        <tr>
            <td>TD #2</td>
            <td></td>
        </tr>
        <tr>
            <td></td>
            <td>TD#5</td>
        </tr>
    </table>

</body>
</html>
```



이런게 있구나 정도만 알아두자!
