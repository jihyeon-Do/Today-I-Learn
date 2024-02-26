# Union Type
- 자바스크립트의 OR연산자와 같이 A이거나 B이다 라는 의미의 타입입니다.

```typescript
function test (text:string | number) {
    //...
}
```

## 장점

```typescript
// any를 사용하는 경우
function getAge(age:any) {
    age.toFixe() // 에러발생, age의 타입이 any로 추론되기 때문에 숫자 관련된 api를 작성할 때 코드가 자동 완성되지 않는다. 
    return age;
}

// 유니온 타입을 사용하는 경우
function getAge(age:number | string) {
    if(typeof age === 'number') {
        age.toFixed();
        return age;
    }

    if(typeof age === 'string') {
        return age;
    }

    return new TypeError('age must be number of string');
}
```
## Intersection Type
인터섹션 타입은 여러 타입을 모두 만족하는 하나의 타입을 의미합니다.

```typescript
interface Person {
    name:string;
    age:number;
}

interface Developer {
    name:string;
    skill:number;
}
type Capt = Person & Developer;

// Capt의 최종 타입
{
    name:string;
    age:number;
    skill:string;
}
```

## 유니온 타입을 쓸 때 주의할 점

```typescript
    interface Person {
        name: string;
        age:number;
    }

    interface Developer {
        name:string;
        skill:string;
    }

    function introduce(someone:Person | Developer) {
        someone.name; // O
        someone.age; // X
        someone.skill; // X
    }
    // 해석 : introduce를 호출하는 시점에 어느 타입이 올지 모르기 때문에 공통된 타입에만 접근할 수 있게 됩니다.
```