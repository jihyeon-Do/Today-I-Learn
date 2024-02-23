# 인터페이스
인터페이스는 상호 간에 정의한 약속 혹은 규칙을 의미합니다.
타입스크립트에서의 인터페이스는 다음과 같은 범주에 대해 약속을 정의할 수 있습니다.
- 객체의 스펙 (속성과 속성의 타입)
- 함수의 파라미터
- 함수의 스펙 (파라미터, 반환타입 등)
- 배열과 객체를 접근하는 방식
- 클래스 

## 옵션 속성
인터페이스 안에 있는 속성을 모두 다 사용하지 않아도 되게끔 만들어줍니다.
```typescript
interface CraftBeer {
    name:string;
    hop?:number;
}

let myBeer = {
    name:'Saporo'
}

function brewBeer (beer:CraftBeer) {
    return beer.name
}

brewBeer(myBeer);
```
### 옵션속성의 장점
- 속성을 선택적으로 적용할 수 있습니다.
- 인터페이스에 정의되이 있지 않은 속성에 대해서 인지시켜줄 수 있습니다.

```typescript
interface CraftBeer {
    name:string;
    hop?:number;
}

let myBeer = {
  name: 'Saporo'
};

function brewBeer(beer:CraftBeer) {
    console.log(beer.brewery) // Error: Property 'brewery' does not exist on type 'Beer' 
     console.log(beer.nam) // 오탈자도 알려줄 수 있다.
}
brewBeer(myBeer)
```

## 읽기 전용
읽기 전용 속성은 객체를 처음 생성할 때만 값을 할당하고 그 이후에는 변경할 수 없는 속성을 의미합니다.

배열을 선언할 때 `ReadonlyArray<T>` 타입을 사용하면 읽기 전용 배열을 생성할 수 있습니다.

```typescript
interface CraftBeer {
    readonly brand: string;
}

// 읽기 전용 배열
let arr: ReadonlyArray<number> = [1, 2, 3];
arr.splice(0,1); // error
arr.push(4); // error
arr[0] = 100; // error
```

## 객체 선언과 관련된 타입 체킹
타입스크립트는 인터페이스를 이용하여 객체를 선언할 때 좀 더 엄밀한 속성 검사를 진행합니다.
```typescript
interface CraftBeer {
    brand?:string;
}

function brewBeer(beer:CraftBeer) {
    //..
}
brewBeer({brandon:'what'}) // error
//* 오탈자 오류
```
만약 위의 상황처럼 타입추론을 무시하고 싶다면 아래와 같이 수정
```typescript
interface CraftBeer {
    brand?:string;
    [propName:string]:any;
}
```
## 함수 타입
인터페이스는 함수의 타입을 정의할 때에도 사용할 수 있습니다.
```typescript
interface login {
    //함수의 인자타입과 리턴타입을 적어준다.
    (username:string, password:string):boolean;
}

//ex
let loginUser: login = function(id, pw) {
    console.log('로그인 했습니다');
    return true;
}
```

## 클래스 타입
C#이나 자바처럼 타입스크립트에서도 클래스가 일정 조건을 만족하도록 타입규칙을 정할 수 있습니다.
class에서 interface를 상속받으려면 implements키워드 사용
```typescript
interface CraftBeer {
    beerName:string;
    nameBeer(beer:string):void;
}

class myBeer implements CraftBeer {
    beerName = 'Cass'
    nameBeer(b) {
        this.beerName = b;
    }
    constructor() {}
}

```

## 인터페이스 확장
클래스와 마찬가지로 인터페이스도 서로 간 확장이 가능합니다. (extends 키워드 사용)
```typescript
interface Person {
    name:string;
}

interface Developer extends Person {
    skill:string;
}
let fe = {} as Developer;
fe.name = 'josh';
fe.skill = 'Typescript';
```

혹은 여러 인터페이스를 상속받아서도 사용할 수 있습니다.
```typescript
interface Person {
    name:string;
}

interface Drinker extends Person {
    drink:string;
}

interface Developer extends Drinker {
    skill:string;
}
let fe = {} as Developer;
fe.name = 'josh';
fe.skill = 'Typescript';
fe.drink = 'Beer';

```

## 하이브리드 타입
인터페이스는 여러가지 타입을 조합하여 만들 수 있습니다.
```typescript
// 함수타입이면서 객체타입을 정의할 수 있는 인터페이스
interface CraftBeer {
    (beer:string):string;
    brand:string;
    brew():void;
}

function myBeer(): CraftBeer {
    let my = (function(beer:string) {}) as CraftBeer
    my.brand = 'Beer';
    my.brew = function(){};
    return my;
}

let brewedBeer = myBeer();
brewedBeer('My first beer');
brewedBeer.brand = 'pangyo craft';
brewedBeer.brew();
```