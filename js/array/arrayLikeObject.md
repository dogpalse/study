# 유사 배열 객체

배열은 아니지만 배열로 처리할 수 있는 객체

## 배열이란

 1. 배열은 Array 객체
 2. 0 이상의 정수로 프로퍼티 이름 존재
 3. length 프로퍼티 존재
 4. Array.prototype이 상속되어 Array.prototype 메서드 사용 가능

## 유사 배열 객체

배열의 성질 중 2, 3번을 만족하는 객체는 배열처럼 처리
*Array.prototype 메서드 사용 불가
*for, for/in 사용 가능

> 유사 배열 객체의 예)
Arguments 객체
NodeList 객체 (getElementsByName, getElementsByTagName 메서드 반환값)

## 유사 배열 객체에서 Array.prototype 메서드 사용 방법

Function.prototype.call 메서드 사용

~~~javascript
let a = {
    0: 'A',
    1: 'B',
    2: 'C',
    length: 3
};
Array.prototype.join.call(a, "/");      // A/B/C
Array.prototype.push.call(a, "D");      // {'0': 'A', '1': 'B', '2': 'C', '3': 'D', length: 4}
~~~