## 11_원시 값과 객체의 비교

- 원시 값은 변경 불가능한 값. 한번 생성된 원시 값은 읽기 전용 값으로서 변경할 수 없다.
- 값에 의한 전달
    
    ```jsx
    var score = 80;
    var copy = score;
    ```
    
    - score변수와 copy변수의 값 80은 다른 메모리 공간에 저장된 별개의 값이다.
- 객체는 프로퍼티의 개수가 정해져 있지 않으며, 동적으로 추가되고 삭제할 수 있다. 즉, 변경 가능한 값이다.
- 얕은 복사: 객체를 프로퍼티 값으로 갖는 개거체의 경우 한 단계까지만 복사하는 것
- 깊은 복사: 객체에 중첩되어 있는 객체까지 복사하는 것
- 참조에 의한 전달: 객체를 가리키는 변수를 다른 변수에 할당하면 원본의 참조 값이 복사되어 전달된다.
