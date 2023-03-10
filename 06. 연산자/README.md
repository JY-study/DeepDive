# 06. 연산자

연산자: 하나 이상의 표현식을 대상으로 산술, 할당, 비교, 논리, 타입, 지수 연산 등을 수행해 하나의 값을 만듦<br>
피연산자: 연산의 대상 → 값으로 평가될 수 있는 표현식이어야 함<br>
부수효과가 있는 연산자: 할당 연산자(`=`), 증가/감소 연산자(`++`/`--`), `delete` 연산자

## 산술 연산자

### 이항 산술 연산자

2개의 피연산자를 산술 연산하여 숫자 값을 만들며, 피연산자의 값을 변경하는 **부수 효과(side effect)가 없어**서<br>
어떤 산술 연산을 해도 피연산자의 값이 바뀌는 경우가 없다. <br>
언제나 새로운 값을 만든다.<br>
ex) `5 + 2 // -> 7`

### 단항 산술 연산자

1개의 피연산자를 산술 연산하여 숫자 값을 만든다.<br>
증가/감소(++/--) 연산자는 피연산자의 값을 변경하는 **부수 효과가 있다**. <br>
ex) `var x = 1; x++ // -> 2`

```js
let x = 1,
  result;

// 후위 증가 연산자, ++연산자는 피연산자의 값을 변경하는 암묵적 할당이 이루어짐
result = x++;

console.log(result); // 1
console.log(x); //2

let y = 1,
  result;

// 전위 증가 연산자, ++연산자는 피연산자의 값을 변경하는 암묵적 할당이 이루어짐
result = ++y;

console.log(result); // 2
console.log(x); //2
```

`-` 단항 연산자는 피연산자의 부호를 반전한 값을 반환하며 피연산자를 변경하지도 않고, 부수 효과도 없다. <br>
ex) `-’10’; // -> -10` `-true; // -> -1`

`+` 단항 연산자는 피연산자를 숫자 타입으로 변환한 값을 생성해서 반환해주며 피연산자를 변경하지도 않고, 부수 효과도 없다. <br>
ex) `var x = ‘1’; +x // -> 1` `x = true; +x // -> 1`

만약 피연산자 중 하나 이상이 문자열인 경우 문자열 연결 연산자로 동작한다. <br>
ex) `‘1’ + 2; // -> ‘12’`

이러한 동작으로 **개발자의 의도와는 상관 없이** 자바스크립트 엔진이 **암묵적으로 타입을 자동 변환** 시킬 수 있다. <br>
→ **암묵적 타입 변환**(= 타입 강제 변환)

## 할당 연산자

우항에 있는 피연산자의 평가 결과를 좌항에 있는 변수에 할당한다. <br>
-> 변수 값이 변하는 **부수 효과가 있다** <br>
할당문은 값으로 평가되는 표현식인 문으로서 할당된 값으로 평가된다. <br>
ex) `console.log(x = 10) // -> 10`

## 비교 연산자

좌항, 우항의 피연산자를 비교 후 결과를 불리언 값으로 반환한다.

**동등 비교(`==`)연산자**는 좌항, 우항의 피연산자를 비교할 때 먼저 **암묵적 타입 변환을 통해 타입을 일치**시킨 후 같은 값인지 비교한다. <br>
ex) `5 == ‘5’; // -> true` `fasle == ‘false’; // -> false`

**일치 비교 (`===`)연산자**는 **타입도 같고 값도 같은 경우**에만 true를 반환한다. <br>
단, `NaN`은 자신과 일치하지 않는 유일한 값이기 때문에 숫자가 NaN인지 확인하려면 `Number.isNaN`을 사용해야 한다.

**대소 관계 비교 연산자**는 피연산자의 크기를 비교하여 불리언 값을 반환한다. <br>
ex) `2 > 3; // -> false`

## 삼항 조건 연산자

조건식의 평가 결과에 따라 반환할 값을 결정한다.<br>
`조건식 ? 조건식이 true일 때 반환 값 : 조건식이 false일 때 반환 값`

만약 조건식의 평과 결과가 불리언 값이 아니면 **불리언 값으로 암묵적 타입 변환** 된다.<br>

```js
var x = 2;

var result = x % 2 ? '홀수' : '짝수';

// 2%2는 0이고 0은 false로 암묵적 타입 변환되어 짝수가 반환된다
console.log(result); // 짝수
```

## 논리 연산자

피연산자를 논리 연산한다. ( `&&`, `||`, `!` )

**드 모르간의 법칙** <br>
`!(x || y) === (!x && !y)`<br>
`!(x && y) === (!x || !y)`

## 지수 연산자

좌항의 피연산자를 밑으로, 우항의 피연산자를 지수로 거듭제곱 하여 숫자 값을 반환한다. <br>
ex) `2 ** 2; // -> 4` `2 ** 0; // -> 1`
