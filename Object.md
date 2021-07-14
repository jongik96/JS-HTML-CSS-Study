## ⛹️‍♂️ 객체의 생성

```javascript
var grades = ('egoing' : 10, 'k8805': 6, 'sorialgi': 80};
```
위 예제에서 egoing은 **key**가 되고, 10은 **value**가 된다. 
아래는 객체를 만드는 다른 방법들이다.
```javascript
var grades = {};
grades['egoing'] = 10;
grades['k8805'] = 6;
grades['sorialgi'] = 80;
//
var grades = new Object();
grades['egoing']=10;
grades['k8805']=6;
grades['sorialgi']=80;
```
### ⛹️‍♂️ 객체에서 필요한 값 가져오기
```javascript
var grades = {'egoing': 10, 'k8805': 6, 'sorialgi': 80};
alert(grades['sorialgi']); // grades객체의 sorialgi에 해당하는 값인 80이 출력된다.
```

- for문을 활용한 값 가져오기
```javascript
var grades = {'egoing': 10, 'k8805': 6, 'sorialgi': 80};
for(key in grades) {
    alert("key : "+key+" value : "+grades[key]);
}
```
- for문은 in 뒤에 따라오는 배열의 key 값을 in 앞의 변수 name에 담아서 반복문을 실행한다.


### ⛹️‍♂️ 객체에는 객체를 담을수도 있고, 함수도 담을 수 있다.
```javascript
var grades = {
    'list': {'egoing': 10, 'k8805': 6, 'sorialgi': 80},
    'show' : function(){
        for(var name in this.list){
            document.write(name+':'+this.list[name]+"<br />");
        }
    }
};
grades.show();
```

<p style="color:red"> 생활코딩 참고하였습니다.<br>https://opentutorials.org/course/743/6491</P>
