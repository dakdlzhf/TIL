## :rocket:  Javascript Event ! input 태그와 onkeyup 

* input 태그에 값을 입력하고 실시간으로 출력하는 onkeyup () 
  * onkeyup 함수에 기능처리 함수를 만들어서 넣어주면 입력과 동시에 출력이가능하다. 

### :star2: onkeyup( ) 사용예



```javascript
<input type="text" id="a" onkeyup="change(this.value)">
```

```javascript
<script>
        function change() {
            const input = document.getElementById('a').value;
            document.getElementById('panel').innerHTML = input;
        }
</script>
```

* input 태그에 값이 변경됨을 감지하는 onchange( ) 
  * onchange 함수는 입력이 끝나거나 해당 input 창에서 벗어날경우 동작하는 함수이다.
  * button 과 잘사용되지만 꼭 button 태그가 있어야 동작하지는 않는다. input 태그 만 벗어나면 동작!

### :star2: onchange( ) 사용예

```javascript
<input type="text" id="a" onchange="change(this.value)">
<input type="button" value="버튼">
```


