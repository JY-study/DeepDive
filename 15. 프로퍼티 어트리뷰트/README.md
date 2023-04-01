# 15. 프로퍼티 어트리뷰트

(조금 어렵)

## 프로퍼티 어트리뷰트 / 프로퍼티 종류

프로퍼티 어트리뷰트란 **프로퍼티의 상태를 나타내는 것**이며, 자바스크립트 엔진이 관리하는 내부 상태값인 **내부 슬롯**<br>
내부 슬롯은 **자바스크립트 엔진의 내부 로직**이므로 직접 접근할 수는 없고 _\_\_proto\_\_를 통해 간접 접근_ 은 가능하다 <br>

| 상태                      | 설명                                                                      |
| ------------------------- | ------------------------------------------------------------------------- |
| 값(value)                 | 프로퍼티에 저장된 값                                                      |
| 갱신 가능(writable)       | 프로퍼티의 값이 변경 가능한지 여부                                        |
| 열거 가능(enumerable)     | 프로퍼티가 for...in 루프나 Object.keys() 메서드 등으로 열거 가능한지 여부 |
| 재정의 가능(configurable) | 프로퍼티의 속성을 변경할 수 있는지 여부                                   |

자바스크립트 엔진은 프로퍼티를 생성할 때 프로퍼티 어트리뷰트를 기본값으로 자동 정의한다.

- **프로토타입**: 어떤 객체의 상위 객체(부모)역할을 하는 객체, 하위 객체(자식)에게<br>
  자신의 프로퍼티와 메서드를 상속하며 **상속받은 하위 객체는 자신의 프로퍼티 또는 메서드인 것처럼 자유롭게 사용할 수 있다.**
- **프로토타입 체인**: 프로토타입이 **단방향 리스트 형태**로 연결되어 있는 **상속 구조**
- **프로퍼티 디스크립터**: 모든 프로퍼티의 **프로퍼티 어트리뷰트 정보를 제공하는 객체**인데, <br>
  `Object.getOwnPropertyDescriptors`메서드를 통해 프로퍼티 디스크립터 객체들을 반환한다.

**데이터 프로퍼티**: **키와 값**으로 구성된 일반적인 프로퍼티

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/86b0b933-f6d1-4dab-b162-bad8d9ccbe75/Untitled.png)

**접근자 프로퍼티**: 자체적으로 값을 갖지 않고 다른 데이터 프로퍼티의 값을 읽거나 저장할 때 <br>
호출되는 **접근자 함수(getter/setter)**로 구성된 프로퍼티

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/712436b0-ad90-4252-9e60-d97924b59a83/Untitled.png)

![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/94588453-8ed3-4b2d-9c3b-1672d64ea653/Untitled.png)

```js
const person = {
  // 데이터 프로퍼티
  firstName: 'Ungmo',
  lastName: 'Lee',
  // getter 함수 (접근자 프로퍼티)
  get fullName() {
    return `${this.firstName} ${this.lastName}`;
  },
  // setter 함수 (접근자 프로퍼티)
  set fullName(name) {
    [this.firstName, this.lastName] = name.split(' ');
  },
};

// 데이터 프로퍼티를 통한 프로퍼티 값의 참조
console.log(person.firstName + ' ' + person.lastName); // 'Ungmo Lee'

// 접근자 프로퍼티를 통한 프로퍼티 값의 참조
// 접근자 프로퍼티 fullName에 접근하면 getter 함수가 호출
console.log(person.fullName); // 'Ungmo Lee'

// 접근자 프로퍼티를 통한 프로퍼티 값의 저장
// 접근자 프로퍼티 fullName에 값을 저장하면 setter 함수가 호출
person.fullName = 'Heegun Lee'; // 'Heegun Lee'
console.log(person); // {
//  firstName: 'Heegun',
//  lastName: 'Lee',
//  fullName: [Getter/Setter]
// }
```

## 프로퍼티 정의

프로퍼티 정의란 _새로운 프로퍼티를 추가_ 하며 **프로퍼티 어트리뷰트를 명시적으로 정의**하거나,<br>
**기존 프로퍼티의 프로퍼티 어트리뷰트를 재정의** 하는 것

- `Object.defineProperty, Object.defineProperties`메서드를 사용하여 정의 및 재정의 할 수 있음
- `Object.preventExtensions` 객체의 확장 금지 → 프로퍼티 추가 금지
- `Object.seal` 객체를 밀봉 → 프로퍼티 추가, 삭제, 어트리뷰트 재정의 금지 → 읽기와 쓰기(갱신)만 가능 → `프로퍼티 어트리뷰트의 configurable이 false`
- `Object.freeze` 객체 동결 → 프로퍼티 추가, 삭제, 어트리뷰트 재정의, 값 갱신 금지 - 읽기만 가능 → `프로퍼티 어트리뷰트의 writable, configurable이 false`

객체 변경을 금지하는 위 세가지 메서드는 얕은 변경을 방지하는 것일 뿐 중첩 객체까지는 영향을 주지 못한다. <br>
중첩 객체까지 변경을 금지하고 싶다면 (불변 객체를 구현하고 싶다면) 재귀적으로 메서드를 호출해야 한다.
