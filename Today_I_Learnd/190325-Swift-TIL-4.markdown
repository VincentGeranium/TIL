## Today Study

- **Equatable**
- Equal 이라는 것을 구현하려고 사용한다
    - Swift에서는 " == " 연산자
- 프로토콜이지만 별도로 구현해야 하는 메소드나 프로퍼티가 없다
- " == " 오퍼레이터 오버로드를 통해 동일한 동작이 된다

```
struct ExampleStruct1: Equatable {
    var exampleValue1: Int = 0
    var exampleValue2: Int = 0
}

func == (lhs: ExampleStruct1, rhs: ExampleStruct1) -> Bool {
    return (lhs.exampleValue1 == rhs.exampleValue1 && lhs.exampleValue2 == rhs.exampleValue2)
}

let testEquatable1 = ExampleStruct1(exampleValue1: 10, exampleValue2: 20)
let testEquatable2 = ExampleStruct1(exampleValue1: 20, exampleValue2: 40)
let testEquatable3 = ExampleStruct1(exampleValue1: 10, exampleValue2: 20)

testEquatable1 == testEquatable2 // false
testEquatable1 == testEquatable3 // true
```

- **Comparable**
- 수치 비교가 가능하게 하는 것을 구현하는 용도
- 반드시 Equtable과 함께 사용해야 한다
- 프로토콜이지만 별도로 구현해야 하는 메소드나 프로퍼티가 없다
- 오퍼레이터 오버로드를 이용해 동작
- " < " 만 구현이 되어있어도 구현하지 않은 " > " 오퍼레이터도 동작한다
    - " < " 와 " == " 오퍼레이터를 오버로드 함으로써 " > " 는 별도의 오버로드가 필요없다
- Comparable과 Equatable 프로토콜을 사용하지 않는다면 " > " 오퍼레이터도 오버로드 헤애 정상적으로 동작한다

```
struct ExampleStruct2: Equatable, Comparable {
    var value: Int = 0
}

func < (lhs: ExampleStruct2, rhs: ExampleStruct2) -> Bool {
    return lhs.value < rhs.value
}

func == (lhs: ExampleStruct2, rhs: ExampleStruct2) -> Bool {
    return lhs.value == rhs.value
}

let testComparable1 = ExampleStruct2(value: 10)
let testComparable2 = ExampleStruct2(value: 20)
let testComparable3 = ExampleStruct2(value: 10)

testComparable1 < testComparable2 // T
testComparable1 > testComparable2 // F
testComparable1 < testComparable3 // F
testComparable1 > testComparable3 // F
testComparable2 < testComparable3 // F
testComparable2 > testComparable3 // T
testComparable1 == testComparable3 // T
```