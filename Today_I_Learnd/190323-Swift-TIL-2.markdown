## Today Study

- **OOP 4대 특징**

- **1. Abstraction(추상화)**

- **공통의 속성이나 기능을 묶어 이름을 붙이는 것**
- 객체지향적 관점에서 보면 Class를 정의하는 것 = 추상화
- **예를 들어** 바나나, 사과, 멜론, 망고 가 있을 때 이 바나나, 사과, 멜론, 망고를 각각의 객체라 한다, 그리고 이 객체들을 하나로 묶을때 과일이라는 추상적인 객체로 크게 정의한다고 하면 이때 과일이라고 묶는 것을 추상화라고 한다
- 대상의 불필요한 부분을 무시, 복잡성을 줄임, 목적에 집중할 수 있도록 단순화 (= 디자인 레벨)
    - 사물들 간의 공통점만 갖고, 차이점은 버리는 일반화를 통한 단순화
    - 중요부분의 강조를 위한 불필요한 세부 사항을 제거하는 단순화
- 추상화는 대상에 대한 관점과 사용 목적에 따라 달라질 수 있다

- Example

```
protocol Dog {
    var name: String { get }
    var age: Int { get }
    var weight: Double { get }
    
    func eatFood()
    func seat()
    func bark()
}

class MyDog: Dog {
    var name: String = "댕댕이"
    var age: Int = 1
    var weight: Double = 23.5
    
    func eatFood() {
        print("밥을 먹다")
    }
    
    func seat() {
        print("댕댕이 앉다")
    }
    
    func bark() {
        print("짖다")
    }
}
```

```
protocol Transportable {
    var canUseMagic: Bool { get set }
    var rangeOfTransportMagic: Double { get }
}

class Magic: Transportable {
    var canUseMagic: Bool = true
    
    private var _rangeOfTransportMagic = 150.0
    var rangeOfTransportMagic: Double {
        get {
            return _rangeOfTransportMagic
        }
    }
}

let harryPorter = Magic()
if harryPorter.canUseMagic {
    print("해리가 순간이동 마법으로 움직일 수 있는 거리는 \(harryPorter.rangeOfTransportMagic) km 입니다")
}
```

- **2. Encapsulation(캡슐화)**

- **데이터 구조와 데이터를 다루는 방법들을 결합 시켜 묶는 것을 캡슐화라고 한다**
- **예를 들어** 변수와 함수를 하나로 묶는 것을 캡슐화라고 한다
    - **객체가 맡은 역활을 수행하기 위한 하나의 목적을 하나로 묶는다고 생각하면 쉽다**
- **데이터를 절대로 외부에서 직접 접근을 하면 안되고 오로지 함수를 통해서만 접근 할 수 있도록 하는 것이 캡슐화이다**
- 캡슐화를 하면 은닉화도 자연스럽게 나타난다
- 추상화가 디자인 레벨에 해당하는 개념이라면 캡슐화는 구현 레벨에서의 개념이다
- **데이터 캡슐화(Data Encapsulation)은 연관된 상태와 행동을 하나의 단위 (객체)로 캡슐화 하는 것을 말한다**
- **정보 은닉화(Information Hiding)는 외부에 필요한 것만 알리고 불필요하거나 감출 정보는 숨기는 것을 말한다**
- 객체가 독립적으로 자신의 상태와 역활을 책임지고 수행할 수 있도록 자율성을 부여하며 접근 제한자를 이용해 데이터를 외부로 부터 보호한다
    - 그러므로서 무결성을 강화하고 변화에 유연하게 대응하게 된다, 자세히 몰라도 되는 내부 동작방법을 숨기고 사용하는 방법만을 외부로 노출하며,외부에서 요청을 전달하면 수신하는 객체는 "어떻게" 처리를 할지 결정한다, 외부에서는 그 내용을 알 필요가 없다

- Example
- 본가로 내려가게 된 광준이, 광준이가 본가로 내려갈때 서울을 출발한다는 정보 그리고 대전에 도착했다는 그 정보만 수아에게 주려고 한다. 중간 중간 쉬거나, 먹는등의 여러 다른 불필요한 정보는 수아가 원하지도 않고 알필요도 없다. 이 것을 코드로 작성해보자.

```
protocol Info {
    var location: String { get }
    func currentLocation()
    func goToDeajeon()
}

class InfoToSua: Info {

    var location: String = "서울"
    
    private func doSomething1() {
        print("휴게소에서 핫도그 하나 먹고 가자")
    }
    
    private func doSomething2() {
        print("금강 휴계소에서 소떡소떡 먹고 가자")
    }
    
    private func doSomething3() {
        print("호현이랑 대청호에서 낚시 하고 가자")
    }
    
    func currentLocation() {
        print("===")
        print("지금 여기는 \(location)이야~")
        print("===")
    }
    
    func goToDeajeon() {
        print("서울에서 출발~")
        doSomething1()
        doSomething3()
        doSomething2()
        print("대전에 도착했어~")
        location = "대전"
    }
}

let jun: InfoToSua = InfoToSua()
jun.currentLocation()
jun.goToDeajeon()
jun.currentLocation()
```

- 광준이는 무사히 대전에 도착, 하지만 수아는 광준이가 중간에 무었을 했는지 알 수 없다
    - 수아가 알 수 있는 정보는 오직 서울에서 출발했다는 것과 대전에 도착했다는 정보뿐이다
- func doSomething1,2,3를 모두 private 처리해서 은닉화 했고, 서울에서 대전까지 가는 정보들을 InfoToSua로 데이터 캡술화 시켰다

- **3. Inheritance(상속)**

- **Swift에서 Class, Structure, Enumeration 중에서 Class 만 상속이 가능하다**
    - **단 하나의 클래스만 상속 받을 수 있다**
- **상속을 통해서 클래스는 메소드, 프로퍼티 그리고 여러 특성들을 다른 클래스에서 상속 받을 수 있다**
- 상속을 통해서 클래스는 두 가지로 나뉘게 된다
    - **1. 하위 클래스 또는 자식 클래스라고 불리우는 "Subclass"**
    - **2. 슈퍼 클래스 또는 부모 클래스라고 불리우는 "Superclass"**
- 상속은 스위프트에서 클래스를 다른 타입과 차별화하는 기본 동작이다
- 클래스는 슈퍼클래스에 속한 메소드, 프로퍼티 및 하위 스크립트를 호출, 접근 할 수 있다
- 슈퍼클래스에 속한 메소드, 속성 및 하위 스크립트의 재정의(override)를 할 수 있으며, 해당 동작을 수정하거나 조정이 가능하다
    - override 정의에 일치하는 슈퍼클래스 정의가 있는지 확인하여 override가 올바른지 확인하는데 도움이 된다
- 클래스는 프로퍼티 옵저버를 상속된 프로퍼티에 추가하여 프로퍼티 값이 변경될 때 알림을 받을 수 있다
- **하나의 클래스의 특징을 다른 클래스가 물려받아 그 속성과 기능을 동일하게 사용하거나 재정의를 통해 사용하는 것**
    - 쉽게 말하면 큰 뼈대를 빌려온다는 느낌으로 받아들이면 된다
- 범용적인 클래스를 작성한 뒤 상속을 이용해 중복되는 속성과 기능을 쉽게 구현 할 수 있다
- **주요 목적으로는 재사용과 확장**
    - 상속은 수직 확장, Extension은 수평 확장
- 다이아몬드 상속 문제로 인해 언어에 따라 다중 상속을 허용하기도 하고 비허용 하기도 한다
    - **스위프트에서는 다중 상속을 비용하는 대신에 Protocol을 이용하여 다이아몬드 상속과 유사한 기능을 구현 할 수 있다**

- **기본 클래스 정의**
- **다른 클래스를 상속받지 않는 클래스를 "기본 클래스(base class)"라고 한다
- 클래스는 보편적인 기본 클래스에서 상속하지 않는다. 슈퍼클래스를 지정하지 않고 정의하는 클래스는 자동으로 기본클래스가 되어 확장(extension)이 가능하다

```
class basicClass {
    func identityOf() {
        print("아무것도 상속받지 않은 저는 기본 클래스 입니다")
    }
}

let baseClassIdentity: basicClass = basicClass()
baseClassIdentity.identityOf()
```

- 위에 나와있는 클래스는 하나의 메소드를 가지고 있는 기본 클래스이다

- 이번에는 Vehicle이라는 이름을 가진 기본 클래스를 만들어보고 부가적인 프로퍼티와 메소드들을 더해 가면서 보자

```
class Vehicle {
    
    var vehicleCurrentSpeed: Double = 0.0
    
    var descriptionAboutSpeed: String {
        return "Your Current Speed is \(vehicleCurrentSpeed) km/h"
        
    }
    
    func soundOfVehicle () {
        // no sound
    }
    
}
```

- 위의 클래스를 보면 현재 속도는 가변 저장 프로퍼티로 선언 되었고, 속도에 대한 설명은 연산 프로퍼티로 선 언되었다
- soundOfVehicle 라는 메소드도 하나 선언 되어있다
- 이 클래스의 모든 프로퍼티에는 기본값이 있어서 따로 이니셜라이저를 안만들어도 된다

```
let someVehicle: Vehicle = Vehicle()
```

- Vehicle타입의 인스턴스를 생성
    - someVehicle 이라는 Vehicle 클래스의 인스턴스
- Vehicle 클래스의 인스턴스이므로 Vehicle의 프로퍼티와 메소드에 접근이 가능해진다

```
print("탈것의 현재 속도 : \(someVehicle.descriptionAboutSpeed)")
```

- **Subclassing**
- 서브클래싱은 기존 클래스에서 새 클래스를 기초로 하는 행위이다
- 하위 클래스는 기존 클래스의 특성(characteristics)을 상속, 수정 가능 하며 또한 새 특성을 서브 클래스에 추가 가능하다
- 하위 클래스에 슈퍼 클래스로 부터 상속 받았다라는 것을 나타내려면 슈퍼클래스 이름 앞에 콜론으로 구분하고 하위 클래스 이름을 쓰면 된다

```
class ExampleSuperClass {
    // SuperClass
}


class ExampleSubClass: ExampleSuperClass {
    
}
```

- **ExampleSubClass는 하위클래스고, ExampleSuperClass는 슈퍼클래스 이다**
- 위의 예시를 보듯이 ( : )으로 하위 클래스와 슈퍼 클래스를 구분지었다
- 그럼 위에서 만든 Vehicle을 슈퍼 클래스로 하여 여러 다른 서브 클래스를 만들어보자

```
class FixedBike: Vehicle {
    var hasBasket: Bool = false
}
```

- Vehicle을 상속한 FixedBike 클래스.
- Vehicle은 슈퍼클래스가 되고 FixedBike는 하위클래스가 된다
- FixedBike 클래스는 Vehicle의 프로퍼티와 메소드들을 상속 뿐만 아니라 새로운 특성인 hasBasket이라는 저장 프로퍼티를 추가했다
- FixedBike 클래스는 vehicleCurrentSpeed와 descriptionAboutSpeed 속성과 soundOfVehicle() 메소드와 같이 Vehicle의 모든 특성을 자동으로 얻는다
- FixedBike도 모두 기본값을 주었으니 이니셜라이저는 필요 없다
- 기본적으로 새로 만드는 모든 FixedBike 인스턴스에는 Basket이 없다(false). 하지만 이것을 true로 설정할 수 도 있다

```
let someBike = FixedBike()
someBike.hasBasket // false 기본으로 지정된 값이 false
someBike.hasBasket = true // true로 값 변경 설정
someBike.hasBasket // true로 값 변경
```

- someBike는 FixedBike 클래스의 인스턴스인데 FixedBike는 Vehicle 클래스를 상속하여 someBike는 Vehicle 클래스의 특성에 모두 접근이 가능하다

```
someBike.vehicleCurrentSpeed = 10.0
print("someBike의 현재 속도는 \(someBike.vehicleCurrentSpeed) 입니다")
```

- **Overriding (재정의)**
- 서브클래스는 슈퍼클래스에서 상속 받을 인스턴스 메소드, 타입 메소드, 인스턴스 프로퍼티, 타입 프로퍼티 또는 하위 스크립트에 대한 고유한 사용자 지정 구현을 제공하는 것을 **overriding(재정의) 라고 한다.
- 위의 설명과는 다르게 상속 될 특성을 겹쳐 쓰려면 Overriding(재정의) 키워드 앞에 override 접두어를 붙인다
    - 이러면 재정의를 제공, 실수로 일치하는 정의를 제공하지 않는다는 것을 분명히 한다
    - 실수로 override하면 예기치 않은 동작이 발생할 수도 있고 override 키워드가 없는 모든 재정의는 컴파일 오류를 일으킨다
- override 키워드는 또한 컴파일러가 재정의를 위해 제공한 것과 일피하는 선언을 슈퍼클래스 또는 슈퍼클래스의 슈퍼클래스 등에 선언했는지 확인하도록 요청한다
    - 이는 재정의 정의가 올바른지 확인하는 것이다

- **슈퍼클래스 메소드, 프로퍼티, 그리고 서브스크립트로의 접근**
- 서브클래스에 대한 메소드, 프로퍼티, 서브스크립트에 대한 재정의 기능을 제공하는 경우에는, 가끔씩 재정의 일부로 기존 상위 클래스 구현을 사용하는 것이 유용하다
    - 예를들어, 기존 구현의 동작을 개선하거나 수정된 값을 기존 상속된 변수에 저장 할 수 있다
- 적절한 경우, super라는 키워드를 사용, 슈퍼클래스의 메소드, 프로퍼티, 서브스크립트에 접근한다
- 예시를 통한 설명
    - exampleMethod()라는 override(재정의)된 메소드는 override(재정의)된 메소드 구현 내에서 super.exampleMethod()를 호출하여 exampleMethod()의 슈퍼클래스 버전을 호출 할 수 있다
    - exampleProperty라는 override(재정의)된 프로퍼티는 overriding getter 또는 setter 구현내에서 exampleProperty의 슈퍼클래스 버전에 super.exampleProperty로 접근할 수 있다
    - exampleIndex에 대한 override(재정의)된 서브스크립트는 override(재정의) 서브스크립트 구현 내에서 super[exampleIndex]와 동일한 서브스크립드의 슈퍼클래서 버전에 접근 할 수 있다

- **Overriding Methods**

- Bus라는 클래스를 만들어 예를 들어가면서 설명해보자
- Bus는 Vehicle 클래스를 상속받아서 만들것이다

```
class Bus: Vehicle {

}
```

- 이제 Bu0s는 Vehicle 클래스를 상속받았다, 이제 Vehicle 클래스의 특성에 접근할 수 있다
- **Bus 클래스에서 Vehicle 클래스의 메소드였던 soundOfVehicle()을 override(재정의)해보자**

```
class Bus: Vehicle {
   override func soundOfVehicle() {
        print("빵빵!")
    }
}

let bus: Bus = Bus()
bus.soundOfVehicle() // 빵빵 이라는 것이 출력된다
```

- **overrid(재정의)를 하려면 무조건 이름이 같아야 한다**
- **그렇기 때문에 재정의를 하려면 꼭 override 키워드를 앞에 붙여야 한다**

```
class Bus: Vehicle {
    func soundOfVehicle() { //이렇게 override 키워드를 붙이지 않으면 Error이 나온다
        print("빵빵!")
    }
}
```

- Error message : Overriding declaration requires an 'overrid' keyword

- **이번에는 위에서 예시로 말했던 슈퍼클래스의 버전을 호출하는 super를 사용해보자**

- Bus 클래스에서 Vehicle 클래스에 있던 soundOfVehicle() 메소드를 override(재정의)하긴 할것인데 슈퍼클래스의 구현을 그대로 따르고 싶을때 super를 사용하면 된다
- 위의 Bus 클래스와 이름이 같으면 안되기 때문에 이번에는 Bus1로 만들어보자

```
class Bus1: Vehicle {
    override func soundOfVehicle() {
        super.soundOfVehicle()
    }
}

let bus1: Bus1 = Bus1()

bus1.soundOfVehicle()
```

- Vehicle 클래스에서 soundOfVehicle() 메소드는 아무것도 없었다 그러므로 bus1.soundOfVehicle() 을 해도 아무것도 출력되지 않는다
- 즉, Vehicle 클래스의 soundOfVehicle() 매소드의 정의를 따르겠다고 한것이기 때문에 Vehicle 클래스의 soundOfVehicle() 메소드를 호출한 것과 똑같이 된다