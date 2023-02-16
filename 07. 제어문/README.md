# 07. 제어문

**블록문**이란 0개 이상의 문을 중괄호로 묶은 것으로, **자바스크립트는 블록문을 하나의 실행 단위로 취급**한다.<br>

## 조건문

**조건문**이란 주어진 **조건식의 평가 결과**에 따라 **코드 블록(블록문)의 실행을 결정**한다.

### if else 문

대부분 삼항 조건 연산자로 바꿔쓸 수 있는데<br>
실행해야 할 문이 **여러줄**이라면 **`if…else`를 사용**하는 것이 좋다.

```js
var result;

// if...else문 경우의 수가 2가지일 때
if (x % 2) {
  result = '홀수';
} else {
  result = '짝수';
}

// 삼항연산자 (경우의 수가 2가지이면 삼항연산자를 쓰는게 더 낫다)
var result = x % 2 ? '홀수' : '짝수';

// 경우의 수가 3가지일 때 삼항연산자
var result = num ? (num > 0 ? '양수' : '음수') : 'zero';

// if...else문 경우의 수가 3가지 일 때
// 확실히 삼항 연산자보단 낫다
if (num > 0) {
  result = '양수';
} else if (num < 0) {
  result = '음수';
} else {
  result = 'zero';
}
```

### switch 문

주어진 표현식을 평가하여 그 값과 일치하는 표현식을 갖는 `case 문`으로 실행 흐름을 옮긴다.<br>
`if…else`문의 조건식은 불리언 값으로 평가되어야 하지만,<br>
`switch`문의 표현식은 **문자열이나 숫자 값**인 경우가 많아서<br>
`if…else`문처럼 논리적 참, 거짓보다는 **다양한 상황에 따라 실행할 코드 블록을 결정할 때 사용**한다.

case 문 마지막에 `break`를 사용하지 않으면 전체 case를 실행하고 **마지막 default문까지 실행**하는 `fall through(폴스루)`가 되기 때문에<br>
case 문 마지막엔 꼭 `break`를 사용해야 한다.

```js
switch (food) {
  case '떡볶이':
    alert('맛있다!');
    break;
  case '피자':
    alert('이것도 맛있다!');
    break;
  case '샐러드':
    alert('이건 좀...');
    break;
  default:
    alert('무난무난;');
}
```

보통 `if…else`문으로 해결할 수 있다면 `switch`문 보다 `if…else`문을 사용하는 편이 좋고,<br>
만약 조건이 너무 많아서 `switch`문을 사용했을 때 가독성이 더 좋다면 `switch`문을 사용하자

## 반복문

조건식의 **평가 결과가 참**인 경우 **코드 블록을 실행**하며,<br>
이후 조건식이 여전히 참인 경우 코드 블록을 다시 실행, **조건식이 거짓일 때까지 반복**된다.

### for 문

변수 선언문 실행 → 조건식 실행 - 코드 블록 실행 → 증감식 실행 → 조건식이 참이면 반복, 거짓이면 중단

### while 문

주어진 조건식의 평가 결과가 참이면 코드 블록을 계속해서 반복 실행<br>
조건식의 **평가 결과가 언제나 참이면 무한루프**가 되므로 코드 블록 내에 **`if`문으로 탈출 조건을 만들고 `break`문으로 탈출**

```js
var count = 0;
// 무한루프
while (true) {
  count++;
  // 탈출구 만들기
  if (count === 3) break;
}

// do...while 문
// count가 3보다 작을 때까지 do 코드 블록을 계속 반복 실행
// 만약 조건식이 거짓이어도 처음 한번은 무조건 실행된다
do {
  console.log(count);
  count++;
} while (count < 3);
```

❗️ `for`문은 **반복 횟수가 명확**할 때, `while`문은 **반복 횟수가 불명확**할 때 사용한다.

### break 문

`레이블문, 반복문, switch문`의 코드 블록을 탈출할 때 사용<br>
이외의 코드 블록에서 사용하면 문법 에러가 발생!

```js
// 외부 for문을 탈출하려면 레이블 문을 사용해야 한다
// 레이블 문: outer처럼 식별자가 붙은 문
// 레이블문은 아래와 같이 중첩된 for문 외부로 탈출할 때에만 사용하자
// (가독성 나쁘고 오류 발생 가능성 있음)
outer: for (var i = 0; i < 5; i++) {
  for (var j = 0; j < 3; j++) {
    if (i + j === 3) {
      console.log(`i는 ${i}, j는 ${j} 합은 3!!`);
      break outer;
    }
    console.log(`inner [${i}, ${j}]`);
  }
}
console.log('Done!!');
```

### continue 문

반복문의 코드 블록 실행을 **현재 지점에서 중단**하고 **다시 위로 올라가서 반복 실행**

```js
var string = 'Hello World';
var search = 'l';
var count = 0;

for (var i = 0; i < string.length; i++) {
  if (string[i] !== search) continue;

  // contine문이 실행되면 이 문은 실행되지 않는다
  count++;
}

console.log(count);
```
