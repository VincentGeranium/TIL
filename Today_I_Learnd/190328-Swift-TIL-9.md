## Today Study

---
  
#### Function(함수)  

스위프트에서 function이란 일련의 작업을 수행하는 코드 묶음을 식별할 수 있는 특정한 이름을 부여하여 사용하는 것이다
  
이 function에는 4가지 유형이 있다
- 1. Input과 Output이 모두 있는 유형 (Function)
- 2. Input이 없고 Output만 있는 유형 (Generator)
- 3. Input이 있고 Output은 없는 유형 (Consumer)
- 4. Input과 Output이 모두 없는 유형
  
Function은 기본적으로 이렇게 이루어져 있다  
  
```
func functionName(parameterList) -> ReturnType {
    statements
}
```
  
파라미터는 이렇게 정의한다

```
(name1: Type, name2: Type)
```
  
먼저 파라미터가 없는 function부터 봐보자  
  
#### Function without parameters

```
func sayHello() {
    print("Hello!!")
}

sayHello() // Hello!!
```

- 위의 예시는 input도 없고 output도 없는 유형이다  
  
```
func sayHello2() -> String {
    return "Hello!!"
}

sayHello2() // Hello!!
```
  
- 위의 예시는 input은 없고 output은 String 타입으로 return을 받는 유형이다
- output이 String 타입이므로 return을 써주고 그 return 값을 String 타입으로 넣어줘야 한다  
  
#### Function without return values  
  
이번에는 리턴 값이 없는 유형을 봐보자  
  
```
func printNumber(number: Int) -> {
    print(number)
}

printNumber(number: 1) // 1
```
  
- 위의 예시는 파라미터로 Int 타입을 받으며 리턴은 없다
- 파라미터 number로 들어온 Int 값이 출력되는 함수이다
- input 값이 있는 함수이므로 함수를 불러들일때 파라미터 값을 넣어주어야 한다
- printNumber(number: 1)
  
```
func stringNumberPrint(strNumber: String) -> Void {
    print(strNumber)
}

stringNumberPrint(strNumber: "13") // "13"
```
  
- 위의 예시는 파라미터로 String 타입을 받으며 리턴은 없다
- Void는 output이 없다, 리턴 타입이 없다는 것을 명시해주는 것이다
- input 값이 있는 함수이므로 함수를 불러들일때 파라미터 값을 넣어주어야 한다
- stringNumberPrint(strNumber: "13"), String 타입으로 input값을 받기 때문에 String 타입의 "13"을 받는 것이다  
  
```
func yourName(name: String) -> () {
    print(name)
}

yourName(name: "Jun") // "Jun"
```

- 위의 예시는 파라미터로 String 타입을 받으며 리턴은 없다
- 파라미터 name으로 String 값을 받아 출력하는 함수이다
- -> () 이렇게 명시되어 있는 것의 의미는 리턴 값이 없다는 뜻이다
  
- **return value가 없다는 것을 나타내는 것이 위에서 보듯이 여러가지이다**
- 1. -> {} 바로 statement가 쓰이는것
- 2. -> Void {} 로 Void를 명시해주는 것
- 3. -> () {} 로 ()로 리턴 값이 없다는 것을 명시해주는 것  
  
#### Function with params and return values  
  
```
func sayHello(person: String) -> String {
    let greeting = "Hello, " + person + "!"
    return greeting
}

sayHello(person: "Jun") // Hello, Jun!
```

- 이 함수는 파라미터로 String 타입을 받고 리턴 타입으로 String를 받으면서 그 함수 안에서 greeting이라는 상수를 설정하여 파라미터를 사이에 두고 값을 연산하여 리턴하는 함수이다
- 그래서 리턴 값으로 상수 greeting을 받아 output으로 Hello, Jun! 이 나오게 되는 것이다  
  
```
func oneLineHello(person: String) -> String {
    return "Hello, " + person + "!"
}

oneLineHello(person: "Jun") // Hello, Jun!
```

- 위의 함수는 따로 상수나 변수를 함수 내에서 정의하지 않고 return 값내에서 바로 연산하여 값을 리턴했다
- 위의 리턴을 받을 수 있는 이유는 연산을 해서 나온 결과값이 String이기 때문에 output 타입과 일치하여서 return value로 가능한 것이다  
  
- **Function with Multiple Parameter**  
  
```
func addNumbers(first: Int, second: Int) -> Int {
    return first + second
}

addNumbers(first: 10, second: 5) // 15
addNumbers(first: 5, second: 5) //10
```

- 위의 예시는 두개의 파라미터를 받아 리턴값으로 두 파라미터로 받아온 값을 더하기 연산하여 리턴해주는 함수이다
- 두개의 파라미터 first와 second 둘 다 Int 타입이고 리턴 타입 또한 Int 값으로 받는다
- return 에서 두 값을 더하는 연산을 하고 return value으로 두 파라미터로 받아온 값을 더하여 return 한다  
  
#### Argument Label  
  
먼저 Argument Label의 정의 형식을 보자

```
(Argument Parameter: Type)
```

이번에는 Argument Label이 있는 함수를 만들고 그 예시를 보며 이해해보자  
  
```
func exampleFunction(firstParameterName: Int, secondParameterName: Int) {
    print(firstParameterName, secondParameterName)
}

exampleFunction(firstParameterName: 3, secondParameterName: 5)
// 3 5
```

- 이 함수는 두개의 파라미터를 받고 리턴으로는 아무것도 없는 함수이다
- 두 파라미터로 받은 값을 각각 출력해주는 함수
- 함수를 불러올때 두 파라미터의 이름을 각각 넣어주고 그 안에 값을 넣어 함수를 불러와야 한다
- exampleFunction(firstParameterName: 3, secondParameterName: 5)  
  
파라미터의 이름이 너무 길기도 하고 이 함수를 사용하는 사용자의 편의를 위하여 파라미터의 값만 넣게 만들고 싶다 혹은 내부에서 사용하는 파라미터의 이름을 다른 것으로 바꾸어 사용하고 싶을때 그럴때 Argument Label을 사용하면 된다. 한번, 사용해서 만들어보자.  
  
```
func exampleArgumentLabelFunction(_ firstParameterName: Int, secondParameterName: Int) {
    print(firstParameterName, secondParameterName)
}

exampleArgumentLabelFunction(5, secondParameterName: 3)
// 5 3
```

- firstParameterName 파라미터 앞에 _ 라는 Argument Label 이 있다 _은 Argument 를 생략하고 값만 받겠다는 뜻이다. 그래서 따로 Argument Label를 쓰고 그에 할당하는 값을 넣는 형식으로 함수를 불러오는 것이 아니고 그냥 값만 넣어주었다
  
- secondParameterName의 경우 Arguement가 따로 없어서 파라미터 이름 그대로 사용하고 그에 할당 받는 값까지 써 주었다  
  
- **Specifying Argument Labels**  
  
이번에는 Argument Label을 다른 이름으로 정의하여 Parameter 이름과 다르게 사용되고 어떻게 사용되며 외부,내부에서 어떤 차이점이 있는지 봐보자  
  
```
func anotherFunction(argumentLabel parameterName: Int) {
    print(parameterName)
}

anotherFunction(argumentLabel: 10) // 10
```

- argumentLabel은 parameterName 대신 외부에서 값을 받아 내부의 parameterName으로 값을 전해주는 용도
- parameterName은 argumentLabel을 통해 값을 전달받아 내부에서 사용되는 용도  
  
- **Variadic Parameters**  
  
- 파라미터의 값을 여러개도 받을 수 있다

```
func averageOfNumber(_ numbers: Double...) -> Double {
    var total = 0.0
    for i in numbers {
        total += i
    }
    return total / Double(numbers.count)
}

averageOfNumbers(1,2,3,4,5) // 3
```
  
  
#### Nasted Function(함수 중첩)  
  
함수를 중첩하여 사용이 가능한데 함수 안에 함수를 사용할 경우 외부에는 숨기고 함수 내부에서만 사용할 함수를 중첩하여 사용하는 것이다  
  
```
func selectStep(backward: Bool, value: Int) -> Int {
    func stepGoAhead(input: Int) -> Int {
        return input + 1
    }
    
    func stepBackward(input: Int) -> Int {
        return input - 1
    }
    
    if backward {
        return stepBackward(input: value)
        } else {
        return stepGoAhead(input: value)
    }
}

var value = 5 // 5
selectStep(backward: true, value: value) // 4
selectStep(backward: false, value: value) // 6
```