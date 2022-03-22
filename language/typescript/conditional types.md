# <b>Conditional Type</b>
> js의 삼항연산자와 비슷한 형태.
```ts
T extends U ? X : Y
``` 
위에 코드 형태이고 T, U ,X, Y 전부 타입이다. <br>
📓 ***T 타입이 U에 할당 가능한 타입이면 X라는 타입이고, 아니면 Y라는 타입이다.***

조건부 타입 `T extends U ? X : Y`는 X 나 Y로 결정되거나 지연된다. 왜냐하면 조건이 하나 혹은 그 이상의 타입 변수에 의존하기 때문이다.<br>
T 나 U가 타입 변수를 포함할 때, X 또는 Y로 결정되거나 지연될지, 타입 시스템이 T가 항상 U에 할당할 수 있는지에 대해 충분한 정보를 가지고 있는지 여부로 결정된다. <br>

ex) 
```ts
// 즉시 결정되는 일부 타입

declare function f<T extends boolean>(x: T): T extends true ? string : number;
// type : string, number

let x = f(Math.random() < 0.5);
```
```ts
// 중첩 조건부 타입을 사용하는 TypeName 타입별칭

type TypeName<T> =
    T extends string ? "string" :
    T extends number ? "number" :
    T extends boolean ? "boolean" :
    T extends undefined ? "undefined" :
    T extends Function ? "function" :
    "object";

type T0 = TypeName<string>;  // "string"
type T1 = TypeName<"a">;  // "string"
type T2 = TypeName<true>;  // "boolean"
type T3 = TypeName<() => void>;  // "function"
type T4 = TypeName<string[]>;  // "object"
```

```ts
// 조건부 타입이 지연되는 지점

interface Foo {
  propA: boolean;
  propB: boolean;
}

declare function f<T>(x: T): T extends Foo ? string : number;

function foo<U>(x: U) {
  // 'U extends Foo ? string : number' 타입을 가지고 있습니다
  let a = f(x);

  // 이 할당은 허용됨
  let b: string | number = a;
}
```
위 코드에서 변수 `a`는 아직 분기를 선택하지 못한 조건부 타입을 가지고 있다. 또 다른 코드가 `foo`의 호출을 그만두면, `U`를 다른 타입으로 대체할 것이고, Typescript가 실제로 분기를 선택할 수 있는지 결정하기 위해 조건부 타입을 재평가한다. 

그동안 조건부 타입을 조건부의 각 분기가 대상에 할당 가능한 한 다른 대상 타입으로 할당할 수 있다. 그래서 위 예제에서 조건부가 어떻게 평가되든지, `string`혹은 `number`로 알려져 있기 때문에, 조건이 `U extends Foo ? string : number`를 `string | number`로 할당 할 수 있다.

### 참고 링크
- <a href="https://typescript-kr.github.io/pages/advanced-types.html#%EC%A1%B0%EA%B1%B4%EB%B6%80-%ED%83%80%EC%9E%85-conditional-types">조건부 타입</a>