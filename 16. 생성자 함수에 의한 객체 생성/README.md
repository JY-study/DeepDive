# 16. 생성자 함수에 의한 객체 생성

## 생성자 함수

생성자 함수란 **new 연산자와 함께 호출하여 객체(인스턴스)를 생성하는 함수**이며<br>
_이 함수에 의해 생성된 객체_ 를 **인스턴스**라고 한다.

같은 프로퍼티를 갖는 객체를 여러개 생성해야 할 경우에<br>
객체 리터럴을 사용하여 생성하면 하나의 객체만 생성하기 때문에 비효율적이므로<br>
생성자 함수를 사용하는 것을 추천한다.

```js
// 객체 리터럴로 생성
const circle1 = {
	radius: 5,
	getDiameter() {...}
}

const circle2 = {
	radius: 10,
	getDiameter() {...}
}
```

생성자 함수로 객체를 생성한다면 _템플릿_ 처럼 **프로퍼티 구조가 동일한 객체 여러 개를 간단히 생성할 수 있다.**

```js
// 생성자 함수로 생성
function Circle(radius) {
  // (this: 객체 자신의 프로퍼티나 메서드를 참조하기 위한 자기 참조 변수)
  this.radius = radius;
	this.getDiameter = function() {...}
}

const circle1 = new Circle(5);
const circle2 = new Circle(10);

console.log(circle1.getDiameter === circle2.getDiameter); // false
```

⇒ 생성자 함수의 역할은 **프로퍼티 구조가 동일한 인스턴스를 생성하기 위한 템플릿(클래스)**으로 동작하여<br>
인스턴스를 생성하는 것과 생성된 인스턴스를 초기화(인스턴스 프로퍼티 추가 및 초기값 할당)하는 것!

이 때 인스턴스를 생성하는 것은 필수, 생성된 인스턴스를 초기화(constructor)하는 것은 옵션이다.

## 인스턴스 생성 및 초기화 과정

1. **인스턴스 생성과 this 바인딩**

   **new 연산자**를 이용해 생성자 함수를 호출하면 암묵적으로 빈 객체(→ 인스턴스)가 생성된다.<br>
   이 인스턴스는 this에 바인딩되어 **생성자 함수 내부의 this가 인스턴스를 가리키게 된다.**<br>
   (바인딩: 식별자와 값을 연결하는 과정)

2. **인스턴스 초기화**

   생성자 함수에 있는 코드가 한 줄씩 실행되어 this에 바인딩 되어 있는 인스턴스를 초기화한다.<br>
   → this에 바인딩되어 있는 인스턴스에 프로퍼티나 메서드를 추가하고<br>
   _인수로 전달받은 초기값_ 을 **인스턴스 프로퍼티에 할당**하여 초기화 또는 고정값 할당

3. **인스턴스 반환**

   완성된 인스턴스가 바인딩된 this를 암묵적으로 반환한다.<br>
   만약 명시적으로 return 문을 사용하여 다른 값을 반환한다면 생성자 함수의 기본 동작을 훼손하는 것이므로<br>
   생성자 함수 내부에서 return문은 반드시 생략해야 한다.

```js
function Circle(radius) {
	// 1. 암묵적으로 빈 객체가 생성되고 this가 바인딩 됨
	// console.log(this) -> Circle {}

	// 2. this에 바인딩되어 있는 인스턴스를 초기화
	this.radius = radius;
	this.getDiameter = function() {...}

	// 3. 완성된 인스턴스가 바인딩된 this가 암묵적으로 반환됨
	// return {} -> 명시적으로 객체를 반환하면 암묵적인 this 반환이 무시됨. {}이 반환된다
	// return 100 -> 명시적으로 원시 값을 반환하면 원시 값 반환은 무시되고 this가 반환됨
}

// 인스턴스 생성. Circle 생성자 함수는 함묵적으로 this를 반환
const circle1 = new Circle(1);
console.log(circle); // Circle {radius: 1, getDiameter: ƒ}
```

## `[[Call]]`, `[[Construct]]`

함수는 객체이지만 일반 객체와는 다르다. → 일반 객체는 호출할 수 없지만 함수는 호출할 수 있다. <br>
함수는 `[[Call]]`, `[[Construct]]` 같은 내부 메서드를 추가로 가지고 있다.

```js
function foo() {...}

// 일반적인 함수로서 호출될 때 [[Call]]이 호출
foo();

// 생성자 함수로서 호출될 때 [[Construct]]가 호출
new foo();
```

| 함수 객체 유형  | 설명                                                                                                                            |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------- |
| callable        | 내부 메소드 `[[Call]]`을 갖고 있는 함수 객체. 일반적인 함수 객체에 해당.                                                        |
| constructor     | 내부 메소드 `[[Construct]]`를 갖고 있는 함수 객체. new 연산자와 함께 생성자로서 사용 가능한 함수 객체에 해당.                   |
| non-constructor | 내부 메소드 `[[Construct]]`를 갖지 않는 함수 객체. 일반적인 함수 객체 중 new 연산자로 생성자로 사용할 수 없는 함수 객체에 해당. |

호출할 수 없는 객체는 함수 객체가 아니므로 함수 객체는 반드시 callable이어야 한다. <br>
즉, **함수 객체는 callable이면서 constructor이거나, callable이면서 non-constructor이다.**

<img width='600px' src='https://user-images.githubusercontent.com/85178602/229357874-5250234d-bb6b-4324-977c-3b022e6615ab.png' />

constructor와 non-constructor를 구분하는 방법은 **함수 정의 방식**이다.<br>
**constructor**: 함수 선언문, 함수 표현식, 클래스
**non-constructor**: 메서드 축약 표현, 화살표 함수

```js
function foo() {}
const bar = function () {};
const baz = {
  x: function () {},
};

new foo(); // foo { __proto__: { constructor: ƒ foo() } }
new bar(); // bar { __proto__: { constructor: ƒ bar() } }
new baz.x(); //x { __proto__: { constructor: ƒ x() } }

const arrow = () => {};

const obj = {
  // 메서드 축약 표현
  x() {},
};
new arrow(); // TypeError: arrow is not a constructor
new obj.x(); // TypeError: obj.x is not a constructor
```

## `new.target`

생성자 함수가 _new 연산자 없이 호출되는 것을 방지_ 하기 위해 파스칼 케이스 컨벤션을 사용해도 실수는 언제나 발생할 수 있다.<br>
이런 위험성을 회피하기 위해 ES6에서는 **`new.target`을 지원**한다.

함수 내부에서 `new.target`을 사용하면 `new 연산자`와 함께 **생성자 함수로서 호출됐는지 확인**할 수 있다.<br>
→ **new 연산자와 함께 생성자 함수로서 호출**되면 **함수 내부의 new.target은 함수 자신**을 가리키며, 아니라면 `undefined`이다.

`new.target`으로 확인했을 때 만약 new 연산자로 생성되지 않은 생성자 함수라면<br>
new 연산자와 함께 **재귀 호출**을 통해 생성자 함수로서 호출할 수 있다

```js
function Circle(radius) {
  this.radius = radius;
  this.getDiameter = function () {};
}

const circle = Circle(4);
// console.log(circle.radius) Error
console.log(radius); // 4

// new.target으로 확인
function Circle(radius) {
  if (!new.target) {
    return new Circle(radius);
  }
  this.radius = radius;
  this.getDiameter = function () {};
}

const circle = Circle(4);
console.log(circle.radius); // 4
```

`new.target`은 this와 유사하게 constructor인 모든 함수 내부에서 암묵적인 지역 변수와 같이 사용되며 메타 프로퍼티라 한다.
