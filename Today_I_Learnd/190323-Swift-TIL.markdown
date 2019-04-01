## Today Study

- **OOP**
    - 객체 지향 프로그래밍 (Object Oriented Programming)
        - 컴퓨터 프로그래밍 패러다임 중 하나
        - 프로그래밍에서 필요한 데이터를 추상화시켜 상태와 행위를 가진 객체를 만들고 그 객체들 간의 유기적인 상호작용을 통해 로직을 구성하는 프로그래밍 방법

- **참고 : 패러다임**
    - 어떤 시대, 분야에서의 특징적인 사고 방식, 인식의 체계, 틀
    - 프로그램을 설계하는 방식에 대한 개념 / 방법론
    - 프로그래머에게 프로그래밍의 관점을 갖게 해주고 결정하는 역활

- **객체 지향 프로그래밍의 장, 단점**
    - 장점
        - 코드 재사용
            - **남이 만든 클래스를 가져와서 이용할 수 있고 상속을 통해 확장해서 사용할 수도 있다**
        - 유지보수가 쉽다
            - **절차 지향 프로그래밍에서는 코드를 수정해야할 때 일일이 찾아 수정해야하는 반면 객체 지향 프로그래밍에서는 수정해야 할 부분이 클래스 내부의 멤버 변수 혹은 메서드로 있기 때문에 해당 부분만 수정하면 된다**
        - 대형 프로젝트에 적합
            - 클래스 단위로 모듈화 시켜서 개발할 수 있으므로 대형 프로젝트처럼 여러명, 혹은 여러회사에서 개발이 필요할 시 업무 분담하기 쉽다
    - 단점
        - 처리속도가 상대적으로 느림
        - 객체가 많으면 용량이 커질 수 있다
        - 설계시 많은 시간과 노력이 필요하다

- Objective-C : OOP언어
- Swift : POP를 지향하는 멀티 패러다임 언어
- 주요 패러다임
    - POP : Protocol-Oriented Programming
    - OOP : Object-Oriented Programming
    - FP : Functional Programming

- **객체지향 프로그래밍**은 캡슐화, 다형성, 상속을 이요하여 코드 재사용을 증가시키고, 유지보수를 감소시키는 장점을 얻기 위해서 객체들을 연결시켜 프로그래밍 하는 것
- **언어 또는 기술이 추상화, 상속, 런타임 다형성을 지원하면 객체 지향이다**
    - 추상화 : 클래스나 객체를 제공
    - 상속 : 이미 존재하는 것으로부터 새로운 추상화를 만들어 내는 능력을 제공
    - 런타임 다형성 : 수행 시간에 바인딩 할 수 있는 어떠한 폼을 제공
- 단순한 데이터 처리 흐름에서 벗어나 각 역활을 지닌 객체들의 상호작용으로 동작
    - 객체 : 데이터(상태) + 메서드(행위)
- Smalltalk = 최초의 OOP 언어 , Smalltalk + C = Objective-C

```
class ExampleClass {
    var exampleVariable1 = 1
    var exampleVariable2: String = "2"
    
    func exampleFunction1(param: Int) {
        // code
    }
    
    func exampleFunction2(param: String) {
        // code
    }
}
```

- **class ExampleClass { 안에 포함된 모든 것들 }** = 클래스 (class)
- **var exampleVariable1 = 1** , **var exampleVariable2: String = "2"** = 속성, 데이터, 상태
- **func exampleFunction1(param: Int) { }** , **func exampleFunction2(param: String) { }** = 행위, 메서드, 동작

#### 클래스, 인스턴스, 객체 (Class, Instance, Object)
- Class : 소프트웨어 세계에 구현할 대상의 설계도
- Object : 소프트웨어 세계에 구현할 대상
- Instance : 설계도에 따라 소프트웨어 세계에 구현된 실체
- **오브젝트는 실체, 인스턴스는 관계에 집중한 용어**
- 오브젝트와 인스턴스를 같은 의미로 사용할때는 둘다 실체를 가리키는 의미로 사용
- 오브젝트와 인스턴스를 구분하여 사용시 강조하는 의미가 다름
    - 인스턴스는 어떤 원본으로부터 생성되었다는 의미가 내포
    - **~의 인스턴스라고 하면, 그것으로 부터 만들어진것**



#### 함수와 메소드의 차이 (Function VS Method)
- **함수(Function) :** 함수는 특정 작업을 수행하는 "코드조각".
    - **전역이던 지역이던 "독립된 기능"을 수행하는 단위**
- **함수는 메소드를 포함하는 범위**

```
func canRideRollerCoster(height: Int) -> Bool {
    if height >= 165 {
        return true
    } else {
        return false
    }
}

canRideRollerCoster(height: 160) // false
canRideRollerCoster(height: 179) // true
```

- **메소드(Method) : 클래스, 구조체, 열거형에 포함되어있는 "함수"**
    - **다른 말로는 "클래스 함수"라고도 한다**
- **다시 말해, 메소드는 클래스/구조체/열거형 내부에 작성된 것을 말한다**

```
class Human {
    func whenMoveMouth(someFood: String) -> String {
        if someFood == "Apple" {
            return "Eat the Apple"
        } else {
            return "I don't like \(someFood) !!"
        }
    }
}

var jun: Human = Human()
jun.whenMoveMouth(someFood: "Apple") // "Eat the Apple"
jun.whenMoveMouth(someFood: "Banana") // "I don't like Banana !!"

var sua = Human()
sua.whenMoveMouth(someFood: "Apple") // "Eat the Apple"
sua.whenMoveMouth(someFood: "Kiwi") // "I don't like Kiwi !!"
```

#### 클래스

- **클래스 기본 구조**

```
 class ClassName: SuperClassName, ProtocolName... {
 PropertyList
 MethodList
 }



let instanceName = ClassName()
instanceName.propertyName
instanceName.functionName()
```

```
class Phone {
    var color = "white"
    var price = 1_200_000
    var madeBy = "Apple"
    
    func call() {
        print("전화 걸기")
    }
    func message() {
        print("문자 보내기")
    }
    func memo() {
        print("메모장 기능")
    }
}

let myPhone: Phone = Phone()
myPhone.color
myPhone.price
myPhone.madeBy
myPhone.call()
myPhone.message()
myPhone.memo()
```

#### 클래스의 초기화 메소드
- **초기화(init)메서드가 필요한 경우 -> 저장 프로퍼티 중 하나 이상의 초기값이 미설정**
- **초기화(init)메서드가 불필요한 경우 -> 모든 저장 프로퍼티에 초기값이 설정**

- **초기화가 불필요**

```
class Tabaco {
    let malboro = "Malboro red"
    let cigar = "Cigar No.1"
    
    func fireOnTheTabaco() {
        print("담배에 불을 붙였습니다")
    }
}

let getTabaco = Tabaco()
getTabaco.fireOnTheTabaco()
```

- **초기화가 필요**
- **파라미터가 없는 경우 초기화**

```
class AnotherTabaco {
    let tabacoName: String
    let spendMoney: Int
    
    init() {
        tabacoName = "Cigar No.1"
        spendMoney = 4500
    }
    
    func fireOnTheTabaco() {
        print("담배에 불을 붙였습니다")
    }
}

let getTabaco2 = AnotherTabaco()
getTabaco2.tabacoName
getTabaco2.spendMoney
```

- **파라미터를 통해 설정하는 경우**

```
class GetRamen {
    let nameOfRamen: String
    let priceOfRamen: Int
    
    init(nameOfRamen: String) {
        self.nameOfRamen = nameOfRamen
        priceOfRamen = 1200
    }
    init(nameOfRamen: String, priceOfRamen: Int) {
        self.nameOfRamen = nameOfRamen
        self.priceOfRamen = priceOfRamen
    }
    
    func haveNoMoney() {
        print("돈이 없어 \(nameOfRamen) 구매 불가")
    }
}

var eatRamen = GetRamen(nameOfRamen: "삼양라면")
eatRamen.nameOfRamen
eatRamen.priceOfRamen
eatRamen.haveNoMoney()

var anotherRamen = GetRamen(nameOfRamen: "보급용 육계장 라면" , priceOfRamen: 1000)
anotherRamen.nameOfRamen
anotherRamen.priceOfRamen
anotherRamen.haveNoMoney()
```
