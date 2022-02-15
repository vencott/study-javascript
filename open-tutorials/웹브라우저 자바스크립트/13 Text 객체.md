# Text 객체
- Text 객체는 텍스트 노드에 대한 DOM 객체로 CharacterData를 상속받는다
- 주목할 것은 DOM에서는 공백이나 줄바꿈도 텍스트 노드이다

```
// HTML
<p id="target1"><span>Hello world</span></p>
<p id="target2">
    <span>Hello world</span>
</p>


// JS
var t1 = document.getElementById('target1').firstChild;
var t2 = document.getElementById('target2').firstChild;
 
console.log(t1.firstChild.nodeValue); // Hello world
try{
    console.log(t2.firstChild.nodeValue);   
} catch(e){
    console.log(e); // TypeError {stack: (...), message: "Cannot read property 'nodeValue' of null"}
}
console.log(t2.nextSibling.firstChild.nodeValue); // Hello world
```

## 값 API
- nodeValue
- data

```
// HTML
<ul>
    <li id="target">HTML</li>
    <li>CSS</li>
    <li>JavaScript</li>
</ul>


// JS
var t = document.getElementById('target').firstChild;
console.log(t.nodeValue); // HTML
console.log(t.data); // HTML
```

## 조작 API
- appendData()
- deleteData()
- insertData()
- replaceData()
- substringData()