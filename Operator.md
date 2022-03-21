# <b>연산자</b>

## <b>우선 연산자 표</b>
![this is an image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=http%3A%2F%2Fcfile10.uf.tistory.com%2Fimage%2F264ACE4658DE886F333F27)

- 비트이동 연산자 a << b, a >> b : a의 비트를 >>(우), <<(좌)으로 b만큼 비트 이동

- 비트논리 연산자 : and, or xor의 논리갑 반환
   - a & b : a, b가 둘 다 참(1)일 때만 참(1)반환, 그 외에는 거짓(0)
   - a | b : a, b가 둘 다 거짓(0)일 때만 거짓(0)을 반환, 그 외에는 참(1)
   - a ^ b : a와 b가 서로 다를 때 참(1)을 반환, 그 외에는 거짓(0)

- typeof 연산자 : <br>
```js
var myFun = new Function("5 + 2");
var shape = "round";
var size = 1;
var foo = ['Apple', 'Mango', 'Orange'];
var today = new Date();

// 일때

typeof myFun;     // "function" 반환
typeof shape;     // "string" 반환
typeof size;      // "number" 반환
typeof foo;       // "object" 반환
typeof today;     // "object" 반환
typeof dontExist; // "undefined" 반환

typeof true // "boolean" 반환
typeof null // "object"반환
```

### <b>참고</b>
- <a href="https://developer.mozilla.org/ko/docs/Web/JavaScript/Guide/Expressions_and_Operators">***연산자 모음***</a>

