#### 팀플 중 axios 예시를 찾아보다가 fetch 구문으로 작성된 코드들을 볼 수 있었다. 뭔가 알아둬야 할 것 같아서 정리하는 글

참고사이트 : https://www.geeksforgeeks.org/difference-between-fetch-and-axios-js-for-making-http-requests/
#### 웹어플리케이션의 기본 업무 중 하나는 HTTP프로토콜을 통해 서버와 통신하는 것이다. 이 작업은 Fetch 또는 axios를 사용하여 쉽게 수행할 수 있다.
#### 사용하기 쉽기 때문에 내장 API 보다 axios를 선호하는 개발자들도 있다. 
#### Fetch API는 Axios의 주요기능을 완벽하게 재현할 수 있다.

## axios
- 브라우저에서 node.js 또는 XMLHttpRequests의 HTTP 요청을 만드는데 사용되는 JS 라이브러리이다.
- JS ES6에 기본으로 제공되는 Promise API를 지원한다.
- XSRF에 대한 클라이언트 측 보호를 활성화한다.
- 프론트엔드와 백엔드의 통신을 도와준다.
#### 코드 작성법
```javascript
axios.get('url') // url과 data, headers 등의 정보를 담아 요청
  .then((response) => {  
    // 통신에 성공했을 때 실행할 코드
  })
  .catch((error) => {
    // 실패 했을 경우 에러처리 코드
  }
```

## Fetch API
- HTTP 파이프라인의 일부(요청 및 응답)에 접근하고 조작할 수 있는 JS 인터페이스를 제공한다.
- 가져올 리소스의 URL이 필수로 있어야한다.
- 요청의 응답을 검색하는데 사용되는 promise를 반환한다.

#### 코드 작성법
```javascript
fetch('path-to-the-resource-to-be-fetched') //url 전송
  .then((response) => {
    // 통신에 성공했을 경우에 실행 할 코드
  })
  .catch((error) => {
    // 실패 했을 경우 에러처리 코드
  });
```


## Axios vs Fetch
|axios|fetch|
|------|---|
|request 객체에 url이 있다.|reqeust객체에 url이 없다.|
|쉽게 설치할 수 있는 패키지|대부분의 최신 브라우저에 내장되어있어 설치할 필요가 없다.|
|XSRF 보호기능을 내장하고 있다.| - |
|data 속성을 사용한다. | body 속성을 사용한다. |
|data에 객체가 포함되어 있다. | body 객체는 stringified를 거쳐야한다. |
|응답코드가 200일 때 정상 | 통신에 성공했을 경우 ok |
|JSON 데이터의 자동변환을 수행 | JSON데이터를 처리할 때 1번째로 요청을 하고 2번쨰로 .json() 메서드를 호출한다. |
|요청 취소가능, 응답시간 초과 설정가능 | 불가능 |
|HTTP요청을 가로챌 수 있음  | 제공하지 않음 |







