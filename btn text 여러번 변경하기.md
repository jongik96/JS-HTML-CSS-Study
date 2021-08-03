 팀플하면서 팔로우 기능을 구현한 뒤에 인스타그램처럼 하나의 버튼으로 'follow','unfollow'를 모두 표현하고 싶었다.
vue를 메인프레임워크로 사용하면서 여러 시도를 해봤는데
vue나 css로는 처음에 한 번 텍스트가 변경되면 그 다음부터는 바뀌지 않았다..
하지만 의외로 자바스크립트로 쉽게 해결이 가능했다.

### 소스코드
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
- 생각보다 간단하게 구현할 수 있었어서 허무하면서도 실제 sns서비스에서도 이런 방식을 사용할런지 싶어서 좀 찝찝했다..

