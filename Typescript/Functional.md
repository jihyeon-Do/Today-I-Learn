## 타입스크립트에서의 함수

- 함수의 파라미터(매개변수)타입
- 함수의 반환 타입
- 함수의 구조 타입

## 함수의 기본적인 타입 선언

```ts
function sum(a: number, b: number): number {
  return a + b;
}
// 함수의 반환 값에 타입을 정하지 않을 때는 void라도 사용
```

## 함수의 인자

타입스크립트에서는 함수의 인자를 모두 필수값으로 간주합니다.
따라서 함수의 매개변수를 설정하면 undefined나 null이라도 인자로 넘겨야하며 컴파일러에서 정의된 매개변수 값이 넘어 왔는지 확인합니다.

## REST 문법이 적용된 매개변수

```ts
// nums = [1, 2, 3, 4, 5]
function sum(a: number, ...nums: number[]): number {
  const totalOfNums = 0;
  for (let key in nums) {
    totalOfNums += nums[key];
  }

  return a + totalOfNums;
}
```

## this

타입스크립트에서 this가 가리키는 것을 명시하려면 아래와 같은 문법을 사용합니다.

```ts
function test(this: 타입) {
  // ...
}
```

EX)

```ts
interface Vue {
  el: string;
  count: number;
  init(this: Vue): () => {};
}

let vm: Vue = {
  el: "#app",
  count: 10,
  init: function (this: Vue) {
    return () => {
      return this.count;
    };
  },
};

let getCount = vm.init();
let count = getCount();
```

타입스크립트에서 자바스크립트의 this가 잘못 사용되었을 때 감지할 수 있습니다.

## 콜백에서의 this

콜백에서의 this는 일반적인 상황에서의 this와는 다르게 콜백으로 함수가 전달되었을 때의 this를 구분해줘야 합니다.
