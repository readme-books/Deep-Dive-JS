## 16_프로퍼티 어트리뷰트

- 내부 슬롯과 내부 매서드
    - 자바스크립트 엔진의 구현 알고리즘을 설명하기 위해 ECMAScript 사양에서 사용하는 의사 프로퍼티와 의사 매서드 이다.
- 자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티의 상태를 나타내는 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.
- 프로퍼티
    - 데이터 프로퍼티 - 키와 값으로 구성된 일반적인 프로퍼티.(Value, Writable, Enumerable, Configurable)
    - 접근자 프로퍼티 - 자체적으로는 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 호출되는 접근자 함수로 구성된 프로퍼티(Get, Set, Enumerable, Configurable)
- 객체 변경 방지
    - 객체 확장 금지 - Object.preventExtensions: 확장 금지된 객체는 프로퍼티 추가가 금지된다
    - 객체 밀봉 - Object.seal: 밀봉된 객체는 읽기와 쓰기만 가능하다. 프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의가 금지된다.
    - 객체 동결 - Object.freeze: 프로퍼티 추가 및 삭제와 프로퍼티 어트리뷰트 재정의 금지, 프로퍼티 값 갱신 금지. 동결된 객체는 읽기만 가능하다.
    - 불변 객체 - 불변 객체를 구현하려면 객체를 값으로 갖는 모든 프로퍼티에 대해 재귀적으로 freeze를 호출해야한다.
