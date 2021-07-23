## 1. 버블정렬 💦
- 버블정렬 (bubble sort, sinking sort)은 두 인접한 원소를 검사하여 정렬하는 방법이다.
**시간복잡도가 O(n^2)**로 상당히 느리지만 코드가 단순하기 때문에 자주 사용된다.
원소의 이동이 거품이 수면으로 올라오는 듯한 모습을 보이기 때문에 지어진 이름이다.

- **코드를 짜기는 쉽지만, 성능면에서는 좋지 않다!**
```javascript
var bubbleSort = function(array) {
  var length = array.length;
  var i, j, temp;
  for (i = 0; i < length - 1; i++) { // 순차적으로 비교하기 위한 반복문
    for (j = 0; j < length - 1 - i; j++) { // 끝까지 돌았을 때 다시 처음부터 비교하기 위한 반복문
      if (array[j] > array[j + 1]) { // 두 수를 비교하여 앞 수가 뒷 수보다 크면
        temp = array[j]; // 두 수를 서로 바꿔준다
        array[j] = array[j + 1];
        array[j + 1] = temp;
      }
    }
  }
  return array;
};
bubbleSort([5,1,7,4,6,3,2,8]); // 1,2,3,4,5,6,7,8
```

## 2. 삽입정렬
- 삽입정렬(Insertion Sort)은 왼쪽에서 오른쪽으로 가면서 각 요소들을 왼쪽 요소들과 비교하여 알맞은 자리에 삽입하는 형식의 정렬 방법이다.
- **시간복잡도**
	정렬이 하나도 안 되어있는 경우 : O(n^2)
    이미 정렬이 되어있는 경우 : O(n)
- **장점** : 메모리가 절약된다. 구현하기 쉽고 이미 정렬된 경우 정렬 유무를 **테스트하는 용도**로 사용될 수 있다.
- **단점** : 자료의 개수가 많아질수록 성능이 매우 떨어진다.
```javascript
function insertionSort (array) {
	for (let i = 1; i < array.length; i++) {
		let cur = array[i];
		let left = i - 1;
			while (left >= 0 && array[left] > cur) {
				array[left + 1] = array[left];
				array[left] = cur;
				cur = array[left];
				left--;
			}
		}
	return array;
}
```
1번째 데이터를 뽑아서 바로 앞의 0번째 데이터와 비교한 후, 0번째 데이터가 더 크면 두 값을 교환한다.
그 다음 2번째 데이터를 뽑아서 1번째 데이터와 비교한다. 1번째 데이터가 더 크면 두 값을 다시 교환.


## 3. 선택정렬
- 버블정렬이 각 회전이 끝날때마다 맨 마지막 데이터의 위치가 정해졌던 것과 반대로,
선택정렬은 n번째 회전이 끝날때마다 앞에서 n번째 데이터의 위치가 정해진다.
- 선택정렬 순서
	1. 먼저 주어진 리스트 중에 **최소값**을 찾는다.
    2. 그 값을 맨 앞에 위치한 값과 **교환**한다.
    3. 이제 맨 앞을 제외하고 다시 순회하며 최소값을 찾는다.
    4. 그 값을 맨 앞 위치 바로 다음 위치와 교체한다
    5. 1~4 반복.

- **시간복잡도**
	- 정렬이 안 되어있는 경우 : O(n^2)
   	- 이미 정렬 되어있는 경우 : O(n^2)
		- 매번 정해진 자리에 올 수 있는 최소값을 찾아야하기 때문에 최선,최악 시간복잡도가 같음

- **장점**
메모리절약, 알고리즘이 직관적이며 구현하기 쉽다.

- **단점**
최선, 최악의 경우 모두 O(n^2)의 시간이 걸리는 만큼 성능이 매우 떨어진다.

```javascript
function selectionSort (array) {
for (let i = 0; i < array.length; i++) {
let minIndex = i;
for (let j = i + 1; j < array.length; j++) {
if (array[minIndex] > array[j]) {
minIndex = j;
}
}
if (minIndex !== i) {
let swap = array[minIndex];
array[minIndex] = array[i];
array[i] = swap;
}
console.log(`${i}회전: ${array}`);
}
return array;
}
console.log(selectionSort([5, 4, 3, 2, 1]));
```

