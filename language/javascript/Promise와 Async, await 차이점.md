# Promise / Async, await의 차이점

## <b>Promise</b>
`promise`는 자바스크립트에서 비동기 처리에 사용되는 객체이다.

### Promise 사용 예시
```js 
const condition = true;
const promise = new Promise((resolve, reject) => {
  if (condition) {
    resolved('resolved')
  } else {
    reject('rejected')
  }
});

promise.
  .then((res) => {
    console.log(res);
  })
  .catch((error) => {
    console.log(error);
  });
``` 
위의 코드처럼 `condition`값의 따라 `promise`의 반환값이 결정 되고 있다.

> - 값이 참이면 `resolved`, 거짓이면 `reject`를 호출 <br>
> - `resolve`한 반환 값은 `then()`을 통해 반환 받고,
`reject`의 반환 값은 `catch()`를 통해 반환 받는다.

## <b>Async / await</b>
async와 await는 `callback, promise`의 단점을 해소하기위해 만들어졌다.

`callback, promise`의 단점은 꼬리에 꼬리를 무는 코드가 나올 수도 있다. <br>
흔히 알고있는 *콜백지옥, then()지옥*이라 부른다.

`await`를 통해 `promise`반환 값을 받아 올 수 있다.

`async/await`를 사용하기 위해서는 선행되어야 하는 조건  
> `await`는 `async`함수 안에서만 동작한다.<br>

ex)
```js 
// 위 promise 사용 코드를 async/await를 사용해 코드를 변경

(async () => {
  const condition = true;
  const promise = new Promise((resolve, reject) => {
    if (condition) {
      resolve('resolved');
    } else {
      reject('rejected');
    }
  });

  try {
    const result = await promise;
    console.log(result);
  } catch (err) {
    console.error(err);
  }
})();
```
`async`함수 내의 `await`를 통해 `promise`의 반환 값을 `result` 변수에 담아 콘솔에 출력하는 코드 <br>

***⚠️`async/await`은 에러핸들링  기능이 없으므로 `try-catch()`문을 사용해 핸들링 해야된다.***

## <b>차이점</b>
- 코드 가독성
  - `promise`의 `then()` 지옥의 가능성
  - 코드가 길어지면 길어질수록, `async/await` 를 활용한 코드가 가독성이 좋음
  - `async/await` 은 비동기 코드가 동기 코드처럼 읽히게 해준다. 코드 흐름을 이해 하기 쉽다.

