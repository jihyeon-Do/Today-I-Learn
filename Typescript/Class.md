# Class 

## readonly

클래스의 속성에 readonly 키워드를 사용하면 아래와 같이 접근만 가능합니다.

```typescript
class Developer {
    readonly name:string;
    constructor(theName: string) {
        // constructor 함수에 초기값 설정 로직을 넣어줘야 한다.
        this.name = theName;
    }
}

let john = new Developer('John');
john.name = 'John'; // 에러 : name is readonly.
```
## Accessor 
getter, setter

일반적으로 객체에 접근하는 방식이 아닌 name 속성에 **제약사항**을 추가하고 싶다면

```typescript
class Developer {
    private name: string;

    get name(): string {
        return this.name;
    }

    set name(newValue: string) {
        if(newValue && newValue.length > 5) {
            throw new Error('이름이 너무 깁니다');
        }

        this.name = newValue;
    }
}
const josh = new Developer();
josh.name = 'Josh Bolton'; // 이름이 너무 깁니다 Error
josh.name = 'Josh';
```
**get만 선언하고 set을 선언하지 않은 경우에는 자동으로 readonly로 인식됩니다.**

## Abstract Class 

추상클래스는 인터페이스와 비슷한 역할을 하면서도 조금 다른 특징을 가지고 있다.
추상클래스 = 특정 클래스의 ❗️상속대상❗️이 되는 클래스

```typescript
abstract class Developer {
    abstract coding():void; // abstract기 붙으면 상속 받은 클래스에서 무조건 구현해야한다.

    drink():void {
        console.log('drink sth');
    }
}

// ✅ 상속받은 클래스
class FrontEndDeveloper extends Developer {
    // 무조건 구현
    coding():void {
        // Developer 클래스를 상속 받은 클래스에서 무조건 정의해야 하는 메서드
        console.log('develop web');
    }

    design():void {
        console.log('design web');
    }
}

const dev = new Developer(); // ❗️error: 추상클래스의 인스턴스는 만들 수 없다
const josh = new FrontEndDeveloper();
josh.coding();
josh.drink();
josh.design();
```
