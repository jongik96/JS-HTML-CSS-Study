- 이전 글에서 팔로우팔로워 버튼을 클릭해 텍스트를 변경하는 글을 올렸었는데 수정이 필요했다.

https://velog.io/@pji3504/javascript-%EB%B2%84%ED%8A%BC-%ED%85%8D%EC%8A%A4%ED%8A%B8-%EB%B0%98%EB%B3%B5-%EB%B3%80%EA%B2%BD

- 문제는 v-for로 출력한 리스트들이 모두 동일한 id 값을 가지고 있기에
적용한 코드가 가장 먼저 출력된 항목에만 작동하고있다는 것을 깨달았다..

그래서 해결방안으로 찾은 것이 *$event* 이다.

### 수정 전 소스코드
- html
```html
 <button class="btn" id="btn" @click="clickFollow">팔로우</button>
```
- javascript
```javascript
const btn = document.querySelector('btn') //id가 'btn'인 요소를 반환한다.
if(btn.innerText == 'Follow' ){ //버튼의 텍스트값 확인
  btn.innerText = 'Unfollow'  // 텍스트를 unfollow로 변경
}else{  // 반대일 경우 다시 변경
  btn.innerText = 'Follow'
}
```

### 수정 후 소스코드
- html
```html
<button class="btn"  @click="clickFollow($event)">follow
</button>   //clickFollow를 호출할때 $event를 같이 넘겨준다
```
- javascript
```javascript
if(event.target.innerText == 'follow' ){
  event.target.innerText = 'Unfollow'
  event.target.style.backgroundColor='#FFFFFF'
}else{
  event.target.innerText = 'follow'

  event.target.style.backgroundColor='#50bcdf'
}
```

#### 아래의 코드로 수정하고 나니 각각의 항목에서 javascript 코드가 문제 없이 적용되는 것을 확인할 수 있었다.


#### Event
- Event인터페이스는 Dom 내에 위치한 이벤트를 나타낸다.
#### Event.target
- Event interface의 target 속성은 event가 전달한 객체에 대한 참조이다.

참고문서 : https://developer.mozilla.org/ko/docs/Web/API/Event
