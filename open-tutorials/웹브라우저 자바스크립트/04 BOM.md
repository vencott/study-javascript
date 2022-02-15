# BOM
- Browser Object Model
- 웹브라우저를 제어하기 위해서 브라우저가 제공해주는 객체들
- BOM을 통해서 JS는 웹브라우저의 다양한 정보를 얻어낼 수 있다

## 전역객체 Window
- window 객체는 window 식별자를 통해서 참조한다
- window 자체가 전역 객체이므로 생략이 가능하다

```
window.alert('hello');
alert('hello');
```

- 어느 객체나 함수에 소속되지 않고 그냥 정의하는 모든 것들은 window의 프로퍼티가 된다

```
var a = 1;
console.log(a);
console.log(window.a);

function foo() {
    alert('hello');
}
foo();
window.foo();
```

## 사용자와 커뮤니케이션 하기
- HTML은 form을 통해서 사용자와 커뮤니케이션 할 수 있는 기능을 제공한다
- JS는 사용자와 정보를 주고 받을 수 있는 간편한 수단을 제공한다

### alert(경고창)
- 사용자에게 정보를 제공하거나 디버깅 할 때 사용한다
- 경고창의 확인을 클릭하기 전까지는 다른 코드를 실행하지 않는다

```
alert('1'); // 확인 클릭 전까진 아래 코드 실행 안함
alert('2');
alert('3');
```

### confirm(확인)
- 확인과 취소의 2개의 버튼이 있다
- true/false의 값을 반환한다

```
var result = confirm('ok?');
alert(result ? 'ok clicked' : 'cancel clicked');
```

### prompt
- 사용자가 입력한 값을 얻어서 JS가 이용할 수 있는 기능

```
var result = prompt('What is your name?');
if (result)
    alert("Your name is " + result);
```

## Location 객체
- 현재 브라우저 창에 열려있는 문서의 URL과 관련된 객체

### 현재 윈도우의 URL 알아내기

```
console.log(location.href); // 추천
console.log(location.toString());
```

### URL Parsing

```
http://opentutorials.org:80/module/1?id=1#hash

http: 				- protocol
opentutorials.org 	- host
80 					- port
/module/1 			- pathname
?id=1 				- search
#hash 				- hash

console.log(location.protocol); // http:
console.log(location.host); // opentutorials.org
console.log(location.port); // 80(생략)
console.log(location.pathname); // /module/1
console.log(location.search); // ?id=1
console.log(location.hash); // #hash
```

### URL 변경하기
- location 객체는 현재 페이지의 URL 정보만 얻어오는 것이 아니라, 그것을 수정할 수 있다
- location 객체 수정 시 해당 페이지로 이동하고 리로드된다

```
if (confirm('Go to Naver?'))
    location.href = 'https://www.naver.com'; // 추천

if (confirm('Go to Naver?'))
    location = 'https://www.naver.com';
```

- 단순하게 현재 페이지를 리로드 할 수도 있다

```
if (confirm('Reload?'))
    location.reload();

// 아래의 원리로 동작
// location.href = location.href;
```

## Navigator 객체
- 브라우저의 정보를 제공하는 객체
- 호환성 문제등을 위해서 사용한다

### Cross Browsing(크로스 브라우징)
- ie, chrome, firefox등 많은 브라우저가 있다
- W3C(HTML, CSS), ECMA(JS) 등의 표준 기관에서 정의한 스펙에 따라 브라우저 개발
- 하지만 완벽히 같을 수 없으므로 브라우저마다 코드가 다르게 동작할 수 있다
- 웹개발자는 브라우저마다 개별적인 처리를 해줘야 하고, 이때 필요한 것이 navigator 객체이다

### appName

```
console.dir(navigator.appName);
// IE - Microsoft Internet Explorer
// 파이어폭스, 크롬 등 - Nescape
```

### appVersion

```
console.dir(navigator.appVersion);
// 운영체제, HTML 레이아웃 엔진, 브라우저 이름과 버전
// 5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36
```

### userAgent
- 웹브라우저가 웹서버에 요청할 때 보내는 웹브라우저에 대한 정보
- HTTP 헤더에 포함

```
console.dir(navigator.userAgent);
// Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36
```

### platform
- 브라우저가 동작하고 있는 운영체제

```
console.dir(navigator.platform);
// MacIntel
```

### 기능 테스트
- Object.keys 라는 메소드는 ECMAScript5에 추가되었기 때문에 오래된 자바스크립트에는 없을 수도 있다
- 있을 경우 브라우저의 기능을 그대로 사용하고, 없을 경우 만들어서 사용하는 코드를 예로 살펴보자

```
// From https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/keys

if (!Object.keys) { // Object에 keys라는 메소드가 없다면
  Object.keys = (function () {
    'use strict';
    var hasOwnProperty = Object.prototype.hasOwnProperty,
        hasDontEnumBug = !({toString: null}).propertyIsEnumerable('toString'),
        dontEnums = [
          'toString',
          'toLocaleString',
          'valueOf',
          'hasOwnProperty',
          'isPrototypeOf',
          'propertyIsEnumerable',
          'constructor'
        ],
        dontEnumsLength = dontEnums.length;
 
    return function (obj) {
      if (typeof obj !== 'object' && (typeof obj !== 'function' || obj === null)) {
        throw new TypeError('Object.keys called on non-object');
      }
 
      var result = [], prop, i;
 
      for (prop in obj) {
        if (hasOwnProperty.call(obj, prop)) {
          result.push(prop);
        }
      }
 
      if (hasDontEnumBug) {
        for (i = 0; i < dontEnumsLength; i++) {
          if (hasOwnProperty.call(obj, dontEnums[i])) {
            result.push(dontEnums[i]);
          }
        }
      }
      return result;
    };
  }());
}
```

## 창 제어

### window.open

```
window.open(); // 새 탭에 빈 창을 띄운다
window.open('index.html'); // 새 탭에 index.html을 띄운다
window.open('index.html', '_self'); // 현재 탭에 index.html을 띄운다
window.open('index.html', '_blank'); // 새 탭에 index.html을 띄운다
window.open('index.html', 'name'); // 탭에 이름을 붙여서 open 최초실행시엔 name이란 이름의 새 탭을, 재실행 했을 때 동일한 이름의 탭이 있다면 그곳에 index.html을 띄운다
window.open('index.html', '_blank', 'width=200, height=200, resizable=no'); // 세번째 인자는 새 탭이 아닌 새 창을 띄우면서, 그 모양과 관련된 속성이 온다

```

### 상호작용

```
<body>
    <input type="button" value="open" onclick="winopen();" />
    <input type="text" onkeypress="winmessage(this.value)" />
    <input type="button" value="close" onclick="winclose()" />
    <script>
    function winopen(){
        win = window.open('demo2.html', 'ot', 'width=300px, height=500px');
    }
    function winmessage(msg){
        win.document.getElementById('message').innerText=msg;
        // 새 창의 message tag는 기존에 미리 작성해놨다고 가정
    }
    function winclose(){
        win.close();
    }
    </script>
</body>
```

- win이란 객체에 새 창을 연 뒤 이를 할당하고, text input tag에 글자를 입력하면 onkeypress callback이 호출되어 새 창의 message tag에 text input tag에 입력한 문자를 띄우게 된다
-window.close는 창을 닫는 메소드이다

### 보안(팝업차단)
- 사용자와의 인터렉션 없이 창을 열려고 하면(window.open 호출) 팝업이 차단된다

```
<input type="button" value="btn" id="btn" onclick="open('index.html')"> // 팝업 차단 x

<script>
    open('index.html'); // 팝업 차단
</script>
```