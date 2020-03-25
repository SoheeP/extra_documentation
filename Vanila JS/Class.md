# Class

ECMAScript 2015에 소개된 문법이며, 기존 prototype 기반의 상속보다 <u>객체를 생성하고 상속을 다루는</u> 데 있어 훨씬 더 단순하고 명확한 문법을 제공한다.

### 객체지향 프로그래밍(Object Orented Programming)

* 객체: 데이터와 기능을 논리적으로 묶어 놓은 것
* OOP는 사물에 관해 추상적으로, 구체적으로 생각할 수 있게 한다.
* 클래스(Class): 추상적이고 범용적인 것
  ex) '어떤' 자동차(객체)
* 인스턴스: 구체적이고 한정적인 것
  ex) '특정' 자동차(객체)
* 메서드(method): 기능
* 클래스 메서드: 클래스에 속하지만 특정 인스턴스에 묶이지는 않는 기능
* 생산자(constructor): 인스턴스를 처음 만들 때 실행되는 메서드. 객체 인스턴스를 초기화 한다. 클래스 안에 단 하나만이 존재할 수 있다.



### 클래스와 인스턴스 생성

```js
class Car {
    constructor(make, model){
        this.make = make;
        this.model = model;
        this.userGears = ["P", "N", "R", "D"];
        this.userGear = this.userGears[0];
    };
    shift(gear){
        if(this.userGears.indexOf(gear) < 0)
            throw new Error(`Invalid gear: ${gear}`);
        this.userGear = gear;
    }
}
```



```js
const car1 = new Car("Tesla", "Model S");
const car2 = new Car("Mazda", "3i");

console.log(car1.make, car2.make)
//"Tesla", "Mazda"

car1.shift('D')
console.log(car1.userGear)
//"D"

```

단, 위와 같이 클래스를 정의할 경우 `car1.userGear="X"` 라고 직접 수정해버릴 경우 막기 어렵다. 따라서 아래처럼 바꾸면 어느정도의 은닉화가 가능하다.(완벽하지 않음)

```js
class Car {
    constructor(make, model){
        this.make = make;
        this.model = model;
        this._userGears = ["P", "N", "R", "D"];
        this._userGear = this._userGears[0];
    };
    get userGear(){ return this._userGear; }
    set userGear(value){
        if(this._userGears.indexOf(value) < 0)
            throw new Error(`Invalid gear: ${value}`);
        this._userGear = value;
    }
    shift(gear){ this.userGear = gear; }
}
```

더 확실하게 프로퍼티를 보호해야 한다면, `WeakMap` 인스턴스를 사용할 수 있다.



### 프로토타입

* 최근 프로토타입 메서드를 `#` 으로 표시하는 표기법이 쓰인다.
  ex) `Car.prototype.shift` &rarr; `Car#shift`
* 객체 생성자인 클래스는 항상 첫글자를 대문자로 표기한다.
* 객체 인스턴스는 생성자의 `prototype` 프로퍼티를 `__proto__` 프로퍼티에 저장한다.
  &rarr; `__proto__` 프로퍼티는 자바스크립트 내부 동작 방식에 영향을 미친다. 마치 프로토타입의 링크를 저장한 것과 비슷하다고 이해해도 좋을 것 같다.
* 동적 디스패치(Dynamic dispatch) 매커니즘이 중요
  - 디스패치: 메서드 호출





출처: 러닝자바스크립트, [Class-MDN](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Classes)