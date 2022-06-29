### Promise.all()
> <span style="color: orange">특징</span>
- 주어진 Promise 중 하나라도 거부되는 경우, 첫 번째로 reject를 반환한 Promise의 내용을 반환합니다.

> <span style="color: orange">결과 값</span>
- 매개 변수로 주어진 순회 가능한 객체에 포함된 모든 값을 담은 배열

	일반 사용 예시 
```javascript
const promise1 = Promise.resolve(3);
const promise2 = 42;
const promise3 = new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'foo');
});

Promise.all([promise1, promise2, promise3]).then((values) => {
  console.log(values);
});
// expected output: Array [3, 42, "foo"]
```
	아래와 같이 여러 프로미스를 바로 넣어 사용할 수 있습니다.
```javascript
Promise.all([Promise.resolve(3), 42, new Promise((resolve, reject) => {
  setTimeout(resolve, 100, 'foo')]).then((values) => {
  console.log(values);
});
// expected output: Array [3, 42, "foo"]
```
	프로미스가 아닌 값이 들어있다면 무시하지만, 이행 시 결과 배열에는 포함되어 반환됩니다.
    
```javascript
// 매개변수 배열이 빈 것과 동일하게 취급하므로 이행함
var p = Promise.all([1,2,3]);
// 444로 이행하는 프로미스 하나만 제공한 것과 동일하게 취급하므로 이행함
var p2 = Promise.all([1,2,3, Promise.resolve(444)]);
// 555로 거부하는 프로미스 하나만 제공한 것과 동일하게 취급하므로 거부함
var p3 = Promise.all([1,2,3, Promise.reject(555)]);

// setTimeout()을 사용해 스택이 빈 후에 출력할 수 있음
setTimeout(function() {
    console.log(p);
    console.log(p2);
    console.log(p3);
});

```
	발생할 수 있는 거부를 사전에 처리하여 동작 방식을 바꿀 수 있습니다.
```javascript
var p1 = new Promise((resolve, reject) => {
  setTimeout(() => resolve('p1_지연_이행'), 1000);
});

var p2 = new Promise((resolve, reject) => {
  reject(new Error('p2_즉시_거부'));
});

Promise.all([
  p1.catch(error => { return error }),
  p2.catch(error => { return error }),
]).then(values => {
  console.log(values[0]) // "p1_지연_이행"
  console.log(values[1]) // "Error: p2_즉시_거부"
})
```
    
---

### Promise.allSettled()
> <span style="color: orange">특징</span>
- 주어진 모든 프로미스를 이행하거나 혹은 거부한 후, 각 프로미스에 대한 결과를 나타내는 객체 배열을 반환합니다.
- 각 프로미스의 실행 결과를 알고 싶을 때 사용할 수 있습니다.

> <span style="color: orange">결과 값</span>
-  Promise.all()와 같이 하나라도 reject를 반환했을 시 reject가 되는 것이 아닌,각 프로미스의 결과값을 반환합니다.


	일반 사용 예시
```javascript
Promise.allSettled([
  Promise.resolve(33),
  new Promise(resolve => setTimeout(() => resolve(66), 0)),
  99,
  Promise.reject(new Error('an error'))
])
.then(values => console.log(values));

// [
//   {status: "fulfilled", value: 33},
//   {status: "fulfilled", value: 66},
//   {status: "fulfilled", value: 99},
//   {status: "rejected",  reason: Error: an error}
// ]
```
	await 사용 예시
```javascript
const values = await Promise.allSettled([
  Promise.resolve(33),
  new Promise(resolve => setTimeout(() => resolve(66), 0)),
  99,
  Promise.reject(new Error('an error'))
])
console.log(values)

// [
//   {status: "fulfilled", value: 33},
//   {status: "fulfilled", value: 66},
//   {status: "fulfilled", value: 99},
//   {status: "rejected",  reason: Error: an error}
// ]
```

> 요약
- Promise.all()은 에러가 발생시 최초의 에러만 반환하며 Promise.allSettled()는 각각의 결과값을 따로 반환합니다.
