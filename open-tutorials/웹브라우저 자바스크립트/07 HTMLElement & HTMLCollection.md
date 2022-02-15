# HTMLElement & HTMLCollection

```
var activeLi = document.getElementById('active');
console.log(activeLi.constructor.name); // HTMLLIElement --> 객체
var lis = document.getElementsByTagName('li');
console.log(lis.constructor.name); // HTMLCollection --> 유사배열객체
```

## HTMLElement
- 리턴 결과가 하나인 경우에 사용된다
- 하나의 Element를 추상화한 객체

```
// HTML
<a id="anchor" href="http://opentutorials.org">opentutorials</a>
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li id="list">JavaScript</li>
</ul>
<input type="button" id="button" value="button" />


// JS
var li = document.getElementById('list'); // HTMLElement 반환
console.log(li.constructor.name); // HTMLLIElement

var anchor = document.getElementById('anchor');
console.log(anchor.constructor.name); // HTMLAnchorElement

var button = document.getElementById('button');
console.log(button.constructor.name); // HTMLInputElement
```

## HTMLCollection
- 리턴 결과가 복수인 경우에 사용된다
- 복수의 Element 추상화 객체들을 담은 유사배열 객체

```
// HTML
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li id="list">JavaScript</li>
</ul>


// JS
console.group('before'); // 콘솔 제어 팁 : 일련의 로그들을 그룹화
var lis = document.getElementsByTagName('li'); // HTMLCollection 반환
for (var i = 0; i < lis.length; i++)
    console.log(lis[i]);
console.groupEnd();

console.group('after');
lis[1].parentNode.removeChild(lis[1]); // lis에 실시간 반영
for (i = 0; i < lis.length; i++)
    console.log(lis[i]);
console.groupEnd();
```

## DOM Tree
- 모든 Element는 HTMLElement의 자식이다
- Element는 Node의 자식이다
- Node는 Object의 자식이다
- 이러한 관계를 DOM Tree라고 한다