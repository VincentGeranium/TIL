## Today Study

- **3. Inheritance(상속)**
- **Overriding**
- **Overriding Property**
- 상속된 인스턴스 또는 타입 프로퍼티를 override하여 해당 프로퍼티에 대한 사용자정의 getter, setter를 제공하거나 프로퍼티 옵저버를 추가하여 override된 프로퍼티가 기본 프로퍼티 값이 변경되는 것을 관찰할 수 있다

- **오버라이딩 프로퍼티의 getter and setter**
- **서브클래스에서는 상속된 특성이 저장 프로퍼티인지 연산 프로퍼티인지 알 수 없다**
- **서브클래스는 상속된 프로퍼티가 특정 이름과 타입을 가지고 있다는 것만 알 수 있다**
- 사용자는 항상 override하는 프로퍼티의 이름과 type을 모두 명시해야만, 컴파일러가 override한 프로퍼티가 super class의 프로퍼티의 타입과 이름이 일치하는지를 검사할 수 있다
- **서브클래스 프로퍼티 override에서 getter과 setter를 모두 제공하여 상속 된 읽기전용 프로퍼티를 읽기/쓰기 프로퍼티로 표시할 수 있다**
    - 그러나 상속된 읽기/쓰기 속성을 읽기 전용으로 표시할 수는 없다
- 프로퍼티의 override의 일부로, setter을 제공하는 경우, 해당 override에 대한 getter도 제공해야 한다.
- override된 getter내에서 상속된 프로퍼티의 값을 수정하지 않으려면 getter에서 super.exampleProperty를 반환하여, 상속된 값을 전달하면 된다
    - 참고 : exampleProperty는 override하려는 프로퍼티의 이름

- **예제를 통하여 설명**

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

- 먼저 기본 클래스를 정의
- 위의 클래스를 다른 클래스가 상속을 받는 순간 위의 클래스는 상속받은 다른 클래스의 슈퍼클래스가 되는것이다

```
class SUV: Vehicle {
    var gear: Int = 1
    
    override var descriptionAboutSpeed: String {
        return super.descriptionAboutSpeed + "in gear\(gear)"
    }
}
```

- Vehicle 클래스를 상속 받고, gear이라는 새로운 프로퍼티를 하나 추가
- override var descriptionAboutSpeed: String, descriptionAboutSpeed를 재정의 하였다
    - **재정의시 이름과 타입을 반드시 명시해야 한다**
        - 이름이 같아야하는 것은 이해가가는데 타입까지도?? 하고 생각 할 수 있지만, 타입을 명시해주지 않으면 컴파일 에러가 난다, 슈퍼클래스의 해당 프로퍼티의 타입과 일치해야 한다

- **override 부분을 자세히 뜯어보자**


```
override var descriptionAboutSpeed: String {
    return super.descriptionAboutSpeed + "in gear\(gear)"
}

```

- 안을 보니 super가 나왔다 super는 슈퍼클래스의 구현을 그대로 가져와 사용하겠다는 뜻이다
    - "in gear\(gear)" 이 부분을 추가해서 리턴하는 연산 프로퍼티이다

- **SUV 클래스의 인스턴스를 만들어서 보자**

```
let car = SUV() // SUV 클래스의 인스턴스 생성

car.vehicleCurrentSpeed = 25.0 // car의 vehicleCurrentSpeed를 25.0 으로 설정

car.gear = 3 // car의 gear를 3으로 설정

print("Car:\(car.descriptionAboutSpeed)") // Car:Your Current Speed is 25.0 km/hin gear3 출력
```

-**또 다른 인스턴스를 만들어 다른 상황을 봐보자**

```
let anotherCar: SUV = SUV() // SUV 클래스의 또 다른 인스턴스 생성

print("anotherCar:\(anotherCar.descriptionAboutSpeed)")
```

- 아무런 다른 값을 주지 않은채 위와 같이하면 어떤 결과값이 나올까?

- anotherCar:Your Current Speed is 0.0 km/h gear1 이 나온다
- 그 이유는 Vehicle 클래스의 vehicleCurrentSpeed의 기본값이 0.0 이였으며 gear1도 SUV 클래스에서 1이 기본값이였기 때문에 저런 출력값이 나온다

- **그렇다면 descriptionAbout을 override 했으니 vehicleCurrentSpeed도 해보자**
- **vehicleCurrentSpee는 Vehicle 클래스에서 저장프로퍼티였다** 이점을 기억하면서 override 해보자

```
class ExampleCar: Vehicle {
    var gear: Int = 1

    override var vehicleCurrentSpeed: Double = 2.0
}
```

- Compile Error 가 뜬다
    - Cannot override with a stored property 'vehicleCurrentSpeed'
    - 저장 프로퍼티인 'vehicleCurrentSpeed'는 overried 할 수 없다고 한다
- **왜 그럴까?? 그 이유는 "프로퍼티"는 "저장 프로퍼티"로 override 할 수 없기 때문이다**
- **그 프로퍼티가 저장이든, 연산이든 override를 저장 프로퍼티로 하려고 하면 오류이다!!**
- **그럼 저장/연산 프로퍼티를 -> 연산 프로퍼티로 override하는 것은 가능할까??**

- **예시를 들어가면서 그 답을 알아보자**

```
class ExampleCar: Vehicle {
    var gear: Int = 1
    override var vehicleCurrentSpeed: Double {
        
        get {
            return 1.0
        }
        set {
            gear = Int(super.vehicleCurrentSpeed)
        }
    }
}
```

- **이렇게 저장프로퍼티인 vehicleCurrentSpeed를 override(재정의)가 가능하다**
- 저장 프로퍼티였는데 왜 getter, setter 두가지 모두 다 구현했냐면, setter을 구현하지 않으면 에러가 나기 때문이다

- **위의 설명에서 "서프클래스 프로퍼티 override(재정의)에서 getter와 setter를 모두 제공하여 상속 된 읽기전용 프로퍼티를 읽기/쓰기 프로퍼티로 표시 할 수 있다 그러나 상속된 읽기/쓰기 속성을 읽기 전용으로 제공 할 수는 없다" 라고 했는데 이 부분이 이해가 잘 안간다**
    - 이해가 안가는 부분은 예제를 통해서 만들어가면서 이해해보자

- **먼저, 읽기전용 프로퍼티를 서브클래스에서 override하여 읽기/쓰기 프로퍼티로 표시 해보자**

```
class ExampleVehicleClass {
    
    var currentSpeed: Double = 0.0
    
    var description: String {
        return "현재 속도는 \(currentSpeed) miles per hour 입니다"
    }
    
    func soundFunction () {
        // no sound
    }
    
}
```

- **description은 연산프로퍼티긴 한데 읽기 전용이다, 이런 읽기 전용 프로퍼티를 이 ExampleVehicleClass를 상속하는 서브클래스에서는 읽기/쓰기 프로퍼티로 override(재정의) 할 수 있다**

```
class OverrideExampleClass: ExampleVehicleClass {
    
    var gear = 1
    
    var returnStr = ""
    
    override var description: String {
        get {
            return super.description + "in gear\(gear)"
        }
        set {
            returnStr = newValue
        }
    }
    
}
```

- **연산 프로퍼티이긴 하지만 읽기 전용이였던 description 프로퍼티를 서브클랴스에서 override하여 읽기/쓰기 전용으로 표기했다**

- **오버라이딩 프로퍼티 옵저버**
- 이번에는 재정의를 사용하여 프로퍼티에 옵저버를 추가하는 것에 대하여 알아보자
-  프로퍼티 override(재정의)를 사용하여 상속된 프로퍼티에 프로퍼티 옵저버를 추가할 수 있다
- **이렇게 하면 상속된 프로퍼티의 값이 변경 될 때 마다, 해당 프로퍼티가 처음 구현된 것과 상관없이 알림을 받을 수 있다**
- **하지만 상속된 "상수 저장 프로퍼티" 또는 "읽기 전용 연산 프로퍼티"에는 프로퍼티 옵저버를 추가할 수 없다
- **떄문에, override의 일부로서, willSet 또는 didSet의 구현을 제공하는 것이 적절하지 않다**
- 또한 동일한 프로퍼티에 대해 override setter와 override 프로퍼티 옵저버 둘다 제공할 수는 없다
- 프로퍼티의 값 변동을 확인하려는 경우, 해당 프로퍼티에 대한 사용자 지정 setter를 이미 제공하고 있는 경우, 사용자 지정 setter내에서 값 변경 내용을 관찰하기만 하면 된다

- 위의 설명 중 **상속된 "상수 저장 프로퍼티" 또는 "읽기 전용 연산 프로퍼티"에는 프로퍼티 옵저버를 추가할 수 없다**라고 했는데 그 이유에 대하여 알아보자
- 먼저 "상수 저장 프로퍼티"에 프로퍼티 옵저버를 추가 할 수 없는 이유는 : 프로퍼티 옵저버에는 willSet, didSet이 있는데 애초에 "상수 저장 프로퍼티"는 Set이 안된다, 왜냐하면 상수이기 때문에 변경이 안되는 것이다
- 두번째로는 "읽기 전용 연산 프로퍼티"에 프로퍼티 옵저버를 추가 할 수 없는 이유에 대하여 알아보자, 그 이유는 말그대로 "읽기 전용" 이기 때문이다 프로퍼티 옵저버에는 willSet와 didSet이 있는데 애초에 setter가 없으므로(읽기 전용이라서 setter이 없다) 안된다
    - Setter가 없음 -> willSet, didSet을 추가 할 수 없다 = Set이 안되니까

- OverrideExampleClass를 상속받아 AutoCar라는 클래스를 정의해보자
- 이 AutoCar는 자동 기어라서, 현재 속도를 기반으로 사용할 기어를 자동으로 선택하는 자동차이다

```
class AutoCar: OverrideExampleClass {
    override var currentSpeed: Double {
        didSet {
            gear = Int(currentSpeed / 10.0) + 1
        }
    }
}
```

- ExampleVehicleClass에서 currentSpeed는 저장 프로퍼티였다, 상수가 아닌 변수로 선언되었었다
- 그러므로 프로퍼티 옵저버를 추가 할 수 있는 요건이 된다
- description 프로퍼티는 연산 프로퍼티이면서 읽기 전용이므로 프로퍼티 옵저버를 추가 할 수 없다

- 그렇다면 didSet 안에 gear은 어느 클래스의 gear를 나타낼까?
- 바로 OverrideExampleClass의 gear 저장 프로퍼티를 나타낸다
- 그 gear 저장프로퍼티에 값을 연산해서 넣어준다
- didSet에는 oldValue가 안쓰이고, currentSpeed가 쓰였다

```
let automaticCar: AutoCar = AutoCar()
automaticCar.currentSpeed = 35.0
print("AutoCar: \(automaticCar.description)")
```

- AutoCar: 현재 속도는 35.0 miles per hour 입니다in gear4 라는 값이 출력된다
- 현재 속도를 지정해주면, 알아서 기어를 맞추어준다

- **덧붙이자면** 프로퍼티 옵저버는 원래 저장 또는 연산 프로퍼티로 정의되었는지 여부에 관계없이 모든 프로퍼티에 추가할 수 있다
- 그런데 위의 설명에서는 상수 저장 프로퍼티와 읽기전용 연산 프로퍼티에는 프로퍼티 옵저버를 추가할 수 없다 라고 했다
- 그 이유는 먼저 프로퍼티 옵저버는 lazy 저장 프로퍼티를 제외하고 저장 프로퍼티에만 추가가 가능하다
- 서브 클래스는 해당 프로퍼티가 저장인지 연산 프로퍼티인지 모르고 특정 이름과 타입만 알 수 있다
- 그래서 원래 프로퍼티가 저장 프로퍼티가 아니라 연산 프로퍼티로 정의 되었다고 해도 서브 클래스에서는 해당 연산 프로퍼티를 재정의해서 프로퍼티 옵저버를 추가 할 수 있는 것이다
- 반드시 읽기/쓰기 프로퍼티여야 한다 읽기전용 프로퍼티이면 에러가 난다

- **예시를 들어서 위의 설명을 이해해보자**

```
class ObserverExampleClass {
    var currentSpeed = 0.0
    
    var str = ""
    
    var description: String {
        get {
            return "currentSpeed is \(currentSpeed) miles per hour"
        }
        set {
            str = "Wow"
        }
    }
}
```

- **이런식으로 description이 읽기/쓰기 연산프로퍼티이면, 원래 연산 프로퍼티에는 프로퍼티 옵저버를 추가 할 수 없지만**

```
class SubClassObExample: ObserverExampleClass {
    override var description: String {
        didSet{
            print(oldValue)
        }
    }
}
```

- 이렇게 override 하면, description이 연산프로퍼티이더라도 프로퍼티 옵저버를 추가할 수 있게 되는것이다
