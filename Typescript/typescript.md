# TypeScript

타입스크립트는 자바스크립트에 타입을 부여한 언어.
타입스크립트는 브라우저에서 실행하려면 파일을 한번 변환해주어야 한다. => **컴파일**

## 타입스크립트를 써야하는 이유

- 에러의 사전 방지
- 코드 가이드 및 자동 완성 (개발 생산성 향상)

### 에러의 사전 방지

타입스크립트는 에러를 사전에 미리 예방할 수 있다.

javascript

```js
function sum(a, b) {
  return a + b;
}

sum(10, 20); // 30
sum("10", "20"); // '1020'
```

typescript

```ts
function sum(a: number, b: number) {
  return a + b;
}

sum("10", "20"); // Error: '10'은 number에 할당될 수 없습니다.
```

타입스크립트는 파라미터에 number타입을 지정해줬기 때문에 문자열로 인자를 넘길시, 에러가 발생한다.

### 코드 자동 완성과 가이드

타입스크립트는 코드를 작성할 때 개발 툴의 기능을 최대로 활용할 수 있다.

javascript

```js
function sum(a, b) {
  return a + b;
}
var total = sum(10, 20);
total.toLocaleString();
```

`toLocaleString()` 이라는 api를 사용할 때 `total` 이라는 변수의 타입이 코드를 작성하는 시점에서 number 라는것을 인지하지 못한다. 만약 오탈자가 생겨도 js파일을 브라우저에서 실행했을 때만 오류를 확인할 수 있다.

typescript

```ts
function sum(a: number, b: number): number {
  return a + b;
}
var total = sum(10, 20);
total.toLocaleString();
```

변수 `total`에 대한 타입이 지정되어 있기 때문에 api를 미리보기로 띄워준다던가 등 빠르고 정확하게 작성할 수 있다.
