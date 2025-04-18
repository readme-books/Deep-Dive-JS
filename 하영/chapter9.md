# chapter9

## 🐩타입 변환이란?

- 기존 원시 값을 사용해 다른 타입의 새로운 원시 값을 생성하는것.
- **명시적 타입 변환(타입캐스팅)** : 개발자가 의도적으로 값의 타입을 변환하는것
- **암묵적 타입 변환(타입강제 변환)** : 개발자의 의도와 상관없이 표현식을 평가하는 도중에 자바스크립트 엔진에 의해 암묵적으로 타입이 자동 변환되는것
  - 기존 변수값을 재할당하여 변경하는것 X

### 🐾암묵적 타입 변환

```jsx
//피연산자가 모두 문자열 타입이어야하는 문맥
"10" + 2; // '102'

//피연산자가 모두 숫자 타입이어야하는 문맥
5 * "10"; // 50

//피연산자 또는 표현식이 불리언 타입이어야하는 문맥
!0; // true
if (1) {
}
```

- 암묵적 타입 변환이 발생하면 문자열, 숫자, 불리언과 같은 원시 타입 중 하나로 타입을 자동 변환

#### 1) 문자열 타입으로 변환

- 문자열 연결 연산자의 역할은 문자열 값을 만드는것.
  -> 문자열 연결 연산자의 모든 피연산자는 코드의 문맥상 모두 문자열 타입
- ES6 에서 도입된 템플릿 리터럴의 표현식 삽입은 표현식의 평가 결과를 문자열 타입으로 암묵적 타입 변환

```jsx
0 + ""; // "0"
true + ""; // "true"
null + ""; // "null"
undefined +
  ""(
    // "undefined"
    Symbol()
  ) +
  ""(
    // TypeError: cannot convert a Symbol value to a string
    {}
  ) +
  ""; // "[object Object]"
```

#### 2) 숫자 타입으로 변환

- 산술 연산자의역할은 숫자 값을 만드는것.
- JS 엔진은 산술 연산자 표현식을 평가하기 위해 산술연산자의 피연사중에서 숫자타입이 아닌 피연산자를 숫자 타입으로 암묵적 타입 변환한다.

```jsx
// 각 타입에 대한 예시 정리

+"" + // 0
  "string" + // NaN
  true + // 1
  null + // 0
  undefined + // NaN
  Symbol() + // TypeError: Cannot convert a Symbol value to a number
  {}; //NaN
```

#### 3) 불리언 타입으로 변환

- if 문/for 문 과 같은제어문 또는 삼황 조건 연산자의 조건식은 불리언 값으로 평가 되어야하는 표현식.
- JS엔진은 조건식의 평가 결과를 불리언 타입으로, 암묵적 타입 변환시킴.
- 아래 값들은 false로 평가되는 Falsy값
  > false , undefined, null , 0, -0, NaN, ''(빈 문자열)

### 🐾명시적 타입 변환

- 개발자 의도에 따라 명시적으로 타입 변경
- 표준 빌트인 생성자 함수(String, Number, Boolean)를 new 연산자 없이 호출하는 방법
- 빌트인 메서드를 사용하는 방법
- 암묵적 타입 변환을 이용하는 방법

#### 1) 문자열 타입으로 변환

> 1.  String 생성자 함수를 new 연산자 없이 호출하는방법
>
> ```jsx
> String(1); //'1'
> String(NaN); //'NaN'
> String(true); //'true'
> ```

> 2.  Object.prototype.toString메서드 사용하는 방법

```jsx
(1)
  .toString()(
    //'1'
    true
  )
  .toString(); //'true'
```

> 3.  문자열 연결 연산자를 이용하는 방법

```jsx
1 + ""; // '1'
true + ""; // 'true'
```

#### 2) 숫자 타입으로 변환

> 1. Number 생성자 함수를 new 연산자 없이 호출하는 방법
>
> ```jsx
> Number("0"); // 0
> Number("10.53"); // 10.53
> Number("true"); // 1
> ```

> 2. parseInt, parseFloat 함수를 사용하는 방법(문자열만 숫자 타입으로 변환 가능)
>
> ```jsx
> // 문자열 타입 => 숫자 타입
> parseInt("0"); // 0
> parseInt("-1"); // -1
> parseFloat("10.53"); // 10.53
> ```

> 3. +단항 산술 연산자를 이용하는 방법

```jsx
+"0"; // 0
+"10.53"; // 10.53
+true; // 1
```

> 4. \*산술 연산자를 이용하는 방법

```jsx
"0" * 1; // 0
"10.53" * 1; // 10.53
true * 1; // 1
```

#### 3) 불리언 타입으로 변환

> 1. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
>
> ```jsx
> Boolean("x"); // true
> Boolean(""); // false
> Boolean("false"); // true
> Boolean("0"); // false
> Boolean("1"); // true
> Boolean("NaN"); // false
> Boolean("Infinity"); // true
> Boolean("null"); // false
> Boolean("undefined"); // false
> Boolean("{}"); // true
> Boolean("[]"); // true
> ```

> 2. Boolean 생성자 함수를 new 연산자 없이 호출하는 방법
>
> ```jsx
> !!"x"; // true
> !!""; // false
> !!"false"; // true
> !!0; // false
> !!1; // true
> !!NaN; // false
> !!Infinity; // true
> !!null; // false
> !!undefined; // false
> !!{}; // true
> !![]; // true
> ```

### 🐾단축 평가

- 논리 연산의 결과를 결정하는 피연산자를 타입 변환하지 않고 그대로 반환하는것.
- 표현식을 평가하는 도중에 평가 결과가 확정된 경우 나머지 평가 과정을 생략하는 것

#### 1) 논리 연산자를 사용한 단축평가

- 논리곱(&&) 연산자는 논리 연산의 결과를 결정하는 두 번째 피연산자를 그대로 반환
  - 두 개의 피연산자가 모두 true로 평가될 때 true 반환
- 논리합(||) 연산자는 논리 연산의 결과를 결정한 첫 번째 피연산자를 그대로 반환
  - 두 개의 피연산자 중 하나만 true로 평가되어도 true 반환
- 단축 평가 사용 시 if문 대체 가능.
  - 어떤 조건이 Truthy 값(참으로 평가되는 값)일 때 무언가를 해야한다면 논리곱(&&) 연산자 표현식으로 if문 대체 가능.
  - 조건이 Falsy 값(거짓으로 평가되는 값)일 때 무언가를 해야한다면 논리합(||) 연산자 표현식으로 if문 대체 가능.
    > | 단축 평가 표현식      | 평가 결과  |
    > | --------------------- | ---------- |
    > | `true ㅣㅣ anything`  | `anything` |
    > | `false ㅣㅣ anything` | `anything` |
    > | `true && anything`    | `anything` |
    > | `false && anything`   | `false`    |

** \*단축평가의 유용한 패턴 **
(1) 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때

- 객체를 가리키기를 기대하는 변수의 값이 객체가 아니라 null 또는 undefined 인 경우 객체의 프로퍼티 참조시 타입에러 발생 => 프로그램 강제 종료

```jsx
var elem = null;
var value = elem.value; // TypeError: Cannot read property 'value' of null

// ---------단축 평가 사용---------------------------
var elem = null;
// elem이 null이나 undefined와 같은 Falsy 값이면 elem으로 평가
// elem이 Truthy 값이면 elem.value로 평가
var value = elem && elem.value; // null
```

(2) 함수 매개변수에 기본값을 설정할 때

- 함수를 호출할 때 인수를 전달하지 않으면 매개변수에 undefined 할당
  -> 단축 평가를 사용해 매개변수의 기본값을 설정하면 undefined로 인해 발생할 수 있는 에러 방지

```jsx
// 단축 평가를 사용한 매개변수의 기본값 설정
function getStringLength(str) {
  str = str || "";
  return str.length;
}

getStringLength(); // 0
getStringLength("hi"); // 2

//ES6 매개변수의 기본값 설정
function getStringLength(str = "") {
  return str.length;
}

getStringLength(); // 0
getStringLength("hi"); // 2
```

#### 2) 옵셔널 체이닝 연산자

- 좌항의 피연산자가 null 또는 undefined인 경우 undefined를 반환하고 그렇지 않으면 우항의 프로퍼티 참조를 이어감.
- 객체를 가리키기를 기대하는 변수가 null 또는 undefined가 아닌지 확인하고 프로퍼티를 참조할 때 유용.
- 옵셔널 체이닝 연산자는 좌항 피연산자가 false로 평가되는 Falsy 값(false, undefined, null, 0, -0, NaN,’’)이라도 null 또는 undefined라 아니면 우항의 프로퍼티 참조를 이어감

```jsx
var str = "";
//문자열의 길이(length)참조.
//좌항 피연산자가 false로 평가되는 Falsy 값이라도
//null or Undefined 가 아니면 우항 프로퍼티 참조
var length = str?.length;
console.log(length); //0
```

#### 3) null 병합 연산자

- 좌항의 피연산자가 null 또는 undefined 인 경우 우항의 피연산자를 반환하고, 그렇지 않으면 좌항의 피연산자를 반환.
- null병합 연산자 `??`는 변수에 기본값을 설정할때 유용.

```jsx
var foo = null ?? "default string";
console.log(foo); //"default string"
//좌항의 피연산자가 Falsy 값이라도 null or undefined가 아니면
//좌항의 피연산자를 반환함.
var foo = "" ?? "default string";
console.log(foo); // ""
```
