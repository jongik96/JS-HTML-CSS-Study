
# 화살표 함수 (Arrow Function)

### 화살표 함수 정의

화살표 함수는 함수 선언문으로 정의할 수 없고 함수 표현식으로 정의해야한다. 
호출 방식은 기존 함수와 동일하다.

```javascript
const multiply = (x,y) => x*y;
multiply(2,3); //6
```

### 매개변수 선언
- 매개변수가 여러 개인 경우 소괄호 () 안에 매개변수를 선언한다.
```javascript
const arrow = (x,y) => { ... };
```

- 매개변수가 한 개인 경우 소괄호 () 를 생략할 수 있다.
```javascript
const arrow = x => {...};
```

- 매개변수가 없는 경우 소괄호 ()를 생략할 수 없다.
```javascript
const arrow = () => {...};
```

### 함수 몸체 정의
- 함수 몸체가 하나의 문으로 구성된다면 함수 몸체를 감싸는 중괄호 {} 를 생략할 수 있다.
  이 때 함수 몸체 내부의 문이 값으로 평가될 수 있는 표현식인 문이라면 암묵적으로 반환된다.
```javascript
//concise body (간결한 표현)
const power = x => x **2;
power(2); // 4

// 위 표현은 다음과 동일
const power = x => {return x ** 2;};
```

- 함수 몸체를 감싸는 중괄호 {} 를 생략한 경우 함수 몸체 내부의 문이 표현식이 아닌 문이라면 에러가 발생한다. 
  표현식이 아닌 문은 반환할 수 없기 때문
```javascript
const arrow = () => const x = 1; // SyntaxError : Unexpected token 'const'

// 위 표현은 다음과 같이 해석된다.
const arrow = () => {return const x = 1;};
```

- 따라서 함수 몸체가 하나의 문으로 구성된다 해도 함수 몸체의 문이 표현식이 아닌 문이라면 중괄호를 생략할 수 없다.
```javascript
const arrow = () => { const x = 1;};
```

- 객체 리터럴을 반환하는 경우 객체 리터럴을 소괄호 () 로 감싸주어야 한다.
```javascript
const create = (id, content) => ({ id, content });
create(1, 'Javascript'); // {id: 1, content: "Javascript"}

// 위 표현은 아래와 동일하다
const create = (id, content) => {return {id,content};};
```

- 객체 리터럴을 소괄호 () 로 감싸지 않으면 객체 리터럴의 중괄호 {}를 함수 몸체를 감싸는 중괄호 {}로 잘못 해석한다.
```javascript
const create = (id,content) => {id, content};
create(1, "Javascript"); // undefined
```

- 함수 몸체가 여러 개의 문으로 구성된다면 함수 몸체를 감싸는 중괄호 {}를 생략할 수 없다. 이 때 반환값이 있다면 명시적으로 반환해야한다.
```javascript
const sum(a,b) => {
  const result = a+b;
  return result;
};
```

- 화살표 함수도 즉시 실행 함수로 사용할 수 있다.
```javascript
const person = (name =>({
  sayHi(){ return `Hi? My name is ${name}.`;}
}))("Park");

console.log(person.sayHi()); // Hi? My name is Park.
```

- 화살표 함수도 일급 객체이므로 map, filter, reduce 같은 고차함수에 인수로 전달할 수 있다.
  이 경우 일반적인 함수 표현식보다 표현이 간결하고 가독성이 좋다.
```javascript
//ES6
[1,2,3].map(v => v*2); // [2,4,6]
```

### 이처럼 화살표 함수는 콜백 함수로서 정의할 때 유용하다. 화살표 함수는 표현만 간략한 것만이 아니다.
### 화살표 함수는 일반 함수의 기능을 간략화했으며 this도 편리하게 설계되었다.
----------------------------
## 화살표 함수와 일반 함수의 차이

### 1. 화살표 함수는 인스턴스를 생성할 수 없는 non-constructor이다.

```javascript
const Foo = () => {};
// 화살표 함수는 생성자 함수로서 호출할 수 없다.
new Foo(); // TypeError: Foo is not a constructor
```

- 화살표 함수는 인스턴스를 생성할 수 없으므로 prototype 프로퍼티가 없고 프로토타입도 생성하지 않는다.
```javascript
const Foo = () => {};
//화살표 함수는 prototype 프로퍼티가 없다.
Foo.hasOwnProperty('prototype'); // false
```

### 2. 중복된 매개변수 이름을 선언할 수 없다.
- 일반함수는 중복된 매개변수 이름을 선언해도 에러가 발생하지 않는다.
```javascript
function normal(a,a) {return a+a;}
console.log(normal(1,2)); //4
```

- 단, stric mode에서 중복된 매개변수 이름을 선언하면 에러가 발생한다.
```javascript
'use strict';
function normal(a,a) {return a + a; }
// SyntaxError: Duplicate parameter name not allowed in this context
```

- 화살표 함수에서도 중복된 매개변수 이름을 선언하면 에러가 발생한다.
```javascript
const arrow = (a,a) => a+a;
//SyntaxError: Duplicate parameter name not allowed in this context
```

### 3. 화살표 함수는 함수 자체의 this, arguments, super, new, target 바인딩을 갖지 않는다.
- 따라서 화살표 함수 내부에서 this, arguments, super, new, target을 참조하면 스코프체인을 통해 상위 스코프의 this,arguments,super,new,target을 참조한다.
- 만약 화살표 함수와 화살표 함수가 중첩되어 있다면 상위 화살표 함수에도 this, arguments, super, new, target 바인딩이 없으므로 스코프 체인 상에서 
  가장 가까운 상위 함수 중에서 화살표 함수가 아닌 함수의 this,arguments,new,super,target을 참조한다.


##### 'use strict'모드가 뭐지
- MDN 사이트에서는 이렇다고 한다.

1. 기존에는 조용히 무시되던 에러들을 throwing합니다.
2. JavaScript 엔진의 최적화 작업을 어렵게 만드는 실수들을 바로잡습니다. 가끔씩 엄격 모드의 코드는 비-엄격 모드의 동일한 코드보다 더 빨리 작동하도록 만들어집니다.
3. 엄격 모드는 ECMAScript의 차기 버전들에서 정의 될 문법을 금지합니다.
