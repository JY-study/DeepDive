# 17. 함수와 일급 객체

## 일급객체

> **일급 객체**란?

1. 런타임에 생성이 가능하다 = 무명의 리터럴로 생성할 수 있다.
2. 변수나 자료구조(객체, 배열 등)에 저장할 수 있다.
3. 함수의 매개변수에 전달할 수 있다.
4. 함수의 반환값으로 사용할 수 있다.
   >

```js
// 1. 함수는 무명의 리터럴로 생성할 수 있다
// 2. 함수는 변수에 저장할 수 있다
const increase = function (num) {
  return ++num;
};
const decrease = function (num) {
  return --num;
};

// 2. 함수는 객체에 저장할 수 있다
const cal = { increase, decrease };

// 3. 함수의 매개변수에 전달할 수 있다
// 4. 함수의 반환값으로 사용할 수 있다
function makeCounter(cal) {
  let num = 0;
  return function () {
    num = cal(num);
    return num;
  };
}

// 3. 함수는 매개변수에 전달할 수 있다
const increaser = makeCounter(cal.increase);
console.log(increaser); // 1
console.log(increaser); // 2
```

함수는 객체이지만 일반 객체와는 차이가 있다.

| 객체 유형 | 설명                                                                           |
| --------- | ------------------------------------------------------------------------------ |
| 일반 객체 | 함수처럼 호출할 수 없고, 함수의 고유 프로퍼티를 갖지 않는 객체                 |
| 함수 객체 | 함수처럼 호출할 수 있으며, 일반 객체에는 없는 함수의 고유 프로퍼티를 갖는 객체 |

## arguments

arguments **객체는 인수의 순서를 key**, **인수를 value**로 가진다.<br>
2개의 인자를 전달해야하는 함수에 인자를 전달하지 않거나 1개만 전달해도 에러는 발생하지 않고,<br>
3개 이상의 인수를 전달해도 에러가 발생하지 않는다.

전달해야하는 인자보다 적게 전달했다면 전달되지 않은 매개변수는 `undefined`로 초기화 된 상태를 유지하며,<br>
더 많이 전달한 매개변수는 무시된다.

무시된 매개변수는 버려지는 것이 아니라 **arguments 객체에 보관**된다.

```js
function square(x, y) {
  console.log('arguments', arguments);
  return x * y;
}

square(1); // NaN | 'arguments' {0: 1}
square(1, 2, 3); // 2 | 'arguments' {0: 1, 1: 2, 2: 3}

function foo() {
  for (let i = 0; i < arguments.length; i++) {
    console.log(arguments[i]);
  }
}

foo(1, 2, 3); // 1, 2, 3
```

ES6에서는 `Rest 파라미터`를 통해 여러개의 인자를 받을 수 있게 됐다.

```js
function foo(...args) {
  args.forEach((el) => console.log(el));
}

foo(1, 2, 3); // 1, 2, 3
```

## prototype 프로퍼티

\_\_proto\_\_는 `[[Prototype]]` 내부 슬롯이 가리키는 프로토타입 객체에 접근하기 위해 사용하는 접근자 프로퍼티이다.<br>
(`[[Prototype]]`같은 내부 슬롯에는 직접 접근할 수 없기 때문! 15번 주제 참고!)

`prototype 프로퍼티`는 생성자 함수로 호출할 수 있는 함수 객체인 **constructor만 소유하는 프로퍼티**다.<br>
함수가 객체를 생성하는 생성자 함수로 호출될 때 생성자 함수가 생성할 인스턴스의 프로토타입 객체를 가진다.<br>
일반 객체나 생성자 함수로 호출할 수 없는 non-constructor에는 prototype 프로퍼티가 없다.

```js
(function () {}.hasOwnProperty('prototype')); // true
({}.hasOwnProperty('prototype')); // false
```
