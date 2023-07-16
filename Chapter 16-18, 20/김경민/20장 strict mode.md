# 20장 strict mode
## 20.1 strict mode란?
```javascript
function foo() {
  x = 10;
}
foo();

console.log(x); //?
```

foo 함수 내에서 선언하지 않은 x 변수에 10을 할당함.
자바스크립트 엔진은 먼저 foo 함수의 스코프에서 x 변수의 선언을 검색하고 실패할 것임.
그 다음 상위 스코프 (예제의 경우 전역 스코프)에서 x 변수 선언 검색함.

전역 스코프에도 선언이 없기 때문에 ReferenceError 발생시킬 것 같지만, 암묵적으로 전역 객체에 x 프로퍼티를 동적 생성함.

전역 객체의 x 프로퍼티는 마치 전역 변수처럼 사용할 수 있음. 이를 암묵적 전역이라 함.

오류 발생시키는 원인 될 가능성 크므로, 반드시 var, let, const 키워드를 사용해서 변수 선언한 다음 사용하자.

ES6에서 도입된 클래스와 모듈은 기본적으로 strict mode가 적용됨.
<br><br>

## 20.2 strict mode의 적용
strict mode 적용하려면 전역의 선두 또는 함수 몸체의 선두에 'use strict';를 추가한다.
<br><br>

## 20.3 전역에 strict mode를 적용하는 것은 피하자.
전역에 적용한 strict mode는 스크립트 단위로 적용됨. <br>
strict mode 스크립트와 non-strict mode 스크립트 혼용은 오류 발생시킬 수 있음.<br>
특히, 외부 서드파티 라이브러리를 사용하는 경우 라이브러리가 non-strict mode인 경우도 있기 때문에, strict mode 적용은 바람직하지 않음. <br>
이 경우, 즉시 실행 함수로 스크립트 전체를 감싸서 스코프 구분하고, 즉시 실행 함수의 선두에 strict mode를 적용함.
<br><br>

## 20.4 함수 단위로 strict mode를 적용하는 것도 피하자.
일부 함수에만 strict mode를 적용하는 것은 바람직하지 않고, 모든 함수에 일일이 strict mode를 적용하는 것은 번거롭다. <br>
strict mode가 적용된 함수가 참조할 함수 외부의 컨텍스트에 strict mode를 적용하지 않으면 또한 문제가 발생할 수 있음. <br>

strict mode는 즉시 실행 함수로 감싼 스크립트 단위로 적용하는 것이 바람직하다.
<br><br>

## 20.5 strict mode가 발생시키는 에러
- 암묵적 전역: 선언하지 않은 변수 참조 시 ReferenceError 발생
- 변수, 함수, 매개변수의 삭제: delete 연산자로 변수, 함수, 매개변수 삭제하면 SyntaxError 발생.
- 매개변수 이름 중복: 중복된 매개변수 이름 사용 시 SyntaxError 발생
- With 문의 사용: with 문 사용하면 SyntaxError 발생. <br>
with 문은 전달된 객체를 스코프 체인에 추가함. <br> 
with 문은 동일한 객체의 프로퍼티를 반복해서 사용할 때 객체 이름을 생략할 수 있어서 코드가 간단해지는 효과가 있지만, 성능과 가독성이 나빠지므로 사용하지 않는 것이 좋다.
<br><br>

## 20.6 strict mode 적용에 의한 변화
### 20.6.1 일반 함수의 this
strict mode에서 함수를 일반 함수로 호출하면 this에 undefined가 바인딩 됨. <br>
생성자 함수가 아닌 일반 함수 내부에서는 this를 사용할 필요가 없기 때문. <br>
이 때 에러는 발생하지 않음.

### 20.6.2 arguments 객체
strict mode에서는 매개변수에 전달된 인수를 재할당하여 변경해도 arguments 객체에 반영되지 않는다.
