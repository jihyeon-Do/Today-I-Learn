타입스크립트 기본 타입

- Boolean
- Number
- String
- Object
- Array
- Tuple
- Enum
- any
- void
- null
- undefined
- never

## String

```ts
let str: string = "hi";
```

## Number

```ts
let num: number = 10;
```

## Boolean

```ts
let isLoggedIn: boolean = false;
```

## Array

```ts
// 방법1
let arr: number[] = [1, 2, 3];

//방법2
let arr2: Array<number> = [1, 2, 3];
```

## Tuple

```ts
let arr: [string, number] = ["hi", 10];
```

## Enum

이넘은 특정 값(상수)들의 집합을 의미

```ts
enum Avengers {
  Capt,
  IronMan,
  Thor,
}
let hero: Avengers = Avengers.Capt;
```

이넘은 인덱스 번호로도 접근할 수 있다.

```ts
enum Avengers {
  Capt,
  IronMan,
  Thor,
}
let hero: Avengers = Avengers[0];
```

이넘의 인덱스를 사용자 편의로 변경하여 사용가능

```ts
enum Avengers {
  Capt = 2,
  IronMan,
  Thor,
}
let hero: Avengers = Avengers[2]; // Capt
let hero: Avengers = Avengers[4]; // Thor
```

## Any

알지 못하는 타입을 표현할 때 사용.
사용자로부터 받은 데이터나, 서드 파티 라이브러리 같은 동적인 컨텐츠에서 받는 값을 표현할 때 사용
타입 검사를 하지 않고, 컴파일 시간에 검사를 통과하길 원할때 사용

```ts
let notSure: any = 4;
notSure = "maybe a string instead";
notSure = false;
```

object가 비슷한 역할을 할 수 있을 것 같다고 생각할 수 있다. 그런데 object로 선언된 변수들은 오직 어떤 값이든 그 변수에 할당할 수 있게 해주지만 실제로 메서드가 존재하더라고 임의로 호출할 수는 없다.

```ts
let notSure: any = 4;
notSure.ifItExists(); // 성공, 런타임엔 존재
notSure.toFixed(); // 성공, 하지만 컴파일러는 검사하지 않음

let prettySure: Object = 4;
prettySure.toFixed(); // 오류 : toFixed는 '0bject'에 존재하지 않습니다
```

## Void

`void`는 어떤 타입도 존재할 수 없음을 나타낸다.
void <=> any
보통 함수에서 반환값이 없을 때 반환 타입을 표현하기 위해 쓰인다.

```ts
function test(): void {
  console.log("test");
}
```

변수에 타입선언으로는 유용하지 않다.
왜냐하면 그 변수에는 null 또는 undefined만 할당할 수 있기 때문이다.

```ts
let unusable: void = undefined;
unusable = null; // 성공 `--strictNullChecks` 을 사용하지 않을때만
```

## Null and Undefined

undefined와 null은 둘다 각각 자신의 타입 이름으로 그대로 사용합니다.
void 처럼 그 자체로 유용한 경우는 거의 없습니다.

```ts
let u: undefined = undefined;
let n: null = null;
```

null과 undefined는 다른 모든 타입의 하위 타입입니다.
이건 null과 undefined를 number와 같은 타입에 할당할 수 있다는 것을 의미합니다.

`--strictNullChecks`를 사용하면 null과 undefined는 오직 any와 각자 타입에만 할당 가능합니다. 이건 많은 에러를 방지할 수 있습니다.

## Never

절대로 발생할 수 없는 타입
예를들면, 함수 표현식이나 화살표 함수 표현식에서 항상 오류를 발생시키거나 절대 반환하지 않는 반환 타입으로 쓰입니다.
변수 또한 타입가드에 의해 아무 타입도 얻지 못하게 좁혀지면 never타입을 얻게 될 수 있습니다.

never => 모든 타입에 할당 가능한 하위 타입. 하지만 어떤 타입도 never에 할당할 수 있거나, 하위타입이 아니다. 심지어 any도 never에 할당할 수 없다.

```ts
// never를 반환하는 함수는 함수의 마지막에 도달할 수 없다.
function error(message:string):never {
    throw new Error(message);
}

// 반환타입이 never로 추론된다.
function fail() {
    return error('something');
}

// never를 반환하는 함수는 함수의 마지막에 도달할 수 없다.
function infiniteLoop(): never {
    while (true) {
        ...
    }
}
```

## Object

object 는 원시타입이 아닌 타입을 나타낸다. 예를 들어 number, string, boolean, bigint, symbol, null 또는 undefined가 아닌 나머지를 뜻한다.

object 타입을 쓰면, Object.create 같은 API가 더 잘 나타난다.

```ts
declare function create(o: object | null): void;

// 성공
create({ prop: 0 });
create(null);

// 실패
create(42);
create("string");
create(false);
create(undefined);
```

## Type assertions

타입단언.
개발자가 컴파일러에게 타입을 단언.

다른 특별한 검사를 하거나 데이터를 재구성하지는 않는다.
이는 런타임에 영향을 미치지 않으며 온전히 컴파일러만 이를 사용한다. 개발자가 필요한 어떤 특정 검사를 수행했다고 인지한다.

2가지 형태

1. angle-braket

```ts
let someValue: any = "test";
let strLength: number = (<string>someValue).length;
```

2.as

```ts
let someVlaue: any = "test";
let strLength: number = (someValue as string).length;
```

**typescript를 JSX와 함께 사용할 때는, as 스타일의 단언만 허용**
