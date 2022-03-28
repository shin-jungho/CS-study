# <b>Class</b>

ex) 클래스 기반한 예제
```ts
class Greeter {
  greeting: string;
  constructor(message: string) {
    this.greeting = message;
  }
  greet() {
    return 'Hello, ' + this.greeting;
  }
}

console.log(new Greeter('world').greet());

// greeting 프로퍼티, 생성자 greet메서드 3가지 멤버가 존재
```
- 클래스의 멤버 중 하나를 참조할 때 클래스에서 `this.`(클래스 멤버에 대한 액세스)를 앞에 둔다. 
- 마지막 줄에 `new`를 사용해 `Greeter`클래스의 인스턴스를 만들고 앞서 정의한 생성자를 호출해 `Greeter`타입의 새로운 객체를 생성 후 초기화한다.

## <b>상속</b>
상속을 사용해 기존 클래스를 확장해 새로운 클래스를 생성할 수 있다.

ex)
```ts
class Animal {
  name: string;
  constructor(theName: string) { 
    this.name = theName;
  }
  move(distanceInMeters: number = 0) {
    console.log(`${this.name} moved ${distanceInMeters}m.`);
  }
}

class Snake extends Animal {
  constructor(name: string) {
    super(name);
  }
  move(distanceInMeters = 5) {
    console.log('slithering...');
    super.move(distanceInMeters);
  }
}

class Horse extends Animal {
  constructor(name: string) {
    super(name);
  }
  move(distanceInMeters = 45) {
    console.log('Galloping...');
    super.move(distanceInMeters);
  }
}

let sam = new Snake('Sammy the Python');
let tom: Animal = new Horse('Tommy the Palomino');

sam.move();
tom.move(34);
```

- 하위 클래스를 만들때 `extends`키워드를 사용
- `Horse`와 `Snake`가 `Animal`의 하위 클래스로 분류되고 그 기능을 액세스 할 수 있다.
- 생성자 함수를 포함하는 파생 클래스는 기본 클래스에서 생성자 함수를 실행할 `super()`를 호출해야 한다.
- 오버라이드하는 `move`메서드를 생성해 각 클래스별로 기능을 부여했다. `tom`은 `Animal`로 선언되었지만, `tom.move (34)`가 `Horse`에서 재정의 메소드를 호출할 때, 그 값은 `Horse`입니다.

결과값
```
Slithering...
Sammy the Python moved 5m.
Galloping...
Tommy the Palomino moved 34m.
```

## <b>`Public`, `Private`, `Protected`</b>
<br>

### <b>`public`</b>
TypeScript에서는 기본적으로 각 멤버가 `public`이고 명시적으로 표시 가능하다.

ex)
```ts
class Animal {
  public name: string;
  public constructor(theName: string {
    this.name = theName;
  })
  public move(distanceInMeters: number) {
    console.log(`${this.name} moved ${distanceInMeters}m.`)
  }
}
```

### <b>`private`</b>
멤버가 `private`으로 표시되면 클래스 외부에서 액세스할 수 없다.

```ts
class Animal {
  private name: string;
  constructor(theName: string) {
    this.name = theName;
  }
}
new Animal('cat').name;
// Error: 'name' is private;
```

```ts
class Animal {
    private name: string;
    constructor(theName: string) { this.name = theName; }
}
class Rhino extends Animal {
    constructor() { super("Rhino"); }
}
class Employee {
    private name: string;
    constructor(theName: string) { this.name = theName; }
}
let animal = new Animal("Goat");
let rhino = new Rhino();
let employee = new Employee("Bob");
animal = rhino;
animal = employee; // Error: 'Animal' and 'Employee' are not compatible
```

- `Animal`과 `Rhino`는 `Animal`의 `private name : string`과 같은 선언으로부터 같은 형태의 `private`부분을 공유하기 때문에 호환된다.
- `Employee`에서 `Animal`에 할당할때 호환되지 않는다는 에러를 얻는다. 
`Employee`도 `name`이라는 `private`멤버를 가지고 있지만 `Animal`로 선언 한 멤버는 아니다.

### <b>`protected`</b>

`protected`키워드는 `private`과 매우 유사하게 동작한다. <br>
`protected`로 선언된 멤버는 파생 클래스의 인스턴스에 액세스할 수 있다.

```ts
class Person {
    protected name: string;
    constructor(name: string) { this.name = name; }
}
class Employee extends Person {
    private department: string;
    constructor(name: string, department: string) {
        super(name);
        this.department = department;
    }
    public getElevatorPitch() {
        return `Hello, my name is ${this.name} and I work in ${this.department}.`;
    }
}
let howard = new Employee("Howard", "Sales");
console.log(howard.getElevatorPitch());
console.log(howard.name); 
// error
```
- `Person`의 외부에서 `name`을 사용할 수 없지만 `Employee`는 `Person`에서 파생되었기 때문에 인스턴스 메서드에서 사용할 수 있다.

생성자는 `protected`로 표시 될 수도 있다. 즉, 클래스 외부에서 클래스를 인스턴스화 할 수 없지만 확장은 가능하다

ex)
```ts
class Person {
    protected name: string;
    protected constructor(theName: string) { this.name = theName; }
}
// Employee can extend Person
class Employee extends Person {
    private department: string;
    constructor(name: string, department: string) {
        super(name);
        this.department = department;
    }
    public getElevatorPitch() {
        return `Hello, my name is ${this.name} and I work in ${this.department}.`;
    }
}
let howard = new Employee("Howard", "Sales");
let john = new Person("John"); // Error: The 'Person' constructor is protected
```

### <b>`readonly`</b>
읽기 전용 속성을 만들 수 있다. <br>
`readonly`속성은 선언 또는 생성자에서 초기화해야한다.
```ts
class Octopus {
    readonly name: string;
    readonly numberOfLegs: number = 8;
    constructor (theName: string) {
        this.name = theName;
    }
}
let dad = new Octopus("Man with the 8 strong legs");
dad.name = "Man with the 3-piece suit"; // error! name is readonly.
```

### 파라미터 프로퍼티
파라미터 프로퍼티는 접근자 또는 `readonly`또는 둘 모두로 생성자 파라미터 앞에 접두어를 붙임으로써 선언된다.

### Getter / Setter(Accessor)
Getter/Setter메서드를 이용해 객체의 멤버 프로퍼티가 액세스되는 방식을 세밀하게 제어할 수 있다.

ex) getter, setter가 없을때
```ts
class Employee {
    fullName: string;
}
let employee = new Employee();
employee.fullName = "Bob Smith";
if (employee.fullName) {
    console.log(employee.fullName);
}
```
사람들이 `fullName`을 설정하도록 허용하는 것은 매우 편리할 수 있지만 무작위 사람들이 이름을 바꿀 수 있다면 문제가 발생할 수도 있다.

ex) getter, setter 사용할때
```ts
let passcode = "secret passcode";
class Employee {
    private _fullName: string;
    get fullName(): string {
        return this._fullName;
    }
    set fullName(newName: string) {
        if (passcode && passcode == "secret passcode") {
            this._fullName = newName;
        }
        else {
            console.log("Error: Unauthorized update of employee!");
        }
    }
}
let employee = new Employee();
employee.fullName = "Bob Smith";
if (employee.fullName) {
    console.log(employee.fullName);
}
```

### `static`프로퍼티
인스턴스가 아닌 클래스 자체에서 볼 수 있는 클래스의 정적 멤버를 만들 수도 있다.

ex) `static`을 사용한 예제
```ts
class Grid {
    static origin = {x: 0, y: 0};
    calculateDistanceFromOrigin(point: {x: number; y: number;}) {
        let xDist = (point.x - Grid.origin.x);
        let yDist = (point.y - Grid.origin.y);
        return Math.sqrt(xDist * xDist + yDist * yDist) / this.scale;
    }
    constructor (public scale: number) { }
}
let grid1 = new Grid(1.0);  // 1x scale
let grid2 = new Grid(5.0);  // 5x scale
console.log(grid1.calculateDistanceFromOrigin({x: 10, y: 10}));
console.log(grid2.calculateDistanceFromOrigin({x: 10, y: 10}));
```

인스턴스 액세스 앞에 `this.`를 추가하는 것과 마찬가지로 정적 액세스 앞에 `Grid.`를 추가한다.

## <b>추상 클래스</b>
추상 클래스는 다른 클래스를 파생시킬 수 있는 기본 클래스이다. 하지만 직접 인스턴스화 할 수 없다. <br>
***인터페이스와 달리 추상 클래스는 멤버에 대한 세부 정보를 포함할 수 있다.***<br>
`abstract` 키워드는 추상 클래스 내 추상 메서드뿐만 아니라 추상 클래스를 정의하는데 사용한다.

ex)
```ts
abstract class Animal {
    abstract makeSound(): void;
    move(): void {
        console.log("roaming the earth...");
    }
}
```
- `abstract`로 표시된 추상 클래스 내의 메서드에는 implementation이 포함되어 있지 않아 파생 클래서에서 구현해야한다.
- `abstract`키워드를 포함해야 하며 선택적으로 getter/setter를 포함할 수 있다.
```ts
abstract class Department {
    constructor(public name: string) {
    }
    printName(): void {
        console.log("Department name: " + this.name);
    }
    abstract printMeeting(): void; // must be implemented in derived classes
}
class AccountingDepartment extends Department {
    constructor() {
        super("Accounting and Auditing"); // constructors in derived classes must call super()
    }
    printMeeting(): void {
        console.log("The Accounting Department meets each Monday at 10am.");
    }
    generateReports(): void {
        console.log("Generating accounting reports...");
    }
}
let department: Department; // ok to create a reference to an abstract type
department = new Department(); // error: cannot create an instance of an abstract class
department = new AccountingDepartment(); // ok to create and assign a non-abstract subclass
department.printName();
department.printMeeting();
department.generateReports(); // error: method doesn't exist on declared abstract type
```