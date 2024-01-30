# TypeAlias

## TypeAlias

- 타입에 대한 별칭을 지어주기 위해 사용한다.
- 의미없는 반복을 줄이고 타입을 명시적으로 사용하도록 돕는다.
- let, const를 선언해 변수를 초기화 하듯이 사용할 수 있다.
- 컴파일러가 따로 추론하지는 않는다.

```typescript
type test1 = 'TEST'
type test2 = 123
type Persont = {
    age:number
    name:string
    gender: 'M' | 'F'
}
```
- Union Type 
```typescript
type gender = 'Male' | 'Female'

type Person = {
    name:string
    age:number
}

type Me = {
    name: string
    genderType:gender
}

const obj : Person | Me = {
    name:'Jang',
    age:99,
    genderType:'Male'
}
```

- Intersection Type

```typescript
type GenderType = 'M' | 'F'

type Person = {
    name:string
    age:number
}

type Me = {
    name:string
    genderType:GenderType
}

const obj: Person & Me = {
    name:'Jang',
    age:12,
    genderType:'M'
}
```