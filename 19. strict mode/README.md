# 19. strict mode

## 암묵적 전역

```js
function foo() {
  x = 10;
}
foo();

console.log(x);
```

foo 함수를 호출하면 변수 x에 10을 할당하기 위해 **foo 함수 스코프에서 x 변수를 찾음** <br>
→ _없다면_ 상위 스코프인 **전역 스코프에서 찾음** <br>
→ _전역 스코프에도 없다면_ **암묵적으로 전역 객체에 x 프로퍼티를 동적 생성** <br>
→ x 프로퍼티는 _전역 변수처럼 사용할 수 있게됨_ (ReferenceError 발생 X) <br>
→ **암묵적 전역 현상**

이러한 잠재적인 오류를 줄이기 위해 ES5부터 **strict mode**가 추가됨 <br>
strict mode는 **JS의 문법을 좀 더 엄격히 적용**하여 오류를 발생시킬 가능성이 높거나<br>
JS 엔진의 최적화 작업에 문제를 일으킬 수 있는 코드에 대해 **명시적인 에러를 발생**시킨다.

### 사용 방법

전역의 맨 상단 또는 함수의 몸체 맨 상단에 `use strict`를 추가<br>
함수 상단에 추가하면 함수와 중첩 함수까지도 적용됨

```js
// 전역의 상단에 추가했을 때
'use strict';

function foo() {
  x = 10; // ReferenceError
}
foo();

// 함수 상단에 추가했을 때
function foo() {
  'use strict';
  x = 10; // ReferenceError
}
foo();
```

하지만 전역 단위로 strict mode를 적용하면 **script 단위로 적용**되기 때문에<br>
다른 스크립트에 영향을 주지 않고 해당 스크립트에 한정되어 적용된다.

```js
<html>
  <body>
    <script>'use strict'; // 여긴 엄격 모드가 적용 됨</script>
    <script>// 엄격 모드가 적용 안됨</script>
    <script>'use strict'; // 엄격 모드가 적용 됨</script>
  </body>
</html>
```

(어떤 스크립트는 엄격 모드를 적용하고 어떤 스크립트는 엄격 모드를 적용하지 않는 건 좀 이상함..)

또한 함수 단위로 strict mode를 적용하는 것도 마찬가지로<br>
함수 하나 하나에 엄격 모드를 적용하는 것은 번거로운 일이고<br>
엄격 모드가 적용된 함수가 참조할 외부 함수의 컨텍스트에 엄격 모드가 적용되지 않았다면 이 또한 문제가 될 수 있다.<br>
책에서는 즉시 실행 함수로 감싼 스크립트 단위로 strict mode를 적용하는 것이 바람직하다고 추천하고 있다.<br>

## strict mode 적용 시 변하는 부분

1. 일반 함수를 호출하면 this에 undefined가 바인딩된다

   ```js
   (function () {
     'use strict';
     function foo() {
       console.log(this); // undefined
     }
     foo();

     function Foo() {
       console.log(this); // Foo
     }
     new Foo();
   })();
   ```

2. 함수에 인수를 전달받아 내부에서 재할당해도 arguments 객체에는 반영되지 않는다
   (처음 전달받은 인수로 계속 가지고 있다)

   ```js
   (function (a) {
     'use strict';
     a = 2;

     console.log(arguments); // {0:1, length:1}
   })(1);
   ```
