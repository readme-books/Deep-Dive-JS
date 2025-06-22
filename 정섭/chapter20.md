## 20_Strict Mode

- strict mode(엄격 모드)
    - 자바스크립트 언어의 문법을 좀 더 엄격히 적용하여 오류를 발생시킬 가능성이 높거나 자바스크립트 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 대해 명시적인 에러를 발생한다.
    - ESLint 같은 린트 도구를 사용해도 strict mode와 유사한 효과를 얻을 수 있다.
    - strict mode를 적용하려면 전역의 선두 또는 함수 몸체의 선두에 ‘use strict’;를 추가한다.
    - 외부 서드파티 라이브러리를 사용하는 경우 non-strict mode인 경우도 있기 때문에 전역에 strict mode를 적용하는 것은 바람직하지 않다.
    - 따라서 strict mode는 즉시 실행 함수로 감싼 스크립트 단위로 적용하는 것이 바람직하다.
        
        ```tsx
        // 즉시 실행 함수의 선두에 strict mode 적용
        (function () {
        	'use strict'
        	
        	// Do something...
        }());
        ```
        
- strict mode가 발생 시키는 에러
    - 암묵적 전역 - 선언하지 않은 변수를 참조하면 ReferenceError가 발생한다.
    - 변수, 함수, 매개변수의 삭제 - delete 연산자로 변수, 함수, 매개변수를 삭제하면 SyntaxError가 발생한다.
    - 매개변수 이름의 중복 - 중복된 매개변수 이름을 사용하면 SyntaxError가 발생한다.
    - with 문의 사용 - with 문을 사용하면 SyntaxError가 발생한다. with 문의 사용은 성능과 가독성에 나빠지는 문제가 있다.
- strict mode 적용에 의한 변화
    - 일반 함수의 this - stirct mode 에서 함수를 일반함수로서 호출하면 thisDP undefined가 바인딩된다.
    - arguments 객체 - 매개변수에 전달된 인수를 재할당하여 변경해도 arguments 객체에 반영되지 않는다.
        
        ```tsx
        (function (a) {
        	'use strict';
        	// 매개변수에 전달된 인수를 재할당하여 변경
        	a = 2;
        	
        	// 변경된 인수가 arguments 객체에 반영되지 않는다.
        	console.log(arguments); // {0: 1, length: 1}
        )(1));
        ```
