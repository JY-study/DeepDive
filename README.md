# DeepDive 독서하기

## 목차

[1. 프로그래밍](https://github.com/JY-study/DeepDive/tree/main/01.%20프로그래밍) <br>
[2. 자바스크립트](https://github.com/JY-study/DeepDive/tree/main/02.%20자바스크립트) <br>
[3. 변수](https://github.com/JY-study/DeepDive/tree/main/03.%20변수) <br>
[4. 표현식과 문](https://github.com/JY-study/DeepDive/tree/main/04.%20표현식과%20문) <br>
[5. 데이터 타입](https://github.com/JY-study/DeepDive/tree/main/05.%20데이터%20타입) <br>
[6. 연산자](https://github.com/JY-study/DeepDive/tree/main/06.%20연산자) <br>
[7. 제어문](https://github.com/JY-study/DeepDive/tree/main/07.%20제어문) <br>
[8. 타입 변환과 단축평가](https://github.com/JY-study/DeepDive/tree/main/08.%20타입%20변환과%20단축평가) <br>
[9. 객체 리터럴](https://github.com/JY-study/DeepDive/tree/main/09.%20객체%20리터럴) <br>
[10. 원시 값과 객체의 비교](https://github.com/JY-study/DeepDive/tree/main/10.%20원시%20값과%20객체의%20비교) <br>
[11-1. 함수 (1)](<https://github.com/JY-study/DeepDive/tree/main/11-1.%20함수%20(1)>) <br>
[11-2. 함수 (2)](<https://github.com/JY-study/DeepDive/tree/main/11-2.%20함수%20(2)>) <br>
[12. 스코프](https://github.com/JY-study/DeepDive/tree/main/12.%20스코프) <br>
[13. 전역 변수의 문제점](https://github.com/JY-study/DeepDive/tree/main/13.%20전역%20변수의%20문제점) <br>
[14. let, const와 블록 레벨 스코프](https://github.com/JY-study/DeepDive/tree/main/14.%20let,%20const와%20블록%20레벨%20스코프) <br>
[15. 프로퍼티 어트리뷰트](https://github.com/JY-study/DeepDive/tree/main/15.%20프로퍼티%20어트리뷰트) <br>
[16. 생성자 함수에 의한 객체 생성](https://github.com/JY-study/DeepDive/tree/main/16.%20생성자%20함수에%20의한%20객체%20생성) <br>
[19. strict mode](https://github.com/JY-study/DeepDive/tree/main/19.%20strict%20mode)

## 독서하면서 메모했던 부분

- **크로스 브라우징**: 브라우저에 따라 웹페이지가 정상적으로 동작하지 않는 것
- **렌더링**: HTML, CSS, JS로 작성된 문서를 해석하여 브라우저에 시각적으로 출력하는 것
  - **SSR**: 서버에서 데이터를 HTML로 변환하여 브라우저에게 전달
- **I/O**: Input, Output의 약자
- **REPL**(Read Eval Print Loop): 입력 수행 출력 반복
- **예약어**: 프로그래밍 언어에서 사용되고 있거나 사용될 예정인 단어
- **UTF-16**: 0개 이상의 16비트 유니코드 문자
- **개행문자**: 텍스트의 한 줄이 끝남을 표시하는 문자 또는 문자열
- **이스케이프 시퀀스**: 백슬래시(`\`)로 시작하는 것 (ex. `\t`, `\’`)
- Object.is(one, two)
- **immutable value**: 변경 불가능한 값 → 원시값
- **인스턴스**: 클래스에 의해 생성되어 메모리에 저장된 실체 / 클래스는 인스턴스를 생성하기 위한 템플릿의 역할을 함
- **얕은 복사**: 객체의 한 단계 깊이만 복사하는 것
- **깊은 복사**: 객체에 중첩되어 있는 모든 단계 깊이를 복사하는 것
- **함수형 프로그래밍**: 순수 함수를 통해 부수 효과를 최대한 억제하여 오류를 피하고 프로그램의 안정성을 높이려는 프로그램 패러다임
  - **순수 함수**: 외부 상태를 변경하지 않고 외부 상태에 의존하지도 않는 함수
- **TDZ**: 스코프의 시작 지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간
- **추상화**: 다양한 속성 중 프로그램에 필요한 속성만 간추려 표현하는 것
