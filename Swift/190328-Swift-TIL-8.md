## Today Study

---

#### 오늘은 지금까지 배웠던 내용들을 복습하는 식으로 공부할 예정이다
  
- let = 상수, 한번 설정하면 값의 변경이 불가  
  
let number: Int = 3 ->  값의 변경이 불가

- var = 변수, 설정한 값의 변경이 가능  
  
var number: Int = 3 -> number = 5 -> 값의 변경이 가능  
    
#### Type Annotation
- 변수 선언 시 사용될 자료의 타입을 명확하게 지정하는 것
  
let myName: String = "Jun" ->  **String**로 자료의 타입을 명확하게 지정
var favoriteNumber: Int = 91 -> **Int**로 자료의 타입을 명확하게 지정
  
#### Type Inference
- 변수 선언 시 초기화로 사용되는 값의 타입을 통해 변수의 타입을 추론하여 적용하는 것  
  
```
var age = 25
type(of: age) // Int.Type

let name = "Jun"
type(of: name) // String.type

var weight = 73.3
type(of: weight) // Double.type
```

#### Typralias
- 문맥상 더 적절한 이름으로 기존 타입의 이름을 참조하여 사용하고 싶은 경우 사용  

```
// typealias type name = type expression

typealias AudioSample = UInt16

var minAudioFound = AudioSample.min // 0
type(of: minAudioFound) // UInt16.Type

var minAudioFound1 = UInt16.min // 0
type(of: minAudioFound1) // UInt16.Type
```
  
#### Type Conversion (타입 변환)
  
```
let height = Int8(5) // 5
let width = 10 // 10
let area = height * width // Error: Binary operator '*' cannot be applied to operandes of type 'Int8' and 'Int'
```

- Error: 이진 연산자인 '*'의 피연산자의 타입이 Int8 과 Int에 적용될 수 없다
- height는 Int8 타입,  width는 Int타입
- 타입이 맞지 않아 연산 불가능
- 타입을 변환하여 타입을 맞추어 줘야 연산이 가능하다

```
let h = UInt8(25) // 25
let x = 10 * h  // 250
```

- 위의 예시와는 다르게 연산이 가능한 이유는 h가 UInt8로 되어 있고 x가 10 * h를 연산하면서 결과값이 타입 추론으로 인하여 x의 타입이 UInt로 되기 때문에 연산이 가능하다
- 즉, 상수 x는 연산의 결과값으로 인하여 타입이 결정  
  
```
let number = 10 // 10, Int type

let floatTypeNumber = Float(number) // 10, Float type

let integerTypeNumber = Int(floatTypeNumber) // 10,  Int type

let stringTypeNumber = String(number) // "10", String type
```

- int 타입인 number을 floatTypeNumber에서 Float(number)로 하여 Float 타입으로 형변환
- float type인 floatTypeNumber을 integerTypeNumber에서 Int(floatTypeNumber)로 하여 Int type으로 형변환 하여 저장
- Int type인 number의 값을 String(number)로 하여 String type로 형변환하여 stringTypeNumber에 저장

#### magnitude와 abs의 공통점과 차이점
- magnitude와 abs 둘다 절대값을 돌려준다는 공통점이 있다
- magnitude는 프로퍼티의 특성을 가지고 있으며 UInt 타입으로 반환하여 준다
- abs는 메서드의 특성을 가지고 있으며 Int 타입으로 반환하여 준다
- **magnitude**
    - summary : The magnitude of this value
    - declaration : var magnitude: UInt { get }
    - descussion : For any numeric value x, x.magnitude is the absoulte value of x. You can use the magnitude property in operations that are simpler to implement in terms of unsinged values, such as printing the value of an integer, which is just printing a'-' charcter in front of an absolute value
    - let x = -200 // x.magitude == 200
  
- **abs**
    - summary: Return the absolute value of the given number
    - declaration: func<T>(_ x: T) -> T where T : Comparable, T : SignedNumeric
    - descussion : The absolute value of x must be representable in the same type. in particular, the absolute value of a signed, fixed-width integer type's minimum cannot be represented
    - let x = Int8.min // x == -128
    - let y = abs(x) // Overflow error  
      
- **특별하게 UInt가 필요하지 않는 이상 Int로 사용하는것이 좋다**  
  
#### Terminology

```
let number = 123 // Int
let anotherNumber = 456 // Int
let optionalNumber = 789 // Optional<Int>.Type
```

- 단항 연산자(Unary Operator)
-number // -123  
  
- 전위 표기법(Prefix)  
-number // -123
  
- 후위 표기법(Postfix)
optionalNumber! // 789

- 이항 연산자 (Binary Operator)
number + anotherNumber // 579

- 중위 표기법 (Infix)
number + anotherNumber // 579

- **삼항 연산자(Ternary Operator)**
- 스위프트에서 삼항 연산자는 단 하나

```
number > 0 ? "positive" : "negative" // "positive"

위의 삼항 연산자를 if로 풀어 사용하면 아래와 같다

if number > 0 {
    "positive"
} else {
    "negative"
}

// "positive"
```
  
#### Assignment Operators
  
- Basic assignment operator
var valueOfNumber = 0 // 0  
    
- Addition assignment operator
valueOfNumber = valueOfNumber + 10 // 10  
  
- Subraction assignment operation
valueOfNumber = valueOfNumber - 5 // 5  
  
- Multiplication assignment operation
valueOfNumber = valueOfNumber * 2 // 10  
  
- Division assigment operator
valueOfNumber = valueOfNumber / 2 // 5
  
- Modulo assignment operator
valueOfNumber = valueOfNumber % 2 // 1  
  
- **Compound Assignment operator**

```
valueOfNumber += 10 // valueOfNumber = valueOfNumber + 10 // 11
valueOfNumber -= 5 // valueOfNumber = valueOfNumber - 5 // 6
valueOfNumber *= 2 // valueOfNumber = valueOfNumber * 2 // 12
valueOfNumber /= 2 // valueOfNumber = valueOfNumber / 2 // 6
valueOfNumber %= 2 // valueOfNumber = vlaueOfNumber % 2 // 0
```
  
- 스위프트는 : ++ 나 -- 를 support 하지 않는다  
  
- **실수에서의 나눗셈**

```
let doubleNumber1 = 123.4 // Double type // 123.4
let doubleNumber2 = 5.678 // Double type // 5.678
```
  
- 나누기  
doubleNumber1 / doubleNumber2 // 21.73300457907714  
  
- 나머지 구하기  
doubleNumber1 % doubleNumber2 // Error
    - Error : "%" is unavaliable: For floating point numbers use truncatingReminder instead
    - 실수에서는 "%"으로 나머지 값을 구 할 수 없다
  
- 실수에서 나머지 구하는 방법
doubleNumber1.trucatingRemainder(dividingBy: doubleNumber2) // 4.162000000000007  
  
- 실수에서 나머지 구하는 방법 2
doubleNumber1.reminder(dividingBy: doubleNumber2) // -1.515999999999993  
  
#### Comparison Operators

- Equal to operators  
a == b  
  
- Not Equal to operator  
a != b  
  
- Greater than operator  
a > b  
  
- Greater than or equal to operator  
a >= b  
  
- Less than operator  
a < b  
  
- Less than or equal ot operator  
a <= b
  
#### Logical Operators  
  
- Logical AND Operator

```
true && true // true
true && flase // false
false && true // false
false && false // false
```

- Logicla OR Operator

```
true || true // true
true || false // true
false || true // true
false || false // false
```

- Logical Negation Operator

```
!true // fals
!false // true
```

- Combining Logical Operators

```
let enterdDoorCode = true
let passedRetinaScan = false
let hasDoorKey = false
let knowsOverridePassword = true
```
  
- **논리연산자에서는 순서에 주의해야 한다**
  
#### Range Operators  
  
- Closed Range Operator  
0...100 // 0부터 100까지  

```
for i in 1...5 {
    print("\(i) times 5 is \(i * 5)")
}

//
1 times 5 is 5
2 times 5 is 10
3 times 5 is 15
4 times 5 is 20
5 times 5 is 25
```

- Half-Open Range Operator  
0..<100 // 0부터 99까지  
  
```
let names = ["Jun", "Sua", "SoYeon", "DaYoon"]
let count = names.count // 4
for i in 0..<count { // 0..<4 -> 0,1,2,3
    print("Person \(i+1) is called \(names[i]")
}

//
Person 1 is called Jun
Preson 2 is called Sua
Person 3 is called SoYeon
Person 4 is called DaYoon
```

- One-Sided Ranges  
1... // 1부터 ~까지  
...100 // ~부터 100까지  
..<100 // ~부터 99까지  
  
```
names[2...] // "SoYeon", "DaYoon"
names[...2] // "Jun", "Sua", "SoYeon"
names[..<2] // "Jun", "Sua"
```
  
- Range Operator reverse  
  
```
for i in (1...5).reversed() {
    print("\(i) times 5 is \(i * 5)")
}
//
5 times 5 is 25
4 times 5 is 20
3 times 5 is 15
2 times 2 is 10
1 times 1 is 5
```
