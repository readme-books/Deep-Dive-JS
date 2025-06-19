# chapter 21 : 빌트인 객체

## 표준 빌트인 객체

Math, Reflext. JSON을 제외한 표준 빌트인 객체는 모두 인스턴스를 생성할수있는 생성자 함수 객체

- 프로토타입 메서드와 정적 메서드를 제공하고 생성자함수 객체가 아닌 표준 빌트인 객체는 정적 메서드만 제공

```tsx
// String 생성자 함수에 의한 String 객체 생성 const strObj = new String('Lee');	// String {"Lee"} console.log(typeof strObj);	 // object
// Number 생성자 함수에 의한 Number 객체 생성
const numObj = new Number(123); // Number {123} console.log(typeof numObj);	 // object
// Boolean 생성자 함수에 의한 Boolean 객체 생성
const boolObj = new Boolean(true); // Boolean {true} console.log(typeof boolObj);	 // object
// Function 생성자 함수에 의한 Function 객체(함수) 생성
const func = new Function("x", "return x * x"); // ƒ anonymous(x ) console.log(typeof func); // function
// Array 생성자 함수에 의한 Array 객체(배열) 생성
const arr = new Array(1, 2, 3); // (3) [1, 2, 3] console.log(typeof arr);	 // object
// RegExp 생성자 함수에 의한 RegExp 객체(정규 표현식) 생성 const regExp = new RegExp(/ab+c/i);	// /ab+c/i console.log(typeof regExp);	 // object
// Date 생성자 함수에 의한 Date 객체 생성 const date = new Date();	 // Fri May 08 2020 10:43:25 GMT+0900 (대한민국 표준시)
console.log(typeof date); // object
```

- 표준 빌트인 객체는 인스턴스 없이도 호출 가능한 빌트인 정적 메서드를 제공

```tsx
// Number 생성자 함수에 의한 Number 객체 생성
const numObj = new Number(1.5); // Number {1.5}
// toFixed는 Number.prototype의 프로토타입 메서드다.
// Number.prototype.toFixed는 소수점 자리를 반올림하여 문자열로 반환한다.
console.log(numObj.toFixed()); // 2
// isInteger는 Number의 정적 메서드다.
// Number.isInteger는 인수가 정수(integer)인지 검사하여 그 결과를 Boolean으로 반환한다.
console.log(Number.isInteger(0.5)); // false
```

## 표준 빌트인 생성자 함수가 존재하는 이유 : 원시값과 래퍼 객체

- 원시값이 있는데도 문자열 , 숫자, 불리언 객체를 생성하는 표준 빌트인 생성자 함수가 존재하는이유
  -> 원시값을 객체처럼 사용하면 자바스크립트 엔진은 암묵적으로 연관된 객체를 생성하여 생성된 객체로 프로퍼티에 접근하거나 메서드를 호출하고 다시 원시값으로 되돌린다.
  => 문자열, 숫자, 불리언 값에 대해 객체처럼 접근하면 생성되는 임시객체를 **래퍼 객체**라고 함
- 문자열, 숫자, 불리언, 심벌 이외의 원시값 즉 null과 undefined은 래퍼 객체를 생성하지않는다.

## 전역 객체

- 코드가 실행되기 이전 단계에서 자바스크립트 엔진에 의해 어떤 객체보다도 먼저 생성되는 특수한 객체 (어느 객체에도 속하지않은 최상위 객체)
- 계층적 구조상 어떤 객체에도 속하지않은 모든 빌트인 객체의 최상위 객체
- 전역객체의 프로퍼티와 메서드는 전역 객체를 가리키는 식별자 window나 global을 생략하여 참조/호출할수있으므로 전역변수와 전역 함수처럼 사용할 수 있다.

## 빌트인 전역 프로퍼티와 전역 함수

- 빌트인 전역 프로퍼티 : 전역 객체의 프로퍼티
- 빌트인 전역 함수 : 애플리케이션 전역에서 호출할 수 있는 빌트인 함수 , 전역 객체의 메서드

(1) eval

```tsx
// 표현식인 문
eval("1 + 2;"); //  3
// 표현식이 아닌 문 eval('var x = 5;'); //  undefined
// eval 함수에 의해 런타임에 변수 선언문이 실행되어 x 변수가 선언되었다.
console.log(x); // 5
// 객체 리터럴은 반드시 괄호로 둘러싼다.
const o = eval("({ a: 1 })");
console.log(o); // {a: 1}
// 함수 리터럴은 반드시 괄호로 둘러싼다.
const f = eval("(function() { return 1; })");
console.log(f()); // 1
```

- 문자열을 인수로 받아 전달받은 **문자열 코드가 표현식이라면** eval 함수는 **문자열 코드를 런타임에 평가하여 값 생성**, 전달 받은 인수가 표현식이 **아니라면 문자열 코드를 런타임에 실행**
- 인수로 전달받은 문자열 코드가 여러개 문으로 이루어져있다면 모든 문을 실행한 다음, 마지막 결과값을 반환
- **인수**로 전달받은 문자열 코드가 Let, const를 사용한 **변수 선언문**이라면 암묵적으로 **strict 모드**가 적용
- 자신이 호출된 위치에 해당하는 기존의 스코프를 런타임에 동적으로 수정
- strict mode에서 기존의 스코프를 수정하지않고 eval 함수 자신의 자체적인 스코프를 생성
- eval로 실행되는 코드는 자바스크립트 엔진에 의해 최적화가 수행되지않으므로 일반적인 코드 실행에 비해 처리속도 느림 -> 금지해야한다

(2) isFinite

- 인수가 정상적인 유한수인지 검사하여 true / false를 반환
- 인수 타입이 숫자가 아닌경우 , 숫자로 변환후 검사를 수행 (new일경우 false)
- null은 true반환(숫자 타입으로 변환시 0이므로)

(3) encodeURI / decodeURI

- encodeURI : 완전한 URI를 문자열로 전달받아 이스케이프 처리를위해 인코딩 한다.
  ![image](https://github.com/user-attachments/assets/94bdb0a0-0885-4cdf-8c27-0a26ba953ba3)

  - 인코딩: URI 문자들을 이스케이프 처리하는것. 네트워크를통해 정보를 공유할때 어떤 시스템에서도 읽을수 있는 아스키 문자 셋으로 변환

- decodeURI : 인코딩된 URI를 인수로 전달 받아 이스케이프 처리 이전으로 디코딩
