## ⛹️‍♂️ 함수 선언식 - Function Declarations
- 일반적인 프로그래밍 언어에서의 함수 선언과 비슷한 형식이다.
```javascript
function 함수명(){
	구현 로직
}
// 예시
function funcDeclarations(){
  return 'A function declaration';
}
funcDeclarations(); // 'A function declaration'
```

## ⛹️‍♂️ 함수 표현식 - Function Expressions
- 자바스크립트 언어의 특징을 활용한 선언 방식
```javascript
var 함수명 = function(){
  구현 로직
}
//예시
var funcExpression = function(){
  return 'A function expression';
}
funcExpression(); // 'A function expression'
```

## ⛹️‍♂️ 함수 선언식과 표현식의 차이점
 - **함수 선언식은 호이스팅에 영향을 받지만**, **함수 표현식은 호이스팅 영향을 받지 않는다**.
 - 함수 선언식은 코드를 구현한 위치와 관게없이 js특징인 호이스팅에 따라 브라우저가 js를 해석할 때 맨 위로 끌어 올려진다.
 아래의 코드를 실행했을 때.
 ```javascript
// 실행 전
logMessage();
sumNumbers();
//
function logMessage() {
  return 'worked';
}
var sumNumbers = function () {
  return 10 + 20;
};
```
호이스팅에 의해 js해석기는 코드를 아래처럼 해석한다.

```javascript
// 실행 시
function logMessage() {
  return 'worked';
}
var sumNumbers;
logMessage(); // 'worked'
sumNumbers(); // Uncaught TypeError: sumNumbers is not a function
sumNumbers = function () {
  return 10 + 20;
};
```

실제 sumNumbers에 할당될 function 로직은 호출된 이후에 선언되므로, sumNumbers는 함수로 인식하지 않고 변수로 인식한다.

**<p style="color:brown">호이스팅을 제대로 모르더라도 함수와 변수를 가급적 코드 상단부에서 선언하면, 호이스팅으로 인한 스코프 꼬임 현상을 방지할 수 있다.</p>**


## ⛹️‍♂️ 함수 표현식의 장점
- '함수 표현식이 호이스팅에 영향을 받지 않는다.'라는 특징 이외에도 함수 선언식보다 유용하게 쓰이는 경우는 다음과 같다.
	- **클로져**로 사용
    - **콜백**으로 사용 (다른 함수의 인자로 넘길 수 있음)

### 함수 표현식으로 클로져 생성하기
- 클로져는 함수를 실행하기 전에 해당 함수에 변수를 넘기고 싶을 때 사용된다.
```javascript
function tabsHandler(index) {
    return function tabClickEvent(event) {
    // 바깥 함수인 tabsHandler() 의 index 인자를 여기서 접근할 수 있다.
        console.log(index); //탭을 클릭할 때 마다 해당 탭의 index 값을 표시
    };
}

var tabs = document.querySelectorAll('.tab');
var i;

for (i = 0; i < tabs.length; i += 1) {
    tabs[i].onclick = tabsHandler(i);
}
```
위 예제는 모든 .tab 요소에 클릭 이벤트를 추가하는 예제이다. 클로져를 이용해 tabClickEvent()에서 바깥 함수 tabHandler()의 인자 값 index를 접근했다는 점이다.
만약 클로져를 쓰지 않았다면 모든 tab의 index값이 for 반복문의 마지막 값인 tabs.length와 같다.
```javascript
// 클로져를 사용하지 않았을 때
var tabs = document.querySelectorAll('.tab');
var i;
var logIndex = function (event) {
  console.log(i); // 3
};

for (i = 0; i < tabs.length; i += 1) {
    tabs[i].onclick = logIndex;
}
```
logIndex가 실행되는 시점은 이미 for문의 실행이 모두 끝난 시점이다. 따라서, 어느 탭을 눌러도 for문의 최종 값인 3이 찍힌다.

## ⛹️‍♂️ 함수 표현식을 다른 함수의 인자 값으로 넘기기
- 함수 표현식은 일반적으로 임시 변수에 저장하여 사용한다.
```javascript
// doSth 라는 임시 변수를 사용
var doSth = function(){
};
```
- 함수 표현식을 임시 변수에 넣지 않고도 아래와 같이 콜백함수로 사용할 수 있다.
```javascript
$(document).ready(function(){
  console.log('An anonymous function'); // 'An anonymous function'
});
```
- 자바스크립트 내장 API인 forEach()를 사용할 때도 콜백함수를 사용 가능하다.
```javascript
var arr = ["a", "b", "c"];
arr.forEach(function () {
  // ...
});
```
- **콜백함수란 다른 함수의 인자로 전달된 함수를 의미한다. 자바스크립트가 일급 객체로서 가지는 특징 중 하나이다.**

<p style="color:brown">캡틴판교님의 블로그를 참고하였습니다.</p>
