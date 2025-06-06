## 07_연산자

- 연산자는 하나 이상의 표현식을 대상으로 산술, 할당, 비교, 논리, 타입, 지수 연산 등을 수행해 하나의 값을 만든다.
- 산술 연산자
    - 이항 산술 연산자: +, -, *, /, %
    - 단항 산술 연산자: ++, —, +, -
- 문자열 연결 연산자: +
- 할당 연산자: =, +=, -=, *=, /=, %=
- 비교 연산자: ==, ===, !=, !==
    - NaN === Nan; // false → Number.isNaN을 사용해서 비교한다.
    - - 0 === +0 // true
    - Object.is(-0, +0) // false
    - Object.is(NaN, NaN) // true
- 대소 관계 비교 연산자: >, <, >=, <=
- 삼항 조건 연산자: 조건식 ? true 일 때 변환값 : false일 때 변환값
- 논리 연산자: ||, &&, !
- typeof 연산자: 타입을 문자열로 반환한다.
- 지수 연산자: **
- 그 외의 연산자
    - ?.: 옵셔널 채이닝 연산자
    - ??: null 병합 연산자
    - delete: 프로퍼티 삭제
    - new: 생성자 함수를 호출할 때 사용하여 인스턴스를 생성
    - instanceof: 좌변의 객체가 우변의 생성자 함수와 연결된 인스턴스인지 판별
    - in: 프로퍼티 존재 확인
