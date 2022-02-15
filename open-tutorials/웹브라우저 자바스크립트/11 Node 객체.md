# Node 객체
- Node 객체는 DOM에서 시조와 같은 역할을 하며 DOM내 최상위 객체이다

```
Node
	Document
		HTMLDocument

	CharacterData
		Text
			Comment

	Element
		HTMLElement
			HTMLLIElement
			HTMLHeadElement

	Attr
```

## 관계
- Element는 서로 부모, 자식 또는 형제 관계로 연결되어있다
- 각각의 Node가 다른 Node와 연결된 정보를 보여주는 API가 있다

```
Node.childNodes // 자식노드들을 유사배열에 담아서 리턴한다.
Node.firstChild // 첫번째 자식노드
Node.lastChild // 마지막 자식노드
Node.nextSibling // 다음 형제노드
Node.previousSibling // 이전 형제노드
Node.contains()
Node.hasChildNodes()
```

### 관계 API
- Node의 기본 제공 프로퍼티들로 관계를 파악할 수 있다
- NodeList는 유사 배열 객체로 []로 접근한다

```
// HTML
<body id="start">
<ul>
    <li><a href="./532">html</a></li> 
    <li><a href="./533">css</a></li>
    <li><a href="./534">JavaScript</a>
        <ul>
            <li><a href="./535">JavaScript Core</a></li>
            <li><a href="./536">DOM</a></li>
            <li><a href="./537">BOM</a></li>
        </ul>
    </li>
</ul>
</body>


// JS
var start = document.getElementById('start');
console.log(1, start.firstChild); // 1 #text --> body 태그와 ul 태그 사이의 공백문
var ul = start.firstChild.nextSibling;
console.log(2, ul); // 2 <ul>
console.log(3, ul.nextSibling); // 3 #text
var li = ul.firstChild.nextSibling;
console.log(4, li); // 4 <li>
console.log(5, li.parentElement); // 5 <ul>
console.log(6, li.firstChild); // 6 <a>
console.log(7, start.childNodes); // 7 NodeList(3) [text, ul, text] --> 유사 배열 객체

for (var i = 0; i < start.childNodes.length; i++)
    start.childNodes[i].style.color = 'red'; // error! #text에는 color 속성이 없으므로!
```

## 노드의 종류
- Node 객체는 최상위 객체이기 때문에 각각의 구성요소가 어떤 카테고리에 속하는 것인지를 알려주는 API를 제공한다

```
Node.nodeType // node의 타입
Node.nodeName // node의 이름(태그명)
```

### 노드 종류 API
- 노드의 종류를 알아보자

```
for (var name in Node) {
	console.log(name, Node[name]);
}

/*
ELEMENT_NODE 1
ATTRIBUTE_NODE 2
TEXT_NODE 3
CDATA_SECTION_NODE 4
ENTITY_REFERENCE_NODE 5
ENTITY_NODE 6
PROCESSING_INSTRUCTION_NODE 7
COMMENT_NODE 8
DOCUMENT_NODE 9
DOCUMENT_TYPE_NODE 10
DOCUMENT_FRAGMENT_NODE 11
NOTATION_NODE 12
DOCUMENT_POSITION_DISCONNECTED 1
DOCUMENT_POSITION_PRECEDING 2
DOCUMENT_POSITION_FOLLOWING 4
DOCUMENT_POSITION_CONTAINS 8
DOCUMENT_POSITION_CONTAINED_BY 16
DOCUMENT_POSITION_IMPLEMENTATION_SPECIFIC 32
*/

var body = $('body');

console.log(body[0].nodeType); // 1
console.log(body[0].firstChild.nodeType); // 3

console.log(body[0].nodeName); // BODY
console.log(body[0].firstChild.nodeName); // #text
```

### 재귀함수
- 다음 코드는 body 태그 하위의 모든 Element들을 탐색해서 출력하는 재귀함수 예제이다
```
function traverse(root, callback) {
    if (root.nodeType === 1) {
        callback(root);
        var c = root.childNodes;
        for (var i = 0; i < c.length; i++)
            traverse(c[i], callback) // 재귀
    }
}

traverse(document.getElementById('start'), function (elem) {
    console.log(elem)
}); 
```

## 값
- Node 객체의 값을 제공하는 API

```
Node.nodeValue
Node.textContent
```

## 변경
- Node 객체의 자식을 추가하는 방법에 대한 API

```
Node.appendChild() // 노드 추가
Node.removeChild() // 노드 삭제
```

### 노드 추가

```
// HTML
<ul id="target">
    <li>HTML</li>
    <li>CSS</li>
</ul>
<input type="button" onclick="callAppendChild();" value="appendChild()" />
<input type="button" onclick="callInsertBefore();" value="insertBefore()" />


// JS
var next = 0;
var before = 0;

function callAppendChild() {
    var target = document.getElementById('target');
    var li = document.createElement('li'); // <li></li>
    var text = document.createTextNode('JavaScript - ' + (++next)); <li>JavaScript - x</li>
    li.appendChild(text);
    target.appendChild(li); // 하위의 맨 끝에 추가
}

function callInsertBefore() {
    var target = document.getElementById('target');
    var li = document.createElement('li');
    var text = document.createTextNode('jQuery - ' + (++before));
    li.appendChild(text);
    target.insertBefore(li, target.firstChild); // 하위의 맨 뒤에 추가 --> insertBefore() : 두번째 인자로 어느 자식의 앞에 넣을것인지 결정
}
```

### 노드 제거

```
// HTML
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li id="target">JavaScript</li>
</ul>
<input type="button" onclick="callRemoveChild();" value="replaceChild()" />


// JS
function callRemoveChild() {
	var target = $('#target')[0];
	target.parentNode.removeChild(target); // parent에 접근해서 removeChild() 호출
}
```

### 노드 변경

```
// HTML
<ul>
    <li>HTML</li>
    <li>CSS</li>
    <li id="oldLi">old li</li>
</ul>
<input type="button" onclick="callReplaceChild();" value="replaceChild()" />


// JS
function callReplaceChild() {
	var newLi = document.createElement('li');
    newLi.appendChild(document.createTextNode('new li'));

    var oldLi = document.getElementById('oldLi');
    oldLi.parentNode.replaceChild(newLi, oldLi);
}
```

## jQuery 노드 변경 API
- jQuery 문서의 Manipulation 카테고리에 있다

### 추가

```
// HTML
<div class="target" style="border: black 1px solid;">
    content1
</div>

<div class="target" style="border: black 1px solid;">
    content2
</div>


// JS
$('.target').before('<div>before</div>');
$('.target').after('<div>after</div>');
$('.target').prepend('<div>prepend</div>');
$('.target').append('<div>append</div>');

/*
before
-------
prepend
content1
append
-------
after
*/
```

### 제거
- remove() : 선택된 엘리먼트를 제거
- empty() : 선택된 엘리먼트의 텍스트 노드 제거

```
// HTML
<div id="target1" style="border: black 1px solid;">
    target 1
</div>
 
<div id="target2" style="border: black 1px solid;">
    target 2
</div>
 
<input type="button" value="remove target 1" id="btn1" />
<input type="button" value="empty target 2" id="btn2" />


// JS
$('#btn1').click(function(){
    $('#target1').remove();
})
$('#btn2').click(function(){
    $('#target2').empty();
})
```

### 바꾸기
- replaceAll() : 제어 대상을 인자로 // new.replaceAll(old)
- replaceWith() : 제어 대상을 먼저 지정 // old.replaceWith(new)

```
<div class="target" id="target1">
    target 1
</div>
 
<div class="target" id="target2">
    target 2
</div>
 
<input type="button" value="replaceAll target 1" id="btn1" />
<input type="button" value="replaceWith target 2" id="btn2" 


// JS
$('#btn1').click(function(){
    $('<div>replaceAll</div>').replaceAll('#target1');
})
$('#btn2').click(function(){
    $('#target2').replaceWith('<div>replaceWith</div>');
})
```

### 복사
- clone()

```
// HTML
<div class="target" id="target1">
    target 1
</div>
 
<div class="target" id="target2">
    target 2
</div>
 
<div id="source">source</div>
 
<input type="button" value="clone replaceAll target 1" id="btn1" />
<input type="button" value="clone replaceWith target 2" id="btn2" />


// JS
$('#btn1').click(function(){
    $('#source').clone().replaceAll('#target1');
})
$('#btn2').click(function(){
    $('#target2').replaceWith($('#source').clone());
})
```

### 이동

```
// HTML
<div class="target" id="target1">
    target 1
</div>
 
<div id="source">source</div>
 
<input type="button" value="append source to target 1" id="btn1" />


// JS
$('#btn1').click(function(){
    $('#target1').append($('#source'));
})
```

## 문자열로 노드 제어

### innerHTML, outerHTML
- innerHTML : 자기 자신을 제외한 하위 항목들 제어
- outerHTML : 자기 자신을 포함한 하위 항목들 제어

```
// HTML
<ul id="target">
    <li>HTML</li>
    <li>CSS</li>
</ul>
<input type="button" onclick="get();" value="get" />
<input type="button" onclick="set();" value="set" />


// JS
function get() {
    var target = document.getElementById('target');
    alert(target.innerHTML);
}

function set() {
    var target = document.getElementById('target');
    target.innerHTML = "<li>JavaScript Core</li><li>BOM</li><li>DOM</li>";
}
```

### innerText, outerText
- 태그 제외하고 제어할 때 사용

```
function get() {
    var target = document.getElementById('target');
    alert(target.innerText);
}

function set() {
    var target = document.getElementById('target');
    target.innerText = "<li>JavaScript Core</li><li>BOM</li><li>DOM</li>";
}
```

### innerAdjustHTML

```
// HTML
<ul id="target">
    <li>CSS</li>
</ul>
<input type="button" onclick="beforebegin();" value="beforebegin" />
<input type="button" onclick="afterbegin();" value="afterbegin" />
<input type="button" onclick="beforeend();" value="beforeend" />
<input type="button" onclick="afterend();" value="afterend" />


// JS
function beforebegin() {
    var target = document.getElementById('target');
    target.insertAdjacentHTML('beforebegin', '<h1>Client Side</h1>');
}

function afterbegin() {
    var target = document.getElementById('target');
    target.insertAdjacentHTML('afterbegin', '<li>HTML</li>');
}

function beforeend() {
    var target = document.getElementById('target');
    target.insertAdjacentHTML('beforeend', '<li>JavaScript</li>');
}

function afterend() {
    var target = document.getElementById('target');
    target.insertAdjacentHTML('afterend', '<h1>Server Side</h1>');
}

/*
실행 결과

<h1>Client Side</h1>
<ul id="target">
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
</ul>
<h1>Server Side</h1>
*/
```