
  
## 콜백 함수 (CallBack Function) 란?
=======================================

#### 콜백함수란 파라미터로 함수를 전달 받아, **함수의 내부**에서 수행하는 함수이다.

#### function sequence
- javascript 함수는 정의된 순서가 아니라 호출 된 순서대로 실행된다
```javascript
function myFirst() {
  myDisplayer("Hello");
}
function mySecond() {
  myDisplayer("Goodbye");
}
myFirst();   // "Hello"가 출력된 뒤
mySecond();   // "Goodbye"가 출력된다.
```

## 🏀 callback ex)
- 콜백을 사용하면 콜백과 함께 myCalculator함수를 호출할 수 있고 계산이 완료된 후 myCalculator함수가 콜백을 실행하도록 할 수 있다.
```javascript
function myDisplayer(some) {
  document.getElementById("demo").innerHTML = some;
}
function myCalculator(num1, num2, myCallback) {
  let sum = num1 + num2;
  myCallback(sum);
}
myCalculator(5, 5, myDisplayer);  // 10
```

## 🏀 콜백함수의 사용원칙
- **익명의 함수 사용**
```javascript
let number = [1,2,3,4,5];
number.forEach(function(x){
	console.log(x*3); // 3,6,9,12,15
});
```
콜백함수는 이름이 없는 '익명의 함수'를 사용한다. 함수의 내부에서 실행되기 때문에 이름을 붙이지 않는다.

- **함수의 이름만 넘기기**
```javascript
function whatYourName(name, callback) {
    console.log('name: ', name);
    callback();
}
function finishFunc() {
    console.log('finish function');
}
whatYourName('durant', finishFunc);
//name: durant
//finish function
```
자바스크립트는 null과 undefined를 타입을 제외하고 모든 것을 객체로 다룬다.
함수를 변수 or 다른 함수의 변수처럼 사용할 수 있다. 함수를 콜백함수로 사용할 경우, 함수의 이름만 넘겨주면 된다.
따라서 위의 예제에서, 함수를 인자로 사용할 때 callback, finishFunc처럼 ()를 붙일 필요가 없다.

- **전역변수, 지역변수 콜백함수의 파라미터로 전달 가능**
```javascript
let guard = 'pg';	// Global Variable

function callbackFunc(callback) {
    let forward = 'sf';	// Local Variable
    callback(forward);
}

function play(forward) {
    console.log(`guard: ${guard} / forward: ${forward}`);
}

callbackFunc(play);
// guard: pg / forward: sf
```

## 🏀 콜백함수 사용 시 주의할 점
- this를 사용한 콜백 함수
```javascript
let userData = {
    signUp: '2021-06-12 19:48:00',
    id: 'durant',
    name: 'Not Set',
    setName: function(firstName, lastName) {
        this.name = firstName + ' ' + lastName;
    }
}

function getUserName(firstName, lastName, callback) {
    callback(firstName, lastName);
}

getUserName('Kevin', 'durant', userData.setName);

console.log('1: ', userData.name);
console.log('2: ', window.name);

<output>
1: Not Set
2: Kevin durant
```
첫번째 콘솔의 값이 Kevin durant가 아니라 Not set이 출력되는 이유:
setName() 함수가 실행되기 전의 name 값이 나오는 것인데 이는 getUserName()이 전역함수이기 때문이다.

**해결방안 : call()과 apply()를 사용하여 this를 보호할 수 있다.**
- call() : 첫번째 인자로 this 객체 사용, 나머지 인자들은 , 으로 구분
- apply() : 첫번째 인자로 this 객체 사용, 나머지 인자들은 배열 형태로 전달
```javascript
// call 사용
let userData = {
    signUp: '2021-06-12 19:48:00',
    id: 'durant',
    name: 'Not Set',
    setName: function(firstName, lastName) {
        this.name = firstName + ' ' + lastName;
    }
}
function getUserName(firstName, lastName, callback, obj) {
    callback.call(obj, firstName, lastName); // (1)
}
getUserName('Kevin', 'durant', userData.setName, userData);	// (2)
console.log(userData.name); // Kevin durant
```
(2)에서 마지막 인자에 담긴 userData는 (1)에서 call 함수의 첫번째 인자로 전달된다. call() 함수에 의해서 userData에 this 객체가 매핑된다.

```javascript
// apply()도 인자를 배열로 전달한다는 점만 다르고 동일하게 작동함
let userData = {
    signUp: '2021-06-12 19:48:00',
    id: 'durant',
    name: 'Not Set',
    setName: function(firstName, lastName) {
        this.name = firstName + ' ' + lastName;
    }
}
function getUserName(firstName, lastName, callback, obj) {
    callback.apply(obj, [firstName, lastName]);
}

getUserName('Kevin', 'durant', userData.setName, userData);

console.log(userData.name); // Kevin durant
```

**<p style="color:brown">콜백 함수는 비동기 함수에서 빛을 발한다.</p>**

## 🏀 콜백지옥 (callback hell)
비동기호출이 자주 일어나는 프로그램의 경우, '콜백 지옥'이 발생한다.
함수의 매개변수로 넘겨지는 콜백 함수가 **반복**되어 코드의 들여쓰기 수준이 감당하기 힘들어질 정도로 깊어지는 현상을 말한다.
```javascript
function add(x, callback) {
    let sum = x + x;
    console.log(sum);
    callback(sum);
}
add(2, function(result) {
    add(result, function(result) {
        add(result, function(result) {
            console.log('finish!!');
        })
    })
})
// 4 8 16 finish!!
```
**해결방안 : Promise를 사용**하여 콜백지옥을 탈출할 수 있다.
- 아래의 코드는 Promise 정상 수행 후 resolve, 실패 후 reject가 실행된다. callback을 사용했던 것과 마찬가지로 resolve에 값을 담아 전달한다.
하지만 결국 콜백지옥처럼 들여쓰기 수준을 감당하기 힘들어진다.
```javascript
function add(x) {
    return new Promise((resolve, reject) => {
        let sum = x + x;
        console.log(sum);
        resolve(sum);
    })
}
add(2).then(result => {
    add(result).then(result => {
        add(result).then(result => {
            console.log('finish!!');
        })
    })
})
// 4 8 16 finish!!
```
**해결방안 :Promise의 return을 사용하여 Promise Hell을 탈출할 수 있다.**
```javascript
function add(x) {
    return new Promise((resolve, reject) => {
        let sum = x + x;
        console.log(sum);
        resolve(sum);
    })
}
add(2).then(result => {
    return add(result);
}).then(result => {
    return add(result);
}).then(result => {
    console.log('finish!!');
})
// 4 8 16 finish!!
```







<p style="color:brown">참고 사이트 <br>https://www.w3schools.com/js/js_callback.asp<br>https://velog.io/@minidoo/%EC%9E%90%EB%B0%94%EC%8A%A4%ED%81%AC%EB%A6%BD%ED%8A%B8-%EC%BD%9C%EB%B0%B1-%ED%95%A8%EC%88%98Callback-Function</p>
