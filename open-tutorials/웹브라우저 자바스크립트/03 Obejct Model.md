# Object Model
- 개발자가 JS로 제어할 수 있도록 브라우저가 자신의 여러 구성 요소들을 객체로 제공하는 것

## 객체화
- HTML의 태그를 JS로 제어하려면 JS가 제어할 수 있는 Object의 형태여야 하고, 이 일은 브라우저가 HTML 코드를 해석하면서 맡는다
- 브라우저가 태그를 객체로 만들어주고, 이 객체를 JS에서 참조해서 제어한다(태그, 클래스, id 값을 이용해서)

```
// HTML
<img src="...">

// JS
var imgs = document.getElementsByTagNmae('img');
imgs[0].style.width = '300px';
```

## window
- 전역객체, 창 그 자체
1. DOM(Document Object Model)
	- document
	- ...
2. BOM(Browser Object Model)
	- navigator
	- screen
	- location
	- frames
	- history
	- XMLHttpRequest
3. JSC(JavaScript Core)
	- Object
	- Array
	- Function
	- ...