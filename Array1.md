## ⛹️‍♂️ 배열
```javascript
function get_members(){
  return ['durant','lebron','leonard'];
}
members = get_members();
// members.length는 배열에 담긴 값의 숫자를 알려준다.
for(let i=0; i<members.length; i++){
  //members[i].toUpperCase() 는 members[i]에 담긴 문자를 대문자로 변환해준다.
  document.write(members[i].toUpperCase());
}
```
![](https://images.velog.io/images/pji3504/post/15924dcc-f9f2-4843-a8ff-1c1f287c0299/image.png)

## ⛹️‍♂️ 배열의 조작
### 1. 추가
- 배열에 하나의 원소를 추가하는 방법, **push()**를 이용한다.
```javascript
var li=['a','b','c','d','e'];
li.push('f');
alert(li); // a,b,c,d,e,f
```

- 복수의 원소를 배열에 추가하는 방법 : **concat()**;
```javascript
var li = ['a', 'b', 'c', 'd', 'e'];
li = li.concat(['f', 'g']);
alert(li); // a,b,c,d,e,f,g
```

- 배열의 시작점에 원소를 추가하는 방법 : **unshift()**
```javascript
var li = ['a', 'b', 'c', 'd', 'e'];
li.unshift('z');
alert(li);  // z,a,b,c,d,e
```

- **splice()** : 첫번째 인자에 해당하는 원소부터 두번째 인자에 해당하는 원소의 숫자만큼 값을 배열로부터 제거한 후에 리턴한다. 그리고 세번째 인자부터 전달된 인자들을 첫번째 인자의 원소 뒤에 추가한다.
```javascript
var li = ['a', 'b', 'c', 'd', 'e'];
li.splice(2, 0, 'B');
alert(li); // a,b,B,c,d,e
```
### 2. 제거
- 배열의 첫번째 원소를 제거하는 방법 : **shift()**
```javascript
var li = ['a', 'b', 'c', 'd', 'e'];
li.shift();
alert(li);  // b,c,d,e
```
- 배열의 끝점의 원소를 배열 제거하는 방법 :** pop()**
```javascript
var li = ['a', 'b', 'c', 'd', 'e'];
li.pop();
alert(li);  // a,b,c,d
```

### 3. 정렬
- 오름차순 정렬 : **sort()**
```javascript
var li = ['c', 'e', 'a', 'b', 'd'];
li.sort();
alert(li);  // a,b,c,d,e
```
- 내림차순(역순) 정렬 : **reverse()**
```javascript
var li = ['c', 'e', 'a', 'b', 'd'];
li.reverse();
alert(li); // e,d,c,b,a
```
