# chapter19 : 프로토타입

자스크립트는 클ㅐ스 기반 객체지향 프로그래밍 언어보다 효율적이며 더 강력한 객체 지향 프로그래밍 능력을 지니고있는 프로토타입 기반의 객체 지향 프로그래밍 언어이다.

## 객체지향 프로그래밍

: 프그램을 명령어 또는 함수의 목록으로 보는 전통적인 명령형 프로그래밍의 절차 지향적 관점에서 벗어나 여러개의 독립적 단위, 객체의 집합으로 프로그램을 표현하려는 프로그래밍 패러다임

- 실계의 실체(특징이나 성질을 나타내는 속성) 를 인식하는 철학적 사고를 프로그래밍에 접목
- 객체는 상태 데이터와 동작을 하나의 논리적인 단위로 묶은 복합적인 자료구조
  - 객체의 상태 데이터 : 프로퍼티
  - 객체의 동작 : 메드

## 상속과 프로포토타입

- 객체지향 프로그래밍의 핵심개념 : 상속 -> 어떤객체의 프로퍼티 또는 메서드를 다른 객체가 상속받아 그대로 사용할수있는것
- 자스크립트는 프로토타입을 기반으로 상속구현 => 불필요한 중복을 제거

```tsx
// 생성자 함수
function Circle(radius) {
  this.radius = radius;
}
// Circle 생성자 함수가 생성한 모든 인스턴스가 getArea 메서드를 // 공유해서 사용할 수 있도록 프로토타입에 추가한다.
// 프로토타입은 Circle 생성자 함수의 prototype 프로퍼티에 바인딩되어 있다.
Circle.prototype.getArea = function () {
  return Math.PI * this.radius ** 2;
};
// 인스턴스 생성
const circle1 = new Circle(1);
const circle2 = new Circle(2);
// Circle 생성자 함수가 생성한 모든 인스턴스는 부모 객체의 역할을 하는 // 프로토타입 Circle.prototype으로부터 getArea 메서드를 상속받는다.
// 즉, Circle 생성자 함수가 생성하는 모든 인스턴스는 하나의 getArea 메서드를 공유한다.
console.log(circle1.getArea === circle2.getArea); // true
console.log(circle1.getArea()); // 3.141592653589793
console.log(circle2.getArea()); // 12.566370614359172
```

- circle생성자 함수가 생성한 모든 인스턴스는 상위 객체 역할을 하는 circle.prototype의 모든 프로퍼티와 메서드를 상속받는다.

## 프로토타입 객체

- 모든 객체는 **prototype** 접근자 프로퍼티를 통해 자신의 프로토타입, 즉 [[Prototype]] 내부슬롯에 간접적으로 접근할수있다.
- **prototype** 은 접근자 프로퍼티이다 -> **prototype** 를 통해 프로토타입에 접근하면 재부적으로 **prototype** 접근자 프로퍼티의 getter함수인 [[Get]] 가 호출된다.
  -> 이렇게 접근자 프로토타입에 접근하기 위해 접근자 프로퍼티를 사용하는 이유 : **상호참조에 의해 프로토타입 체인이 생성되는것을 방지하기 위해서**
- 프로토타입체인은 단방향 링크드 리스트로 구현되어야한다.
  - 순환 참조하는 프로토타입 체인이 만들어지면 프로토타입 체인 종점이 존재하지않기때문에 프로토타입 체인에서 프로퍼티를 검색할때 무한 루프에 빠짐

## 프로토타입의 생성 시점

- 프로토타입은 생성자 함수가 생성되는 시점에 생성
- 생성자 함수로서 호출할수있는 함수인 constructor는 함수 정의가 평가되어 함수 객체를 생성하는 시점에 프로토타입도 더불어 생성된다.
- 객체가 생성되기 이전에 생성자 함수와 프로토타입은 이미 객체화 -> 이후 생성자 함수 또는 리터럴 표기법으로 객체를 생성하면 프로토타입은 생성된 객체의 [[Prototype]] 내부 슬롯에 할당됨

## 프로토타입 체인

```tsx
function Person(name) {
  this.name = name;
}
// 프로토타입 메서드
Person.prototype.sayHello = function () {
  console.log(`Hi! My name is ${this.name}`);
};
const me = new Person("Lee");
// hasOwnProperty는 Object.prototype의 메서드다.
console.log(me.hasOwnProperty("name")); // true
```

- Person 생성자 함수에 의해 생성된 me 객체는 Object.prototype의 메서드인 **hasOwnProperty**를 호출 가능 -> me 객체가 Person.prototype뿐만 아니라 Object.prototype도 상속받았다는 것을 의미

## 오버라이딩과 프로퍼티 섀도잉

- 오버라이딩: 상위클래스가 가지고있는 메서드를 하위 클래스가 재정의 하여 사용하는 방식
- 오버로딩: 함수의 이름은 동일하지만 매개변수의 타입 또는 개수가 다른 메서드를 구현하고 매개변수에 의해 메서드를 호출하는 방식
- 하위 객체를 통해 프로토타입의 프로퍼티를 변경 또는 삭제하는것은 불가능
  -> 하위 객체를 통해 get 엑세스는 허용, set 엑세스는 불허

## instanceof 연산자

- 이항연산자로서 좌변에 객체를 가리키는 식별자, 우변에 생성자 함수를 가리키는 식별자를 피연산자로 받는다.
- 우변의 생성자 함수의 **prototype 에 바인딩된 객체가 좌변의 객체의 프로토타입 체인상에 존재하면 true 아니면 false**
- 프로토타입의 construnctor프로퍼티가 가리키는 생성자 함수를 찾는것이 아니라 생성자 함수의 prototype에 바인딩된 객체가 프로토타입 체인 상에 존재하는지 확인한다.
