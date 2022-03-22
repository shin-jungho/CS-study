# <b>Generics</b>
> 💥 ***타입을 마치 함수의 파라미터처럼 사용하는 것***

ex)
```ts 
// 제네릭 x
function getText(text) {
  return text;
}

getText('hi'); // 'hi'
getText(10); // 10
getText(true); // true

// 제네릭 ㅇ
function getText<T>(text: T): T {
  return text;
}

getText<string>('hi');
getText<number>(10);
getText<boolean>(true);
```
### `getText<string>('hi')`의 제네릭의 동작

```ts
function getText<string>(text: T): T {
  return text;
}
// getText()함수를 호출할때 제네릭(함수에서 사용할 타입) 값으로 string을 넘겼기 때문

getText<string>('hi');
// 함수 인자로 'hi'라는 값을 아래와 같이 넘기게 되면

function getText<string>(text: string): string {
  return text;
} 
// 함수는 입력 값의 타입이 string이면서 반환 값 타입도 string이어야 한다.
```

## <b>제네릭을 사용하는 이유</b>
```ts
// 인자를 하나 넘겨 받아 반환해주는 함수
function logText(text: string): string {
  return text;
}
```
위 코드에서 인자와 반환 값 모드 `string`으로 지정되 있지만 만약 여러 타입을 허용하고 싶다면 `any`를 사용할 수 있다.
```ts
function logText(text: any): any {
  return text;
}
```
`any`로 타입을 정할 경우 타입 검사를 안하기 때문에 ***함수의 인자로 어떤 타입이 들어갔고 어떤 값이 반환되는지는 알 수 없다.***

따라서 이러한 문제를 해결하는 것이 **제네릭**이다.

```ts
function logText<T>(text: T): T {
  return text;
}
```
함수 이름 뒤에 `<T>`를 추가하고 함수의 인자와 반환값에 모두 `T`라는 타입을 추가하면 된다.

```ts
// 위의 함수 호출방법 2가지
// 1.
const text = logText<string>('hi');

// 2. -> 가독성, 코드 짧아서 많이쓰임
const text = logText('hi');
```

## <b>제네릭 타입 변수</b>
> 앞에서 배운 내용으로 제네릭을 사용하면 **컴파일러에서 인자에 타입을 넣어달라는 에러가 뜬다.**

### 함수의 인자로 받은 값의 `length`를 확인하고 싶다면 어떻게 ??
```ts
// 1. 
function logText<T>(text: T): T {
  console.log(text.length);
  return text;
}
// 컴파일러에서 에러난다. 왜냐면 text에 .length가 있다는 단서가 없기 때문이다.

// 2.
function logText<T>(text: T[]): T[] {
  console.log(text.length); // 제네릭 타입이 배열이기 때문에 length를 허용한다.
  return text;
}
```
2번째 코드는 `T`라는 변수 타입을 받고, 인자 값으로 배열 형태의 `T`를 받는다. 

이러한 방식으로 제네릭을 사용하면 유연한 방식으로 함수 타입을 정의할 수 있다.

2번 코드를 명시적으로 바꾸면
```ts
function logText<T>(text: Array<T>): Array<T> {
  console.log(text.length);
  return text;
}
```
## <b>제네릭 인터페이스</b>

```ts
function logText<T>(text: T): T {
  return text;
}
// 1.
let str: <T>(text: T) => T = logText;

// 2.
let str: {<T>(text: T): T} = logText;
// 1, 2는 같은 코드이다.
```
위의 코드를 제네릭 인터페이스 코드로 변경하면
```ts
interface GenericsLogTextFn {
  <T>(text: T): T;
}
function logText<T>(text: T): T {
  return text;
}
let myString: GenericsLogTextFn = logText; //

// 인터페이스에 인자 타입을 강조할 경우 
interface GenericsLogTextFn<T> {
  (text: T): T;
}
function logText<T>(text: T): T {
  return text;
}
let myString: GenericsLogTextFn<string> = logText;
```
### ***⚠️ enum, namespace는 제네릭 생성 불가!***

## <b>제네릭 클래스</b>
```ts
class GenericMath<T> {
  pi: T;
  sum: (x: T, y: T) => T;
}

let math = new GenericMath<number>();
```
제네릭 클래스를 선언할 때 클래스 이름 오른쪽에 <T>를 붙여준다. 그리고 해당 클래스로 인스턴스를 생성할 때 타입에 어떤 값이 들어갈지 지정하면 된다.
> *<span style="gray">인스턴스란? 일반적으로 실행 중인 임의의 프로세스, 클래스의 현재 생성된 객체를 말한다.</span>*

## <b>제네릭 제약 조건</b>
제네릭 함수에 어느정도 타입 힌트를 줄 수 있는 방법
```ts
function logText<T>(text: T): T {
  console.log(text.length);
  return text;
}
```
인자 타입에 선언한 T는 아직 어떤 타입인지 구체적으로 정의하지 않았기 때문에 length 코드에서 오류가 난다.

이럴 경우 해당 타입을 정의하지 않고도 `length` 속성 정도는 허용하려면 이 와 같이 작성한다.
```ts
interface LengthWise {
  length: number;
}

function logText<T extends LengthWise>(text: T): T {
  console.log(text.length);
  return text;
}

logText(10);
// 에러 -> 숫자타입에 length가 존재 x
logText({ length: 0, value: 'hi' }) // text.length 코드는 객체의 속성 접근과 같이 동작하므로 에러 x
```

### <b>객체의 속성을 제약하는 방법</b>
두 객체를 비교할 때도 제네릭 제약 조건을 사용가능
```ts
function getProperty<T, O extends keyof T>(obj: T, key: O) {
  return obj[key];  
}
let obj = { a: 1, b: 2, c: 3 };

getProperty(obj, 'a');
// 에러 x
getProperty(obj, 'z');
// z는 obj의 a, b, c 속성에 해당되지 않으므로 에러
```

## <b>참고 링크</b>
- ***<a href="https://joshua1988.github.io/ts/guide/generics.html#%EC%A0%9C%EB%84%A4%EB%A6%AD-generics-%EC%9D%98-%EC%82%AC%EC%A0%84%EC%A0%81-%EC%A0%95%EC%9D%98">제네릭 관련 링크</a>***