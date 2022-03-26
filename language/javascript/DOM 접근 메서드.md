# <b>DOM(Document Object Model)</b>
> **DOM** : *객체 지향 모델로써 구조화된 문서를 표현하는 방식*

![this is an image](https://upload.wikimedia.org/wikipedia/commons/thumb/5/5a/DOM-model.svg/1200px-DOM-model.svg.png)

- DOM은 HTML, XML 문서의 프로그래밍 interface이다.
- DOM은 자바스크립트와는 독립적인 기술 표준이다.
- DOM은 HTML, CSS와 같은 W3C의 기술의 한 종류이다.
- DOM은 문서의 구조화된 표현(structured representation)이다.

## <b>DOM tree </b>
- **문서 노드(Document Node)** : 트리의 최상위에 존재하며 각각 요소, 어트리뷰트, 텍스트 노드에 접근하려면 문서 노드를 통해야 한다. 즉, DOM tree에 접근하기 위한 시작점(entry point)이다.

- **요소 노드(Element Node)** : 요소 노드는 HTML 요소를 표현한다.
- **어트리뷰트 노드(Attribute Node)** : 어트리뷰트 노드는 HTML 요소의 어트리뷰트를 표현한다. 해당 요소 노드를 찾아 접근하면 어트리뷰트를 참조, 수정할 수 있다.
- **텍스트 노드(Text Node)** : 텍스트 노드는 HTML 요소의 텍스트를 표현한다. 텍스트 노드는 요소 노드의 자식이며 자신의 자식 노드를 가질 수 없다.

## <b>DOM 접근 메서드</b>
자바스크립트로 웹을 다루기 위해서 DOM요소에 접근해야한다. <br>
### <b>웹 페이지에서 특정 DOM요소에 접근하는 방법</b>
`document.getElementById()`
```js
// id가 title인 객체
const title = document.getElementById('title');
```
- element의 id 값을 이용해 접근하는 메서드
- 해당 id의 단일 객체를 리턴

`document.querySelector()`
```js
// id가 name인 객체
const name = document.querySelector('#name');

// class가 age인 객체
const age = document.querySelector('.age');
```
- element의 css선택자를 통해 접근하는 메서드
- 해당 css선택자를 가진 단일 객체를 리턴

`document.querySelectorAll()`
```js
// id가 name인 객체
const names = document.querySelectorAll('#name');

// class가 age인 객체
const ages = document.querySelectorAll('.age')
```
- `document.querySelector()`와 같이 css선택자를 통해 접근
- 단일 객체가 아닌 여러 객체가 담긴 리스트를 반환

`document.getElementByClassName()`
```js
// class가 age인 객체
const age = document.getElementsByClassName('age')
```
- element의 class 값을 통해 접근하는 메서드
- 해당 class를 가지는 객체를 리턴
- id와는 달리 class는 중복되는 객체가 존재할 수 있으므로 ***단일객체가 아닌 컬렉션(collection) 객체를 리턴***

`document.getElementByTagName()`
```js
// tag가 img인 객체
const images = document.getElementsByTagName('img')

// tag가 div인 객체
const tasks = document.getElementsByTagName('div')
```
- element의 tag를 통해 접근하는 메서드
- 해당 tag를 가진 객체를 리턴
- 컬렉션 객체를 리턴