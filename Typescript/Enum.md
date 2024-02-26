# Enum
- 특정 값들의 집합을 의미하는 자료형

## 1. 숫자형 열거
 
 * 의미있는 상수 자료를 정의할 수 있다.
 * 키를 값에 할당 순서가 없는 집합이자 자료구조이다.
 * enum 키워드 + 파스칼케이스 조합으로 생성
 * 계산된 값을 사용할 수 있다.
    - 타입스크립트가 알아서 추론

```typescript
enum Order {
    // 숫자 열거형
    First = 1,
    Second, // 2
    Third // 3
}
```

## 2. 문자형 열거

- 숫자형과는 다르게 이넘 값 전부 다 특정 문자 또는 다른 이넘 값으로 초기화 해줘야 한다.
- 자동으로 증가되지 않는다.

## 3. 혼합형 열거
- 지원하긴 하지만 굳이 사용하지 않는게 좋다.

## 4. 리버스 열거

- 숫자형 열거에서 역방향 값 찾기가 가능하다.

```typescript
enum Order {
    First = 1,
    Second = 2,
    Third = 3
}
console.log(Order)
/*
{
  "1": "First",
  "2": "Second",
  "3": "Third",
  "First": 1,
  "Second": 2,
  "Third": 3
} 
*/

console.log(Order.First) // 1

console.log(Order['1']) // First
```

## 5. const 열거형

- 일반 열거형에 비해 비교적 안전하다.
- 컴파일 후 제거되기 때문에 Javacsript 코드를 생성하지 않는다.

## 6. 열거형 활용 
이넘이 런타임 시점에서는 실제 객체지만 keyof 를 사용할 때 주의해야합니다.
일반적으로 keyof를 사용해야 되는 상황에서는 keyof typeof 를 사용하세요.

```typescript
enum Language {
    TypeScript = 'TS',
    JavaScript = 'JS',
    Java = 'JAVA',   
    Ruby = "RB",
}

type Lang = 'TS' | 'JS'
// keyof typeof
type LangCode = keyof typeof Language;
// keyof 는 자바스크립트에 존재하지 않는 연산자 입니다.
// keyof 연산자는 타입의 키 값들을 유니온 타입으로 반환해줍니다.
// keyof 연산자는 객체 타입에 사용할 수 있습니다.
function getLang(langCode:string){
    console.log(langCode)
}
```
## 7. 런타임 시점에서의 이넘
이넘은 런타임시에 실제 객체 형태로 존재합니다.
```typescript
enum E {
    X, Y, Z
}

function getX(obj:{X:number}) {
    return obj.X;
}

getX(E); // 이넘 E의 X는 숫자이기 때문에 정상 동작
// 왜냐! 값을 주지 않으면 0부터 차례로 1씩 증가하기 때문이다!
```