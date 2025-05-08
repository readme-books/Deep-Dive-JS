# chapter 16: 프로퍼티 어트리뷰트

## 내부 슬록과 내부 메서드

- JS 엔진의 구현알고리즘을 설명하기 위해 SCMAScript사양에서 사용하는 의사 프로퍼티와 의사 메서드 (JS의 내부로직임)
  ![Image](https://github.com/user-attachments/assets/21fb3fc3-34b3-475c-9b6c-7214afd32d76)
- JS 엔진에서 실제로 동작하지만 개발자가 직접 접근할수 있도록 외부로 공개된 객체의 프로퍼티는 아니다.

```tsx
const o = {};
// 내부 슬롯은 자바스크립트 엔진의 내부 로직이므로 직접 접근할 수 없다.
o.[[Prototype]] //  Uncaught SyntaxError: Unexpected token '[' // 단, 일부 내부 슬롯과 내부 메서드에 한하여 간접적으로 접근할 수 있는 수단을 제공하기는 한다.
o.__proto__ //  Object.prototype
```

## 프로퍼티 어트리뷰트와 프로퍼티 디스크립터 객체

- JS엔진은 프로퍼티를 생성할때 프로퍼티의 상태를 나타내는 프로퍼티 어트리 뷰트를 기본값으로 자동 정의
- 자바스크립트 엔진이 관리하는 내부 상태값 : **내부 슬롯** `[[Value]], [[Writable]], [[Enumerable]], [[Configurable]]`

```tsx
const person = { name: "Lee" };
// 프로퍼티 동적 생성
person.age = 20;
// 모든 프로퍼티의 프로퍼티 어트리뷰트 정보를 제공하는 프로퍼티 디스크립터 객체들을 반환한다.
console.log(Object.getOwnPropertyDescriptors(person));
/*
{
name: {value: "Lee", writable: true, enumerable: true, configurable: true}, age: {value: 20, writable: true, enumerable: true, configurable: true} }
*/
```

## 데이터 프로퍼티와 접근자 프로퍼티

- 데이터 프로퍼티: 키와 값으로 구성된 일반적인 프로퍼티

![Image](https://github.com/user-attachments/assets/1615a571-a0fc-465f-abe4-0b9b33481fac)

```tsx
const person = { name: "Lee" };
// 프로퍼티 동적 생성
person.age = 20;
console.log(Object.getOwnPropertyDescriptors(person));
/*
{
name: {value: "Lee", writable: true, enumerable: true, configurable: true}, age: {value: 20, writable: true, enumerable: true, configurable: true} }
*/
```

- 접근자 프로퍼티 : 자체적으로는 값을 갖지않고 다른 데이터 프로퍼티의 값을 읽거나 저장할때 호출되는 접근자 함수로 구정된 프로퍼티

```tsx
const person = {
  // 데이터 프로퍼티 firstName: 'Ungmo', lastName: 'Lee',
  // fullName은 접근자 함수로 구성된 접근자 프로퍼티다.
  // getter 함수
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },
  // setter 함수
  set fullName(name) {
    // 배열 디스트럭처링 할당: "31.1 배열 디스트럭처링 할당" 참고
    [this.firstName, this.lastName] = name.split(" ");
  },
};
// 데이터 프로퍼티를 통한 프로퍼티 값의 참조.
console.log(person.firstName + " " + person.lastName); // Ungmo Lee
// 접근자 프로퍼티를 통한 프로퍼티 값의 저장 // 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출된다.
person.fullName = "Heegun Lee";
console.log(person); // {firstName: "Heegun", lastName: "Lee"}
// 접근자 프로퍼티를 통한 프로퍼티 값의 참조 // 접근자 프로퍼티 fullName에 접근하면 getter 함수가 호출된다.
console.log(person.fullName); // Heegun Lee
// firstName은 데이터 프로퍼티다.
// 데이터 프로퍼티는 [[Value]], [[Writable]], [[Enumerable]], [[Configurable]] // 프로퍼티 어트리뷰트를 갖는다.
let descriptor = Object.getOwnPropertyDescriptor(person, "firstName");
console.log(descriptor);
// {value: "Heegun", writable: true, enumerable: true, configurable: true}
// fullName은 접근자 프로퍼티다.
// 접근자 프로퍼티는 [[Get]], [[Set]], [[Enumerable]], [[Configurable]] // 프로퍼티 어트리뷰트를 갖는다.
descriptor = Object.getOwnPropertyDescriptor(person, "fullName");
console.log(descriptor);
// {get: ƒ, set: ƒ, enumerable: true, configurable: true}
```

**프로토타입**

- 어떤 객체의 상위 객체의 역할을 하는 객체
- 하위 객체에게 자신의 프로퍼티와 메서드를 상속
- 프로토타입 객체의 프로퍼티나 메서드를 상속받은 하위 객체는 자신의 프로퍼티 또는 메서드인것처럼 자유롭게 사용할 수 있다.

## 프로퍼티 정의

- 새로운 프로퍼티를 추가하면서 프로퍼티 어트리뷰트를 명시적으로 정의하거나 기존 프로퍼티의 프로퍼티 어트리뷰트를 재정의하는것
- 프로퍼티값을 갱신가능하도록 할것인지 열거하도록 할것인지 정의할수 있음
  -> 이를 통해 객체의 프로퍼티가 어떻게 동작해야하는지를 명확히 정의할 수 있다.

## 객체 변경방지

- 객체 확장 금지
  :확장이 금지된 객체는 프로퍼티 추가가 금지됨
- 객체 밀봉
  : 밀봉된 객체는 읽기 쓰기만 가능
- 객체 동결
  : 프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의 금지, 프로퍼티 값 갱신 금지
  : 읽기만 가능함
  -> but, 중첩 객체까지 동결할 수 없음
- 불변 객체
  : 객체의 중첩 객체까지 동결하여 변경이 불가능한 읽기전용의 불변객체를 구현하려면 객체를 값으로 갖는 모든 프로퍼티에 대해 재귀적으로 Object.freeze메소드를 호출해야함
