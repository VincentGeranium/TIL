## Today Study

### Closure

#### 클로저 2번째 이야기

---

```
앞의 클로저 1편에 이어 2번째 이야기를 시작합니다
앞의 Closure (1)을 보고 오시지 않은 분은 보고 오시는 것을 추천드립니다
```
---

- **클로저는 사용자의 코드 안에서 전달되어 사용할 수 있는 기능이다**
- **클로저는 위의 설명된 기능을 포함하는 독립적인 블럭이다**
- **스위프트의 클로저는 다른 언어의 람다와 유사하다**
- 이해하기는 어렵겠지만 클로저는 자신이 정의된 context로부터 임의의 상수와 변수에 참조(reference)를 획득하고 저장할 수 있다
    - 이는 상수와 변수를 제약하는 특징이다
    - 이 특징으로 인해 "클로저"라는 이름이 유래되었다고 한다
- 스위프트는 획득한 모든 메모리 관리를 다룬다
- **클로저는 세가지 중 하나의 형태를 취한다**
- 1. 전역 함수의 이름은 있지만 아무런 값을 가지지 않는 클로저
- 2. 중첩 함수의 이름이 있고, 내부 함수에서 값을 획득할 수 있는 클로저
- 3. 클로저 표현식으로 둘러싸고 있는 context에서 값을 획득하는 가벼운 문법으로 작성된 이름 없는 클로저
- **스위프트 클로저 표현식은 일반적인 경우에 깨끗하고, 명확한 스타일로 최적화되어 간략하고, 깔끔한 문법을 가지고 있으며 이러한 최적화하는 다음을 포함한다**
- 1. Context로부터 Parameter와 Return value type를 유추한다
- 2. 단일 표현식 클로저로부터 명확한 반환
- 3. 축약 인자 이름
- 4. 후행 클로저 문법

---

#### 클로저 표현식(Closure Expressions)

- 중첩 함수는 더 큰 함수의 일부로서 독립적인 코드 블럭을 정의하거나 명명하는 편리한 방법이다
- 그러나 때때로 완전한 선언과 이름 없는 더 함축된 버전의 함수 같은 구조가 유용할 때가 있다
- **이것은 다른 함수들이 하나 이상의 인자로 받는 함수로 작업할 때 특히 더 그러하다**
- 클로저 표현식은 간략하게 나타내는 문법에 초점을 맞추어 작성하며, 명확성이나 의도를 잃지 않는 축약된 형태로 문법의 최적화를 제공한다.

---

#### 기본 클로저(Basic Closure)

```
func testFunction() {
    print("Function !!")
}
testFunction() // Function !!

- 위의 Function을 축약해보자

({
    print("Function !!")
})() // Function !!

- 클로저는 함수안에도 사용이 가능하다

func exampleFunction() {
    print("이것은 그냥 함수")
    ({
        print("그냥 함수 안에 사용된 클로저")
    })()
}

exampleFunction() // 이것은 그냥 함수 // 그냥 함수 안에 사용된 클로저
```

- 위에서 예시를 보면 알듯이 클로저는 input output이 없다
- 클로저는 변수에 담아 사용도 가능하다

```
let closure = {
    print("변수에 담겨 사용되는 클로저")
    }

closure() // 변수에 담겨 사용되는 클로저
```

- 클로저 뿐만 아니라 함수도 변수에 담겨 사용이 가능하다

```
var functionTest =  testFunction
functionTest() // Function !!
```

- 이렇게 함수를 담았던 변수 functionTest의 값을 클로저를 담았던 상수 closure으로 바꾸었다

```
functionTest = closure
functionTest()
```

- **클로저의 표현식은 다음과 같다**

```
{(Parameter) -> return type in
    statements
}
```

- 여러가지 클로저를 만들어보자.

- 기본 함수 형태 정의

```
func hello(_ param: String) -> String {
    return param + "!!"
}

print(hello("function")) // function !!

- Type Annotation을 이용한 Closure

let hello: (String) -> String = { param in
    return param + "!!"
}

hello("Closure") // Closure!!
```

- 위의 예제는 ( = )을 기준으로 나뉘어져 있다
- **{ }의 역활은 함수의 역활을 한다 라고 나타내는 것과 같다**
- **{ } 안에 있는 in을 기준으로 앞에는 parameter가 쓰이고 뒤에는 실행 코드가 쓰인다**

- Type Inference(타입 추론)을 이용한 Closure

```
let hello2 = {(param: String) -> String in
    return param + "!!"
}

hello2("Closure") //Closure!!
```

- 위의 예시는 상수 hello2를 정의하고 Closure 표현식으로 사용하여 상수 hello2에 대입하였다
- 그러므로써 컴파일러는 let hello2를 클로저로 판단한다

```
let hello3 = {param in
    return param + "!!"
}

hello3("closure") // closure!!
```

- **위의 예시는 인풋과 아웃풋이 추론이 가능해야 클로저로서 성립하여 에러가 안난다**
- 이 코드는 in 뒤에 나오는 실행코드에서 보면 return param + "!!"인데 "!!"가 String 처리 되어 param과 더해진다
- 컴파일러는 param과 "!!" String타입이 결합되는 연산을 보고 param도 String 으로 추론한다.

- 이번에는 문자열을 입력받으면 그 문자열의 개수를 반환하는 클로저를 구현해보자.

```
let stringCount = {(param: String) -> Int in
    return param.count
}

stringCount("Swift") // 5
```

- 위의 클로저는 Type Inference(타입 추론)을 이용하여 만든 클로저다
- input과 output을 컴파일러가 스스로 추론할 수 없어서 input type과 output type를 명시해주었다.

- 숫자 하나를 입력받은 뒤 1을 더한 값을 반환하는 틀로저를 구현해보자.

```
let countUp = {param in
    return param + 1
}

countUp(8) // 9
```

- **문법 최적화(Syntax Optimization)**

- 함수의 인자로, 입력된 문자열의 개수를 반환하는 클로저를 전달하는 예시를 보자
- 예시의 함수가 밑으로 갈수록 최적화 되어가는 모습을 볼 수 있을 것이다

```
func countString(param: (String) -> Int) {
    param("Swift")
}

countString(param: { (str: String) -> Int in
    return str.count
})

countString(param: { (str: String) in
    return str.count
})

countString(param: { str in
    return str.count
})

countString(param: {
    return $0.count // 받아오는 파라미터가 같으면 $0으로 바꿔 줄 수 있으며 파라미터가 2개이면 $0, $1 식으로 늘려나간다
})

countString(param: {
    $0.count // return 될 값이 하나뿐이므로 return도 없앨 수 있다
})

countString() {
    $0.count
}

countString{ $0.count }
```

- **클로저의 장점은 더 있을 수 있지만 다음 세가지로 축약 해본다**
- 1.문법 간소화와 가독성
- 2. 지연 생성
- 3. 주변 context의 값을 캡쳐하여 수행이 가능