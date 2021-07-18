
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
```
const arrow = () => {...};
```
