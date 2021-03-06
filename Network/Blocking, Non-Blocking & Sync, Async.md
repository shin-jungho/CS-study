![this is an image](https://camo.githubusercontent.com/b7b28ae739c50d5ed8a4594f52f24e671aeeae234befd0991e5230561ba303bf/68747470733a2f2f696d67312e6461756d63646e2e6e65742f7468756d622f523132383078302f3f73636f64653d6d746973746f72793226666e616d653d6874747073253341253246253246626c6f672e6b616b616f63646e2e6e6574253246646e25324664613530597a2532466274713044736a65345a562532466c47653848386e5a676442646746766f3749637a5330253246696d672e706e67)

## <b>Blocking / Non-Blocking</b>
block / non-block은 간단히 말해 ***호출된 함수***가 ***호출한 함수***에게 제어권을 건네주는 유무의 차이라고 볼 수 있다.<br>
ex) 함수 `A`, `B`가 있고 `A` 안에서 `B`를 호출했다고 가정해보자. 이때 호출한 함수는 `A`, 호출된 함수는 `B`가 된다. 현재 B가 호출되면서 B는 자신의 일을 진행해야된다. ***(제어권이 B에게 주어진 상황)*** <br>

- Blocking: 함수 B는 할 일을 마칠 때까지 제어권을 가지고 있으므로 A는 B가 다 마칠 때까지 기다려야 한다.
- Non-Blocking: 함수 B는 할 일을 마치지 않았어도 A에게 제어권을 넘겨준다. 따라서 A는 B를 기다리면서도 다른 일을 진행 할 수 있다.

## <b>Sync / Async</b>
Sync / Async(동기/비동기)는 일을 수행 중인 ***동시성***을 중점으로 봐야한다.<br>

아까처럼 함수 A와 B라고 똑같이 생각했을 때, B의 수행 결과나 종료 상태를 A가 신경쓰고 있는 유무의 차이라고 생각하면 된다.
- Sync: 함수 A는 함수 B가 일을 하는 중에 기다리면서, 현재 상태가 어떤지 계속 체크한다.
- Async: 함수 B의 수행 상태를 B 혼자 직접 신경쓰면서 처리한다. (Callback)

따라서, ***호출된 함수***를 ***호출한 함수***가 신경쓰는지, ***호출된 함수*** 스스로 신경쓰는지를 동기/비동기라고 생각하면된다.

비동기는 호출시 Callback을 전달하여 작업의 완료 여부를 호출한 함수에게 답하게 된다. 
(Callback이 오기 전까지 호출한 함수는 신경쓰지 않고 다른 일을 할 수 있음)

위 그림에서 4가지상황을 쉬운케이스 별로 나누면

### 1) Blocking & Sync
```
나 : 사장님 치킨 한마리만 포장해주세요
사장님 : 네 금방되니까 잠시만요!
나 : 넹
-- 사장님 치킨 튀기는 중--
나 : (아 언제 되지?..궁금한데 그냥 멀뚱히 서서 치킨 튀기는거 보면서 기다림)
```

### 2) Blocking & Async
```
나 : 사장님 치킨 한마리만 포장해주세요
사장님 : 네 금방되니까 잠시만요!
나 : 앗 넹
-- 사장님 치킨 튀기는 중--
나 : (언제 되는지 안 궁금함, 잠시만이래서 다 될때까지 서서 붙잡힌 상황)
```

### 3) Non-blocking & Sync
```
나 : 사장님 치킨 한마리만 포장해주세요
사장님 : 네~ 주문 밀려서 시간 좀 걸리니까 볼일 보시다 오세요
나 : 넹
-- 사장님 치킨 튀기는 중--
(5분뒤) 나 : 제꺼 나왔나요?
사장님 : 아직이요
(10분뒤) 나 : 제꺼 나왔나요?
사장님 : 아직이요ㅠ
(15분뒤) 나 : 제꺼 나왔나요?
사장님 : 아직이요ㅠㅠ

```

### 4) Non-blocking & Async
```
나 : 사장님 치킨 한마리만 포장해주세요
사장님 : 네~ 주문 밀려서 시간 좀 걸리니까 볼일 보시다 오세요
나 : 넹
-- 사장님 치킨 튀기는 중--
나 : (앉아서 다른 일 하는 중)
...
사장님 : 치킨 나왔습니다
나 : 잘먹겠습니다~
```

## [참고]
- <a href="https://musma.github.io/2019/04/17/blocking-and-synchronous.html">링크</a>