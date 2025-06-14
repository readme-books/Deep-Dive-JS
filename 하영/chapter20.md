# chapter 20: strict mode

- 오타나 문법 지식의 미비로 인한 실수를 줄여 코드를 생산하기위해 나온 모드
- 적용하려면 전역의 선두 또는 함수 몸체의 선두에 use strict를 추가해야함
- 전역에 적용한 strict mode는 스크립트 단위로 적용된다.

## strict mode가 발생시키는 에러

- 암묵적 전역 : 선언하지 않은 변수를 참조시 referenceError
- delete 연산자로 변수, 함수, 매개변수 삭제시 syntaxError
- 매개변수 이름 중복시 syntaxError
- with 문 사용시 syntaxError

  - with문 사용시 동일한 객체의 프로퍼티를 반복해서 사용할때 객체 이름을 생략할수있음 -> 코드가 간단해지지만 성능과 가독성이 나빠짐

  ## strict mode 적용에 의한 변화

  - 일반함수 this
    strict mode에서 함수를 일반 함수로서 호출하면 this에 undefined가 바인딩
    -> 생성자 함수가 아닌 일반 함수 내부에서는 this를 사용할 필요가 없기 때문에.

- arguments 객체
  strict mode에서는 매개변수에 전달된 인수를 재할당하여 변경해도 arguments 객체에 반영되지 않는다.
