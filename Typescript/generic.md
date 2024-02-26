# 제네릭

- C# 및 Java와 같은 언어에서 널리 사용되는 문법
- 대규모 소프트웨어를 구축할 수 있는 가장 유연한 기능을 제공
- `<T>` 와 같은 꺽쇠 괄호를 사용한다.
- 임의의 타입을 받는다.
- 타입을 마치 함수의 파라미터처럼 사용


## 제네릭 사용
```typescript
function getInfo<타입 변수 지정>(msg:타입인자):타입반환 {
    ...
}

function getInfo<T>(msg:T):T {
    ...
}

console.log(getInfo<string>('word'));
console.log(getInfo<number[]>([1, 2, 3]))
```

## 함수 제네릭
```typescript
type InfoFunc = <T>(msg:T) => T
interface InterfaceGetInfoFunc {
    <T>(msg:T) : T;
}

function getInfo<T>(msg:T):T{
    return msg
}

const TypeAliases:InfoFunc = getInfo
const TypeInterface:InterfaceGetInfoFunc = getInfo

// 인터페이스 인자타입 강조하기
interface GenericLogTextFn<T> {
    <T>(text:T):T;
}

function logText<T>(text:T):T {
    return text;
}

let myString:GenericLogTextFn<string> = logText;

```
## 클래스 제네릭
```typescript
class GenericMath<T> {
    pi:T;
    sum:(x:T, y:T) => T
}

let math = new GenericMath<number>();
```
## 타입 좁혀보기
- extends 키워드 사용

```typescript
function test<T extends string | number> (name:T) {
    return name;
}

animal('고양이');
animal(123);

```
## 객체의 속성을 제약하는 방법

두 객체를 비교할 때도 제네릭 제약 조건을 사용할 수 있습니다.

```typescript
function getProperty<T, O extends keyof T>(obj:T, key:O) {
    return obj[key];
}

let obj = {a:1, b:2, c:3};

getProperty(obj, 'a');
getProperty(obj, 'z'); // error
```