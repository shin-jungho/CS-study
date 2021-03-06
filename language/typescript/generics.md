# <b>Generics</b>
> π₯ ***νμμ λ§μΉ ν¨μμ νλΌλ―Έν°μ²λΌ μ¬μ©νλ κ²***

ex)
```ts 
// μ λ€λ¦­ x
function getText(text) {
  return text;
}

getText('hi'); // 'hi'
getText(10); // 10
getText(true); // true

// μ λ€λ¦­ γ
function getText<T>(text: T): T {
  return text;
}

getText<string>('hi');
getText<number>(10);
getText<boolean>(true);
```
### `getText<string>('hi')`μ μ λ€λ¦­μ λμ

```ts
function getText<string>(text: T): T {
  return text;
}
// getText()ν¨μλ₯Ό νΈμΆν λ μ λ€λ¦­(ν¨μμμ μ¬μ©ν  νμ) κ°μΌλ‘ stringμ λκ²ΌκΈ° λλ¬Έ

getText<string>('hi');
// ν¨μ μΈμλ‘ 'hi'λΌλ κ°μ μλμ κ°μ΄ λκΈ°κ² λλ©΄

function getText<string>(text: string): string {
  return text;
} 
// ν¨μλ μλ ₯ κ°μ νμμ΄ stringμ΄λ©΄μ λ°ν κ° νμλ stringμ΄μ΄μΌ νλ€.
```

## <b>μ λ€λ¦­μ μ¬μ©νλ μ΄μ </b>
```ts
// μΈμλ₯Ό νλ λκ²¨ λ°μ λ°νν΄μ£Όλ ν¨μ
function logText(text: string): string {
  return text;
}
```
μ μ½λμμ μΈμμ λ°ν κ° λͺ¨λ `string`μΌλ‘ μ§μ λ μμ§λ§ λ§μ½ μ¬λ¬ νμμ νμ©νκ³  μΆλ€λ©΄ `any`λ₯Ό μ¬μ©ν  μ μλ€.
```ts
function logText(text: any): any {
  return text;
}
```
`any`λ‘ νμμ μ ν  κ²½μ° νμ κ²μ¬λ₯Ό μνκΈ° λλ¬Έμ ***ν¨μμ μΈμλ‘ μ΄λ€ νμμ΄ λ€μ΄κ°κ³  μ΄λ€ κ°μ΄ λ°νλλμ§λ μ μ μλ€.***

λ°λΌμ μ΄λ¬ν λ¬Έμ λ₯Ό ν΄κ²°νλ κ²μ΄ **μ λ€λ¦­**μ΄λ€.

```ts
function logText<T>(text: T): T {
  return text;
}
```
ν¨μ μ΄λ¦ λ€μ `<T>`λ₯Ό μΆκ°νκ³  ν¨μμ μΈμμ λ°νκ°μ λͺ¨λ `T`λΌλ νμμ μΆκ°νλ©΄ λλ€.

```ts
// μμ ν¨μ νΈμΆλ°©λ² 2κ°μ§
// 1.
const text = logText<string>('hi');

// 2. -> κ°λμ±, μ½λ μ§§μμ λ§μ΄μ°μ
const text = logText('hi');
```

## <b>μ λ€λ¦­ νμ λ³μ</b>
> μμμ λ°°μ΄ λ΄μ©μΌλ‘ μ λ€λ¦­μ μ¬μ©νλ©΄ **μ»΄νμΌλ¬μμ μΈμμ νμμ λ£μ΄λ¬λΌλ μλ¬κ° λ¬λ€.**

### ν¨μμ μΈμλ‘ λ°μ κ°μ `length`λ₯Ό νμΈνκ³  μΆλ€λ©΄ μ΄λ»κ² ??
```ts
// 1. 
function logText<T>(text: T): T {
  console.log(text.length);
  return text;
}
// μ»΄νμΌλ¬μμ μλ¬λλ€. μλλ©΄ textμ .lengthκ° μλ€λ λ¨μκ° μκΈ° λλ¬Έμ΄λ€.

// 2.
function logText<T>(text: T[]): T[] {
  console.log(text.length); // μ λ€λ¦­ νμμ΄ λ°°μ΄μ΄κΈ° λλ¬Έμ lengthλ₯Ό νμ©νλ€.
  return text;
}
```
2λ²μ§Έ μ½λλ `T`λΌλ λ³μ νμμ λ°κ³ , μΈμ κ°μΌλ‘ λ°°μ΄ ννμ `T`λ₯Ό λ°λλ€. 

μ΄λ¬ν λ°©μμΌλ‘ μ λ€λ¦­μ μ¬μ©νλ©΄ μ μ°ν λ°©μμΌλ‘ ν¨μ νμμ μ μν  μ μλ€.

2λ² μ½λλ₯Ό λͺμμ μΌλ‘ λ°κΎΈλ©΄
```ts
function logText<T>(text: Array<T>): Array<T> {
  console.log(text.length);
  return text;
}
```
## <b>μ λ€λ¦­ μΈν°νμ΄μ€</b>

```ts
function logText<T>(text: T): T {
  return text;
}
// 1.
let str: <T>(text: T) => T = logText;

// 2.
let str: {<T>(text: T): T} = logText;
// 1, 2λ κ°μ μ½λμ΄λ€.
```
μμ μ½λλ₯Ό μ λ€λ¦­ μΈν°νμ΄μ€ μ½λλ‘ λ³κ²½νλ©΄
```ts
interface GenericsLogTextFn {
  <T>(text: T): T;
}
function logText<T>(text: T): T {
  return text;
}
let myString: GenericsLogTextFn = logText; //

// μΈν°νμ΄μ€μ μΈμ νμμ κ°μ‘°ν  κ²½μ° 
interface GenericsLogTextFn<T> {
  (text: T): T;
}
function logText<T>(text: T): T {
  return text;
}
let myString: GenericsLogTextFn<string> = logText;
```
### ***β οΈ enum, namespaceλ μ λ€λ¦­ μμ± λΆκ°!***

## <b>μ λ€λ¦­ ν΄λμ€</b>
```ts
class GenericMath<T> {
  pi: T;
  sum: (x: T, y: T) => T;
}

let math = new GenericMath<number>();
```
μ λ€λ¦­ ν΄λμ€λ₯Ό μ μΈν  λ ν΄λμ€ μ΄λ¦ μ€λ₯Έμͺ½μ <T>λ₯Ό λΆμ¬μ€λ€. κ·Έλ¦¬κ³  ν΄λΉ ν΄λμ€λ‘ μΈμ€ν΄μ€λ₯Ό μμ±ν  λ νμμ μ΄λ€ κ°μ΄ λ€μ΄κ°μ§ μ§μ νλ©΄ λλ€.
> *<span style="gray">μΈμ€ν΄μ€λ? μΌλ°μ μΌλ‘ μ€ν μ€μΈ μμμ νλ‘μΈμ€, ν΄λμ€μ νμ¬ μμ±λ κ°μ²΄λ₯Ό λ§νλ€.</span>*

## <b>μ λ€λ¦­ μ μ½ μ‘°κ±΄</b>
μ λ€λ¦­ ν¨μμ μ΄λμ λ νμ ννΈλ₯Ό μ€ μ μλ λ°©λ²
```ts
function logText<T>(text: T): T {
  console.log(text.length);
  return text;
}
```
μΈμ νμμ μ μΈν Tλ μμ§ μ΄λ€ νμμΈμ§ κ΅¬μ²΄μ μΌλ‘ μ μνμ§ μμκΈ° λλ¬Έμ length μ½λμμ μ€λ₯κ° λλ€.

μ΄λ΄ κ²½μ° ν΄λΉ νμμ μ μνμ§ μκ³ λ `length` μμ± μ λλ νμ©νλ €λ©΄ μ΄ μ κ°μ΄ μμ±νλ€.
```ts
interface LengthWise {
  length: number;
}

function logText<T extends LengthWise>(text: T): T {
  console.log(text.length);
  return text;
}

logText(10);
// μλ¬ -> μ«μνμμ lengthκ° μ‘΄μ¬ x
logText({ length: 0, value: 'hi' }) // text.length μ½λλ κ°μ²΄μ μμ± μ κ·Όκ³Ό κ°μ΄ λμνλ―λ‘ μλ¬ x
```

### <b>κ°μ²΄μ μμ±μ μ μ½νλ λ°©λ²</b>
λ κ°μ²΄λ₯Ό λΉκ΅ν  λλ μ λ€λ¦­ μ μ½ μ‘°κ±΄μ μ¬μ©κ°λ₯
```ts
function getProperty<T, O extends keyof T>(obj: T, key: O) {
  return obj[key];  
}
let obj = { a: 1, b: 2, c: 3 };

getProperty(obj, 'a');
// μλ¬ x
getProperty(obj, 'z');
// zλ objμ a, b, c μμ±μ ν΄λΉλμ§ μμΌλ―λ‘ μλ¬
```

## <b>μ°Έκ³  λ§ν¬</b>
- ***<a href="https://joshua1988.github.io/ts/guide/generics.html#%EC%A0%9C%EB%84%A4%EB%A6%AD-generics-%EC%9D%98-%EC%82%AC%EC%A0%84%EC%A0%81-%EC%A0%95%EC%9D%98">μ λ€λ¦­ κ΄λ ¨ λ§ν¬</a>***