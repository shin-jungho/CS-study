# <b>Stack, Queue</b>
stack, queue를 js문법으로 알아보기

![image](https://media.vlpt.us/images/nayeon/post/a6dfbb5c-bc62-44e2-820d-411a993fd67e/1_GNA2E1NFiJMc6cTHHPa6kw.png)

## <b>🧱Stack</b>
마지막에 쌓인 요소가 먼저 나오는 원리
- Last In First Out(LIFO)로 불림

### <b>Method</b>
Stack의 메서드는 `push`, `pop`, `peek`이 있다.
- `push`: 순서대로 데이터를 넣는 메서드
- `pop`: 제일 마지막 데이터를 꺼내고 제거하는 메서드
- `peek`: stack에 쌓인 데이터의 제일 마지막 데이터를 보여주기만 하는 메서드

ex) js array의 예시
```js
const stack = []

// push
stack.push('dog');
stack.push('cat');
stack.push('bear');
stack // ['dog', 'cat', 'bear']

// pop 
stack.pop(); // 'bear'
stack // ['dog', 'cat']

// peek
stack[stack.length - 1] // 'cat'
```

ex) js object의 예시
```js
class Stack {
  constructor() {
    this.storage = {}
    this.size = 0
  }
  push(element) {
    this.size++ 
    this.storage[this.size] = element 
  }

  pop() {
    let removed = this.storage[this.size]
    delete this.storage[this.size]
    this.size--
    return removed
  }

  peek() {
    return this.storage[this.size]
  }
}

const stack = new Stack()
stack.push('dog')
stack.push('cat')
stack.push('bear')

console.log(stack);
// Stack { storage: { '1': 'dog', '2': 'cat', '3': 'bear' }, size: 3 }

console.log(stack.pop());
// 'bear'

console.log(stack.peek());
// 'cat'
```

# <b>⬇️ Queue</b>
가장 먼저 쌓인 데이터가 먼저 나오는 원리
 - First In First Out(FIFO)로 불림

### <b>Method</b>
- `enqueue` : 데이터를 넣는 것
- `dequeue` : 앞에서부터 데이터를 꺼내는 과정

ex) js array의 예시
```js
const queue = [];

queue.push('1');
queue.push('2');
queue.push('3');

console.log(queue); // ['1', '2', '3']

console.log(queue.shift());
// 1
console.log(queue);
// ['2', '3']
```

ex) js Object의 예시
```js
class Queue {
  constructor() {
    this.storage = {}
    this.head= 0
    this.tail = 0
  }
  enqueue(element) { 
    this.storage[this.tail] = element 
    this.tail++
  }

  dequeue() {
    let removed = this.storage[this.head]
    delete this.storage[this.head]
    this.head++
    return removed
  }
}

const queue = new Queue()

queue.enqueue('1')
queue.enqueue('2')
queue.enqueue('3')
console.log(queue);
// Queue { storage: { '0': '1', '1': '2', '2': '3' }, head: 0, tail: 3 }

console.log(queue.dequeue());
// 1

console.log(queue);
// Queue { storage: { '1': '2', '2': '3' }, head: 1, tail: 3 }
```