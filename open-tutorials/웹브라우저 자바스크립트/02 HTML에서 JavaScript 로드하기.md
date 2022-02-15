# HTML에서 JavaScript 로드하기

## inline 방식
- 이벤트 처리 등에서 쓰이며 HTML 태그의 속성에 JS 코드를 삽입하는 방식
- 브라우저는 onClick 등의 속성의 값을 JS 문법으로 해석하여 실행
- 단점 : 정보와 제어의 분리가 되어있지 않다

```
<input type="button" value="button" onclick="alert('hello');"/>
```

## script 태그 이용
- script 태그를 만들어서 그 안에 JS 코드를 삽입하는 방식
- script 태그 내의 코드를 브라우저가 JS 문법으로 해석해서 실행
- 장점 : HTML 태그와 JS 코드를 분리할 수 있다(정보와 제어의 분리)
- 하지만, JS 코드가 여전히 HTML 파일 내에 존재하므로 온전히 정보의 기능을 가진 HTML이 아니라는 점에서 아쉬움이 있다

```
<input type="button" value="button" id="btn"/>

<script>
    var btn = document.getElementById('btn');
    btn.addEventListener('click', function () {
      alert('hello');
    });
</script>
```

## 외부 파일 로드
- script 코드의 src 속성에 외부 파일명을 삽입하는 방식
- 크롬 개발자 도구에서 네트워크 탭을 보면 해당 JS 파일을 다운로드 받은 것을 확인할 수 있다
- body 태그의 끝에 위치시키는 것이 좋다
- 장점
	- HTML 문서에서 JS 코드를 완전히 바깥으로 몰아낼 수 있다
	- 재사용과 유지보수에 편리하다
	- 브라우저의 캐시 덕분에 네트워크의 latency에 이점이 있다

```
<script src="example.js"></script>
```

### script 태그의 위치
- head 태그에 위치시키는 것보다 body 태그의 끝에 위치시키는 것이 좋다
- 브라우저는 script 태그를 만났을 때 해당 JS 파일을 다운로드 하고 나머지 내용을 실행하기 때문이다

```
<body>
<input type="button" value="button" id="btn"/>
<script src="example.js"></script>
</body>
```

#### head 태그에 위치 시켰을 때
- head 태그에 script 태그를 위치시키면 body의 내용들이 실행되기 전이기 때문에 에러가 발생할 확률이 높다
- window.onload를 이용해 해결할 수 있다
	- window.onload : 웹페이지의 모든 코드와 리소스들이 다운로드가 끝나서 웹페이지가 완성이 되었을 때 불리는 콜백함수
- 다만, 여전히 브라우저는 script 태그를 만났을 때 해당 JS 파일을 다운받고, 그동안 다른 HTML 코드가 해석되지 않기 때문에 사용자 입장에서는 웹페이지가 느리게 로딩되는 느낌을 받을 수 있기 때문에 여전히 body 태그의 끝에 위치시키는 것이 좋다

```
// HTML
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="example.js"></script>
</head>

// example.js
window.onload = function() {
    var btn = document.getElementById('btn');
    btn.addEventListener('click', function () {
      alert('hello');
    });
}
```