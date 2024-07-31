
# 타입스크립트 기본 문법

React Native으로 프론트엔드 개발을 하면서 타입스크립트를 같이 적용해서 공부하는 중입니다.
타입스크립트를 적용한 큰 이유는 유지보수와 오류 예방 차원인데, 졸업 프로젝트이기에 규모가 작은 프로젝트가 아닐거라는 판단에 JS가 더 익숙하지만 나중을 위해 처음부터 TS적용해서 개발해 나가는 중입니다 :) 아래는 간단한 문법을 정리해 보았습니다!

---

##  1. 기본 타입 선언

> 프로그램이 유용하려면 숫자, 문자열, 구조체, 불리언 값과 같은 간단한 데이터 단위가 필요합니다. TypeScript는 JavaScript와 거의 동일한 데이터 타입을 지원하며, 열거 타입을 사용하여 더 편리하게 사용할 수 있습니다.
> 

### 1-1. 문자열

```tsx
let message: string = "Hello TypeScript!";
```

### 1-2. 숫자

```tsx
let luckyNumber: number = 42;
```

### 1-3. 배열

```tsx
let numbers: number[] = [1, 2, 3];
let strings: Array<string> = ["TypeScript", "JavaScript"];
let mixed: [string, number] = ["John", 35];
```

### 1-4. 객체

```tsx
let user: object = { name: "John", age: 25 };
let person: { name: string; age: number } = {
  name: "Jane",
  age: 30
};
```

### 1-5. 불리언 (Boolean)

```tsx
let isActive: boolean = false;
```

---

## 2. 함수 선언

> TypeScript 함수는 JavaScript와 마찬가지로 기명 함수(named function)과 익명 함수(anonymous function)로 만들 수 있습니다. 이를 통해 API에서 함수 목록을 작성하든 일회성 함수를 써서 다른 함수로 전달하든 애플리케이션에 가장 적합한 방법을 선택할 수 있습니다.
> 

### 2-1. 함수 타입 지정

TypeScript에선 parameter와 return 값의 타입 선언

```tsx
function add(x: number, y: number): number {
  return x + y;
}
```

### 2-2. 선택적 매개변수 (optional parameter)

optional parameter`(있어도 되고 없어도 되는 parameter)`는 `?`를 앞에 추가해주면 된다.

```tsx
function buildFullName(firstName: string, lastName?: string) {
  return lastName ? `${firstName} ${lastName}` : firstName;
}

let name1 = buildFullName("John");
let name2 = buildFullName("John", "Doe");
```

---

## 3. 인터페이스 (Interface)

> TypeScript의 핵심 원칙 중 하나는 타입 검사가 값의 형태에 초점을 맞추고 있다는 것입니다. 이를 "덕 타이핑(duck typing)" 혹은 "구조적 서브타이핑 (structural subtyping)"이라고도 합니다. TypeScript에서, 인터페이스는 이런 타입들의 이름을 짓는 역할을 하고 코드 안의 계약을 정의하는 것뿐만 아니라 프로젝트 외부에서 사용하는 코드의 계약을 정의하는 강력한 방법입니다.
> 

`interface`는 자주 사용하는 타입들을 object 형태의 묶음으로 정의해 새로운 타입을 만드는 기능이다.

### 3-1. 인터페이스 선언
```tsx
interface User {
  age: number;
  name: string;
}
```

### 3-2. 변수에 인터페이스 사용

```tsx
const user: User = { name: "John", age: 25 };
```

### 3-3. 함수 매개변수에 인터페이스 사용

```tsx
function printUser(user: User) {
  console.log(user);
}

printUser({ name: "John", age: 25 });
```

### 3-4. 함수 타입 인터페이스

```tsx
interface Add {
  (x: number, y: number): number;
}

let add: Add = (a, b) => a + b;

console.log(add(10, 20));
```

### 3-5. 배열 타입 인터페이스

```tsx
interface StringArray {
  [index: number]: string;
}

let stringArray: StringArray = ["hello", "world"];
```

### 3-6. 객체 타입 인터페이스

```tsx
interface StringMap {
  [key: string]: string;
}

const stringMap: StringMap = {
  key1: "value1",
  key2: "value2"
};
```

### 3-7. 인터페이스 확장

```tsx
interface Person {
  name: string;
  age: number;
}

interface Developer extends Person {
  position: string;
}

const developer: Developer = {
  name: "Alice",
  age: 30,
  position: "Frontend Developer"
};
```

---

## 4. 타입 (type)

`type` 키워드는 `interface`와는 다르게 새로운 타입을 생성하는 것이 아닌 별칭을 부여하는 것이다. `extends` 키워드는 사용할 수 없다.

### 4-1. 타입 별칭 선언

```tsx
type StringOrNumber = string | number;

const example1: StringOrNumber = "hello";
const example2: StringOrNumber = 100;
```

### 4-2. 타입과 인터페이스의 차이

타입 별칭과 인터페이스의 가장 큰 차이점은 타입의 확장 가능 / 불가능 여부이다. 인터페이스는 확장이 가능한데 반해 타입 별칭은 확장이 불가능하다. 따라서, 가능한 한 type보다는 interface로 선언해서 사용하는 것을 추천한다.

---

## 5. 연산자 (Operator)

### 5-1. 유니언 타입 (Union Type)

한 개 이상의 type을 선언할 때 사용할 수 있다.

`|` 키워드를 사용한다.

```tsx
function formatValue(value: string | number) {
  if (typeof value === 'string') {
    return value.toUpperCase();
  } else if (typeof value === 'number') {
    return value.toFixed(2);
  } else {
    throw new TypeError('문자열 또는 숫자만 허용됩니다!');
  }
}

formatValue('hello'); // "HELLO"
formatValue(123.456); // "123.46"
```

### 5-2. 교차 타입 (Intersection Type)

합집합과 같은 개념이다.

함수 호출의 경우, 함수 인자에 명시한 type을 모두 제공해야 한다.

`&` 키워드를 사용한다.

```tsx
interface Animal {
  name: string;
  age: number;
}

interface Bird {
  wingspan: number;
}

type WingedAnimal = Animal & Bird;

let eagle: WingedAnimal = {
  name: "Eagle",
  age: 5,
  wingspan: 2.1
};
```

---

## 6. Class

### 6-1. 접근 제한자

클래스 기반 객체 지향 언어가 지원하는 접근 제한자(Access modifier) `public`, `private`, `protected`를 지원하며 의미 또한 동일하다.

접근 제한자를 명시하지 않았을 때

- 다른 클래스 기반 언어 : `protected`로 지정
- TypeScript : `public`으로 지정

| 접근 가능성 | public | protected | private |
| --- | --- | --- | --- |
| 클래스 내부 | O | O | O |
| 자식 클래스 내부 | O | O | X |
| 클래스 인스턴스 | O | X | X |

### 6-2. 클래스에서의 타입 선언

```tsx
class Vehicle {
  private brand: string;
  public model: string;
  readonly year: number;

  constructor(brand: string, model: string, year: number) {
    this.brand = brand;
    this.model = model;
    this.year = year;
  }
}
```

---

## 7. Enum 열거형

> 열거형(Enums)으로 이름이 있는 상수들의 집합을 정의할 수 있습니다. 열거형을 사용하면 의도를 문서화 하거나 구분되는 사례 집합을 더 쉽게 만들수 있습니다. TypeScript는 숫자와 문자열-기반 열거형을 제공합니다.
> 

`enum` 키워드를 사용하면 default 값을 선언할 수 있다.

### 7-1. 숫자형 enum

자동으로 0에서 1씩 증가하는 값을 부여한다.

```tsx
enum Direction {
  Up,      // 0
  Down,    // 1
  Left,    // 2
  Right    // 3
}

const move = Direction.Up; // 0
```

### 7-2. 문자형 enum

```tsx
enum Status {
  Success = "SUCCESS",
  Error = "ERROR"
}

const status = Status.Success; // "SUCCESS"
```

---

## 8. 제네릭(generics)

> C#과 Java 같은 언어에서, 재사용 가능한 컴포넌트를 생성하는 도구상자의 주요 도구 중 하나는 제네릭입니다, 즉, 단일 타입이 아닌 다양한 타입에서 작동하는 컴포넌트를 작성할 수 있습니다. 사용자는 제네릭을 통해 여러 타입의 컴포넌트나 자신만의 타입을 사용할 수 있습니다.
> 

제네릭을 활용하면 같은 기능의 함수를 또 만들 필요가 없고, 타입 추론에 있어서 강점을 가진다는 장점이 있다.

### 8-1. 제네릭 함수 선언

`<T>`와 같이 타입을 선언한다. 알파벳은 대부분 `T`를 사용한다.

```tsx
function logText<T>(text: T): T {
  console.log(text);
  return text;
}

logText<string>('Hello');
```

### 8-2. interface에 제네릭 선언

```tsx
interface Menu<T> {
  value: T;
  price: number;
}

const hamburger: Menu<string> = { value: 'hamburger', price : 5000 };
```

### 8-3. 제네릭 타입 제한

### 8-3-1. 배열 힌트

```tsx
function textLength<T>(text: T[]): T[] {
    console.log(text.length);
    return text;
}

textLength<string>(['hello', 'world']);
```

### 8-3-2. 정의된 타입 이용 (extends)

```tsx
interface LengthType {
    length: number;
}

function logTextLen<T extends LengthType>(text: T): T {
    console.log(text.length);
    return text;
}

logTextLen('hello world'); // 11
logTextLen(100); // 에러!
logTextLen({ length: 100 }); // 100
```

### 8-3-3. keyof

interface에 정의된 key 값만을 허용

```tsx
interface Item {
    name: string;
    price: number;
    stock: number;
}

function getItemOption<T extends keyof Item>(itemOption: T): T {
    return itemOption;
}

// 'name', 'price', 'stock'만 인자로 사용 가능
getShoppingItemOption('price');
```