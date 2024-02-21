Array Method
===

배열은 Array.prototype 프로퍼티를 상속한 객체.  
Array.prototype에 정의된 메서드를 모든 배열에서 사용 가능

## Array.prototype 메서드

### 수정 메서드

원본 배열을 수정.

- _<span style="color:red">[ES6]</span> copyWithin(targetIndex[, startIndex[, count]])_
    - copyWithIn(targetIndex) : 모든 요소를 targetIndex에 복사
    - copyWithIn(targetIndex, startIndex) : startIndex 요소부터 targetIndex에 복사
    - copryWithIn(targetIndex, startIndex, endIndex) : startIndex ~ endIndex-1까지의 요소를 targetIndex에 복사
~~~javascript
let array = [1, 2, 3, 4, 5, 6];
console.log(array.copyWithin(1));           // [1, 1, 2, 3, 4, 5]
console.log(array.copyWithin(1, 3));        // [1, 3, 4, 5, 4, 5]
console.log(array.copyWithin(2, 3, 4));     // [1, 3, 5, 5, 4, 5]
~~~

- _<span style="color:red">[ES6]</span> fill(value[, startIndex[, endIndex]])_
    - fill(value) : 모든 요소를 value로 대체
    - fill(value, startIndex) : startIndex 요소부터 value로 대체
    - fill(value, startIndex, endIndex) : startIndex ~ endIndex-1까지 value로 대체
~~~javascript
let array = [1, 2, 3, 4, 5, 6];
consol.log(array.fill(10));                 // [10, 10, 10, 10, 10, 10]
consol.log(array.fill(10, 2));              // [1, 2, 10, 10, 10, 10]
consol.log(array.fill(10, 1, 4));           // [1, 10, 10, 10, 5, 6]
~~~

- _pop()_
배열의 마지막 요소 제거

- _push(data)_
배열 끝에 data 값을 배열 요소에 추가

- _reverse()_
배열의 요소를 역순으로 정렬

- _shift()_
배열을 첫 번째 요소를 제거

- _unshift(data1[, data2 ...])_
data를 배열의 첫 번째 요소부터 추가  
배열의 크기가 증가

- _sort([callback])_
    - sort() : 배열을 오름차순으로 정렬
    - sort(callback) : 배열을 callback의 방식으로 정렬
**sort 메서드는 요소를 문자열로 변환하여 정렬*

~~~javascript
let list = [
    { id: 1, name: 'Park' }, 
    { id: 2, name: 'Son' }, 
    { id: 3, name: 'Kim' }
];
// id 값으로 정렬
list.sort((a, b) => a.id - b.id);
// id 값을 역순으로 정렬
list.sort((a, b) => b.id - a.id);
// name 값으로 정렬
list.sort((a, b) => a.name.localeCompare(b.name));
// name 값을 역순으로 정렬
list.sort((a, b) => b.name.localeCompare(a.name));
~~~

- _splice(index, count[, data ...])_
index부터 count 갯수의 요소를 제거or 대체

### 접근자 메서드

원본 배열은 수정하지 않고 새로운 배열을 반환

- _concat(array)_
배열에 array를 연결한 새 배열을 반환

- _indexOf(data, index)_

- _lastIndexOf(data, index)_
index부터 data 값을 가진 index를 검색

- _join(string)_
요소를 string으로 연결한 문자열을 반환

- _slice(startIndex[, endIndex])_
startIndex ~ endIndex-1 까지의 요소를 제거한 새 배열을 반환

- _toLocaleString()_
해당 지역에 맞는 언어로 번역 후 문자열로 반환
- _toStirng()_
배열을 문자열로 반환

### 반복 메서드

배열을 순회하며 특정 작업 수행하거나 특정 조건을 만족하는 요소 반환.  
callback 함수 형태 => (value, index, array) => {}

- _<span style="color:red">[ES6]</span> entries()_
각 요소의 키(인덱스)와 값을 배열 형태로 값을 갖는 이터레이터를 반환

- _every(callback)_
모든 요소가 callback의 조건에 맞으면 true, 하나라도 틀리면 false

- _some(callback[, thisArg])_
모든 요소 중 callback 조건에 하나라도 맞으면 true

- _filter(callback)_
callback의 조건에 맞는 요소만 모아 새로운 배열을 반환

- _<span style="color:red">[ES6]</span> find(callback[, thisArg])_
요소 중에서 callback 조건에 맞는 첫 번째 요소를 반환

- _<span style="color:red">[ES6]</span> findIndex(callback[, thisArg])_
요소 중에서 callback 조건에 맞는 첫 번째 요소의 index 반환

- _forEach(callback[, thisArg])_
각 요소를 callback 함수의 값으로 실행

- _<span style="color:red">[ES6]</span> keys()_
배열의 각 요소의 인텍스를 값으로 가지는 이터레이터를 반환

- _map(callback[, thisArg])_
각 요소를 callback 함수의 값으로 실행하고 callback의 반환 값으로 새로운 배열을 반환  
callback 함수는 반환값 필수

- _reduce(callback[, initial])_
전체 요소의 합성 곱 처리
**합성 곱 처리 : 요소를 함수 처리 후 반환값을 다음 요소의 함수 값으로 사용*

~~~javascript
let array = [1, 3, 5, 7];
let sum = array.reduce((prev, value) => {
    return prev + value;
}, 0);
~~~

- _reduceRight(callback[, initial])_
오른쪽(끝) 요소부터 합성 곱 처리

- _<span style="color:red">[ES6]</span> values()_
각 요소를 값으로 가지는 이터레이터를 반환