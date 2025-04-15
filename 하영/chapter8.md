# ⚽️제어문

- 조건에 따라 블록을 실행(조건문) 하거나 반복실행(반복문)할 때 사용.
- 제어문을 사용하면 코드의 실행 흐름을 인위적으로 제어 가능.
- 코드의 흐름을 이해하기 어렵게 만들어 가독성을 해치는 단점이 있음.

## 🏀블록문

- 0개이상의 문을 중괄호로 묶은것으로 코드 블록 또는 블록이라고 부름.
- 단독으로 사용할 수 있으나 일반적으로 제어문이나 함수 정의시 사용.
- 문의 끝에는 세미클론(;)을 붙이는게 일반적이나 블록문 끝에는 붙이지 않는다.

> ```jsx
> //블록문
> {
>   var foo = 10;
> }
>
> //제어문
> var x = 1;
> if (x < 10) {
>   x++;
> }
>
> //함수선언문
> function sum(a, b) {
>   return a + b;
> }
> ```

## 🏀조건문

- 주어진 조건식의 평가 결과에 따라 코드 블록(블록문)의 실행을 결정.
- 불리언 값으로 평가될 수 있는 표현식

### 1)`if...else문`

- 주어진 조건식의 평가 결과 -> 논리적 참 또는 거짓에 따라 실행할 코드블록 결정.
- 조건식의평가 결과 true => if문의 코드블록 실행 / false -> else문 코드 블록 실행
- 만약 if 문에 불리언 값이 아닌 값으로 평가되면 자바스크립트 엔진에 의해 암묵적으로 불리언 값으로 강제 변환 -> 실행할 코드 블록 결정
- 조건식을 늘리려면 if & else if문을 사용
- if...else는 대부분 `삼황 조건 연산자` 로 바꿀수 있음.
  > ```jsx
  > var x = 2;
  > car result = x % 2 ?'홀수' : '짝수';
  > console.log(result); // 짝수
  > ```
- 삼황조건 연산자는 값으로 평가되는 식을 만듦.
- 조건에 따라 단순히 값을 할당 ==> `삼황 조건 연산자`
- 조건에따라 실행해야할 내용이 복잡하여 여러줄의 문 필요 ==> `if...else`

### 2)`switch문`

- 주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 case 문으로 실행 흐름을 옮긴다.
- 논리적 참,거짓 보다는 다양한 상황(case)에 따라 실행할 코드 블록을 결정할 때 적합.
- `break`문을 사용해서 case문에 해당하는 코드 블록에서 탈출
- `default`문에는 break문을 생략.
  > ```jsx
  > switch (표현식) {
  > ```
      case 표현식1:
      	switch 문의 표현식과 표현식1이 일치하면 실행될 문;
      	break;
      case 표현식2:
      	switch 문의 표현식과 표현식2가 일치하면 실행될 문;
      	break;
      default:
      	switch 문의 표현식과 일피하는 case 문이 없을 때 실행될 문;
  }
  > ```
  >
  > ```

## 🏀반복문

- 조건식의 평가 결과가 참인 경우 코드 블록 실행->조건식을 다시 평가하여참인 경우 코드블록 다시 실행.
- 조건식이 거짓일때까지 반복됨.

### 1) for 문

- 조건식이 거짓으로 평가될 때까지 코드 블록 반복 실행
- for문의 변수 선언문, 조건식, 증감식은 모두 옵션이므로 반드시 사용할 필요 X.

> ```jsx
>  for (변수 선언문 또는 할당문; 조건삭; 증감식;) {
> ```

    	조건식이 참인 경우 반복 실행될 문;
    }

> ```
>
> ```

![](https://velog.velcdn.com/images/hayoung78/post/8fcf70f4-eed2-46e4-85f5-0066adc98154/image.jpeg)

### 2) while문

- 주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실헹
- for문은 반복 횟수가 명확할 때 주로 사용하고 while문은 반복 횟수가 불명확할 때 주로 사용
- while문은 조건문의 평가 결과가 거짓이 되면 코드 블록을 실행하지 않고 종료
- 조건식의 평가 결과가 불리언 값이 아니면 불리언 값으로 강제 변환하여 논리적 참, 거짓 구별
  ```jsx
  var count = 0;

  //count가 3보다 작을 때까지 코드 블록을 계속 반복 실행
  while (count < 3) {
    console.log(count); // 0, 1, 2
    count++;
  }
  ```

### 3) do … while문\*\*

- 코드 블록을 먼저 실행하고 조건식 평가
  -> 코드 블록은 무조건 한 번 이상 실행
  ```jsx
  var count = 0;

  // count가 3보다 작을 때까지 코드 블록을 계속 반복 실행
  do {
    console.log(count); // 0, 1, 2
    count++;
  } while (count < 3);
  ```

## 🏀break문\*\*

- 코드 블록 탈출.
- 레이블 문, 반복문(for, for … in, for … of, while, do … while) 또는 switch문의 코드 블록 탈출.

> ```jsx
>
> ```

    if (true) {
    	break; // Uncaught SyntaxError: Illegal break statement
    }

>

    //foo 라는 레이블 식별자가 붙은 레이블 문
    foo: console.log('foo');

>

    //foo 라는 레이블 식별자가 붙은 레이블 블록문
    foo: {
    	console.log(1);
    	break foo; // foo 레이블 블록문 탈출
    	console.log(2);
    }
    console.log('Done!');

> ```
>
> ```

- 중첩된 for문의 내부 for문에서 break문을 실행하면 내부 for문을 탈출,외부 for문으로 진입
  -> 내부 for문이 아닌 외부 for문을 탈출하려면 레이블 문 사용

> ```jsx
>
> ```

    outer: for (var i = 0; i < 3; i++) {
    	for (var j = 0; j < 3; j++) {
    		// i + j === 3이면 outer라는 식별자가 붙은 레이블 for문 탈출
    		if (i + j === 3) break outer;
    		console.log(`inner [${i}, ${j}]`);
    	}
    }
    console.log('Done!');

> ```
>
> ```

- 레이블 문은 중첩된 for문 외부로 탈출할 때 유용, 그 밖의 경우에는 일반적으로 권장 X
- break문은 레이블 문뿐 아니라 반복문, switch문에서도 사용 가능.
  -> break문에 레이블 식별자 지정 X
- break문은 반복문의 불필요한 반복을 회피할 수 있어 유용.

## 🏀continue 문

- 반복문의 코드 블록 실행을 현 지점에서 중단하고 반복문의 증감식으로 실행 흐름을 이동시킴.

  > ```jsx
  >
  > ```

      var string = 'Hello World.';
      var search = 'l';
      var index;

  >

      // 문자열은 유사 배열이므로 for문으로 순회가능
      for (var i = 0; i < string.length; i++) {
      	// 'l'이 아니면 현 지점에서 실행을 중단하고 반복문의 증감식으로 이동
      if (string[i] !== search) continue
      	count++; // continue문이 실행되면 이 문은 실행되지 않음
      }

  >

      console.log(count); // 3
      // 참고로 String.prototype.indexOf 메서드를 사용해도 같은 동작
      const regexp = new RegExp(search, 'g');
      console.log(string.match(regexp).length); // 3

  > ```
  >
  > ```

- if 문 내에서 실행해야할 코드가 길다면 => continue문
