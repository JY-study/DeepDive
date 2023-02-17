# 08. 타입 변환과 단축평가

## 명시적 타입 변환 (타입 캐스팅)

개발자가 **의도적**으로 값의 타입을 변환하는 것

```js
// 문자열 타입으로 변환
String(1); // '1'
(1).toString(); // '1'

// 숫자 타입으로 변환
Number('1'); // 1

// 불리언 타입으로 변환
Boolean(1); // true
```

## 암묵적 타입 변환 (타입 강제변환)

개발자의 **의도와는 상관없이** 표현식을 평가하는 중 **JS 엔진에 의해 타입이 자동 변환** <br>
기존 변수 값을 재할당하여 변경하는 것이 아니라,<br>
표현식을 에러 없이 평가하기 위해 **피연산자의 값을 암묵적 타입 변환**해 새로운 타입의 값을 만들어 사용

```js
// 문자열 타입으로 변환
1 + ''; // '1'

// 숫자 타입으로 변환
('1'); // 1

// 불리언 타입으로 변환
!!'1'; // true
```

❗️ 명시적 타입이든 암묵적 타입이든 중요한건 **코드를 예측할 수 있어야 한다**는 것이 중요하다!

## 단축평가

논리 연산의 결과를 결정하는 **피연산자를 타입 변환하지 않고 그대로 반환** <br>
표현식을 평가하는 도중에 _평가결과가 확정된 경우 나머지 평가 과정을 생략_ 하는 것

```js
// 'Cat'이 true여도 두번째 피연산자까지 평가해보아야 평가 결과를 알 수 있다
// 논리 연산의 결과를 결정하는 것은 두 번째 피연산자이므로 'Dog'를 그대로 반환한다
'Cat' && 'Dog'; // 'Dog'

// 'Cat'이 Truthy 값이므로 두 번째 피연산자까지 평가하지 않아도 평가 결과를 알 수 있다
// 'Cat'을 그대로 반환한다
'Cat' || 'Dog'; // 'Cat'
```

1. 변수가 `null` 또는 `undefined`가 아닌지 확인하고 프로퍼티를 참조할 때

   ```js
   let element = null;
   let error = element.value; // TypeError: ~~
   let value = element && element.value; // null
   ```

2. 함수 매개변수에 `기본값`을 설정할 때

   ```js
   function getStringLength(str) {
     str = str || '';
     return str.length;
   }

   getStringLength(); // -> 0
   getStringLength('hi!'); // -> 3

   // 매개변수의 기본값을 설정할 수도 있다
   function getStringLength(str = '') {
     return str.length;
   }

   getStringLength(); // -> 0
   getStringLength('hi!'); // -> 3
   ```

## 옵셔널 체이닝 연산자(`?.`)

좌항의 피연산자가 `null` 또는 `undefined`인 경우 **`undefined`를 반환**, 아니라면 우항의 프로퍼티 참조 <br>
옵셔널 체이닝 연산자는 **`falsy` 값**이라도 **`null`, `undefined`가 아니라면 우항의 프로퍼티 참조**를 이어감 <br>

↔ `논리곱(&&)`을 사용하여 좌항 피연산자의 값이 `null`, `undefined인`지 확인할 때 `falsy 값, 0, ‘’`이라면 **좌항 피연산자를 그대로 반환** <br>

```js
let str = '';
// str('')이 falsy 값으로 평가되어 length를 참조하지 못하고 좌항인 str이 평가된다
let length = str && str.length; // ''

let str = '';
// str이 falsy 값이어도 null 또는 undefined가 아니여서 length를 참조하여 평가된다
let length = str?.length; // 0
```

## null 병합 연산자(`??`)

좌항의 피연산자가 `null` 또는 `undefined`인 경우 **우항의 피연산자를 반환**, 아니라면 좌항의 피연산자를 반환<br>
변수에 기본값을 설정할 때 유용하다<br>

```js
// 좌항의 피연산자 ''가 falsy 값이어서 우항의 피연산자가 반환된다
let str = '' || 'default string'; // 'default string'

// 좌항의 피연산자가 falsy 값이어도 null 또는 undefined가 아니여서 좌항의 피연산자를 반환한다
let str = '' ?? 'defalut string'; // ''
// 좌항의 피연산자가 null이므로 우항의 피연산자를 반환한다
let str = null ?? 'default string'; // 'default string'
```
