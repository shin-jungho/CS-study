# ES6 문법
## <b>const & let</b>
---
`const`는 변수 선언을 위한 es6의 새로운 키워드이다. `const`는 `var`보다 강력하고 변수를 다시 할당할 수 없다. 따라서 객체와 함께 사용할 때를 제외하고는 ***변경 불가능한 변수***이다

```js
// es5 
var myBtn = document.getElementById('mybtn');

// es6
const myBtn = document.getElementById('mybtn');
```
위의 코드에서 `const`는 변경되지 않고 재할당 또한 할 수 없다. 만약 새로운 값을 할당하려고 하면 오류가 반환된다.

`let`은 새로운 값을 가질 수도 있고 재할당도 가능하므로 변경 가능한 변수가 생성된다.
```js
let name = '철수';

name = '영희';
console.log(name);

// A: 영희
```
`let`, `const`는 블럭 범위이므로 변수는 범위 내에서만 사용할 수 있고, `var`는 ***블록 범위를 가지지않아 값 할당의 영향이 블록 밖에서도 미친다.*** <br>

*자세한건 따로 정리!*

## <b>Arrow function</b>
---
화살표 함수는 코드를 더 가독성있고, 체계적이게 만든다.
```js
// es5
function myFunc(name) {
  return 'hi ' + name;
}
console.log(myFunc('철수'))
// A: 안녕 철수
---------------------------

// es 6
const myFunc = (name) => {
  return `안녕 ${name}`
}
// or
const myFunc = (name) => `안녕 ${name}`;

console.log(myFunc('철수'));
// A: 안녕 철수
```

es5의 함수보다 es6의 화살표 함수가 더 가독성이 좋고 깔끔해보인다. 또한 화살표 함수를 `map, filter, reduce`등 내장 함수와 함께 사용할 수 있다. <br>
ex)
```js
// ES5
const myArrary = ['진수', '영철', '영희', 5];

let arr1 = myArrary.map(function(item) {
	return item;
});

console.log(arr1); // 출력 => (4) ["진수", "영철", "영희", 5]

// ES6
let arr2 = myArrary.map((item) => item);

console.log(arr2); // 출력 => (4) ["진수", "영철", "영희", 5]
```
위의 코드와 같이 화살표 함수에서의 `map`함수가 더 가독성이 있다.

## <b>Template Literals</b>
---
문자열을 연결하기 위해 더하기(+) 연산자를 사용할 필요가 없고 ***백틱(`)안에 ${}를 사용해*** 문자열 내에서 변수를 사용할 수 있다. <br>
ex) 
```js
// es5
function myFunc1() {
	return '안녕' + name + '너의 나이는' + age + '살 이다!'; 
}

console.log(myFunc1('영희', 22));

// A: 안녕 영희 너의 나이는 22살 이다!
---------------------------

// es6
const myFunc = (name, age) => {
	return `안녕 ${name}, 너의 나이는 ${age}살 이다!`; 
};

console.log(myFunc1('영희', 22));
// A: 안녕 영희 너의 나이는 22살 이다!
```
## <b>Array and Object destructing(구조 분해 할당)</b>
---
비구조화를 통해 배열, 객체의 값을 새로운 변수에 더 쉽게 할당할 수 있다.
```js
// es5 문법
const contacts = {
	famillyName: '이',
	name: '영희',
	age: 22
};

let famillyName = contacts.famillyName;
let name = contacts.name;
let myAge = contacts.age;

console.log(famillyName);
console.log(name);
console.log(age);
// A: 이 / 영희 / 22
-------------------------

// es6 문법
const contacts = {
	famillyName: '이',
	name: '영희',
	age: 22
};

let { famillyName, name, age } = contacts;

console.log(famillyName);
console.log(name);
console.log(age);
// A: 이 / 영희 /22
```

es5에서는 각 변수에 각 값을 할당해야되지만, es6에서는 객체의 속성을 얻기위해 중괄호 안에 넣는다.<br>
⚠️: 속성 이름과 동일하지 않은 변수를 할당할 경우 `undefinded`가 반환된다. 예로 속성의 이름이 `name`이고 `username` 변수에 할당할경우 `undefinded`를 반환한다. <br>

항상 속성의 이르모가 동일하게 변수 이름을 지정해야되지만, 변수의 이름을 바꿀경우 `:`를 사용해 바꿀 수 있다.<br>
ex)
```js
// es6 문법
const contacts = {
	famillyName: '이',
	name: '영희',
	age: 22
};

let { famillyName, name: otherName, age } = contacts;

console.log(otherName);
// A: 영희

// 배열일 경우 중괄호를 대괄호로 바꾸면 된다.
const arr = ['광희', '지수', '영철', 20];

let [value1, value2, value3] = arr;

console.log(value1);
console.log(value2);
console.log(value3);
// A: 광희/ 지수/ 영철
```
## <b>Import and Export</b>
---
JS MVC 패턴을 사용할 때 주로 쓰이는 것으로 `export`를 하면 다른 js구성 요소에 사용할 모듈을 내보낼 수 있고, 그 모듈을 사용하기 위해 가져오는 `import`를 사용한다. <br>

ex)
```js
// es6
// detailComponent.js
export default function detail(name, age) {
  return `안녕 ${name}, 너의 나이는${age}살 이다.`
}
// homeComponent.js
import { detail } from './detailComponent'
console.log(detail('영희', 20));
// A: 안녕, 영희 너의 나이는 20살 이다.
```
위의 코드처럼 `detailComponent.js`를 `export`하고 `homeComponent.js`에서 `import`하면 `detailComponent.js`를 사용가능하다.

둘 이상의 모듈을 가져오려는 경우에 `import` 중괄호 안에 넣으면 가져올 수 있다.

## <b>Promise</b>
---
`promise`를 사용하면 비동기 메서드에서 마치 동기 메서드처럼 값을 반환할 수 있다. 다만, 최종 ***결과를 반환하는 것이 아니고 미래의 어떤 시점에 결과를 제공***하겠다는 프로미스를 반환한다.

`promise`는 다음 중 하나의 상태를 갖는다.

- 대기(*pending*): 이행하지도, 거부하지도않는 초기 상태
- 이행(*fulfilled*): 연산이 성공적으로 완료됨
- 거부(*rejected*): 연산이 실패함

대기 중인 프로미스는 값과 함계 이행할 수도, 어떤 이유(에러)로 인해 거부될 수도 있다. 이행이나 거부될 때 `promise`의 `then`메서드에 의해 대기열에 추가된 처리기들이 호출된다. 이미 이행했거나 거부된 `promise`에 처리기를 연결해도 호출되므로 비동기 연산과 처리기 연결 사이에 경합 조건은 없다.<br>
![this is an image](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise/promises.png)

## <b>Rest parameter / Spread operator</b>
--- 
<br>
1. 배열에서의 spread operator <br>
ex)

```js
var arr1 = [1,2,3]; 
var arr2 = [4,5,6]; 
arr1.push(...arr2) 

console.log(arr1); 
// A: [1,2,3,4,5,6]

var arr1 = [1,2];
var arr2 = [0, ...arr1, 3, 4];

console.log(arr2); 
// A: [0, 1, 2, 3, 4]
```
<br>
2. 함수에서의 Spread Operator
=== Rest Parameter <br>

Rest Parameter를 사용하면 함수의 파라미터로 오는 값들을 모아서 *배열* 에 집어넣는다. <br>
ex)
```js
function add(...rest) {
  let sum = 0;
  for (let item of rest) {
    sum += item;
  }
  return sum;
}

console.log( add(1) ); // 1
console.log( add(1, 2) ); // 3
console.log( add(1, 2, 3) ); // 6
```
rest parameter를 이용하면 인자의 개수에 상관없이 모든 인자를 더하는 함수를 쉽게 구현할 수 있다.<br>
***⚠️ Rest 파라미터는 항상 제일 마지막 파라미터로 있어야한다.***
```js
function addMul (...rest, method) {}
```
와 같은 방식으로 사용할 수 없다.
<br><br>
3. 객체에서의 spread operator<br>
객체에서 spread operator를 이용하는 객체의 복사 또는 프로퍼티를 업데이트 할 수 있다.<br>
ex)
```js
var currentState = { name: '철수', species: 'human'};
currentState = { ...currentState, age: 10}; 

console.log(currentState)// {name: "철수", species: "human", age: 10}

currentState = { ...currentState, name: '영희', age: 11}; 
console.log(currentState); // {name: "영희", species: "human", age: 11}
```
## <b>Class</b>
--- 
`class`는 객체 지향 프로그래밍의 핵심이며 코드를 안전하게 캡슐화할 수 있다.<br>
ex) class 만드는 코드

```js
class myClass {
	constructor() {

	}
}

// new 키워드를 사용해 class메서드와 속성에 액세스할 수 있다.

class myClass {
	constructor(name, age) {
		this.name = name;
		this.age = age;
	}
}

const user = new myClass('영희', 22);

console.log(user.name); // 영희
console.log(user.age); // 22

// 다른 class에 상속하려면 extends 키워드 후에 상속할 class의 이름을 사용

class myClass {
	constructor(name, age) {
		this.name = name;
		this.age = age;
	}

	sayHello() {
		console.log(`안녕 ${this.name} 너의 나이는 ${this.age}살이다`);
	}
}

// myClass 메서드 및 속성 상속
class UserProfile extends myClass {
	userName() {
		console.log(this.name);
	}
}

const profile = new UserProfile('영희', 22);

profile.sayHello(); // 안녕 영희 너의 나이는 22살이다.
profile.userName(); // 영희
```

> es6의 기본문법들을 정리, 자세하게는 따로 만들어서 정리할 예정