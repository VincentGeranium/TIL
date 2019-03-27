## Today Study

### View Controller Life Cycle

---

오늘은 뷰 컨트롤러에 대해 배웠다. 
다른 부분도 차근 차근 정리할꺼지만 그 중에서 가장 헷갈렸던 뷰 컨트롤러 라이프 사이클에 대해 정리해 보려고 한다.
  
자, 한번 시작해보자

---
  
### View Controller Life Cycle
  
뷰 컨트롤러의 생명주기 라는 처음보는 단어에 대한 이해부터 시작해보자.  

먼저, 앱들은 "View Controller"들로 이루어져 있다는 것을 알고 있어야 한다.
화면이 하나로 되어있는 앱들도 많지만, 보통 다른 앱들을 보면 화면이 넘어가거나 아니면 다른 화면으로
전환되는 앱들을 보았을 것이다.  

이렇게 화면이 넘어가거나 전환되는 앱들은 보통 하나 이상의 화면으로 구성되어있고, 이 각각의 뷰 컨트롤러들은 생명주기를 가지고 있다.  

생명주기?? 라고 하니까 뭔가 인간의 탄생과 죽음처럼 삶이 있는것 같아 보인다.
그러한 상상으로 이 뷰 컨트롤러 라이프 사이클을 보면 조금 쉽게 이해가 될 것이다.  

---

### UIViewController Lifecycle  
  
뷰는 아래의 그림과 같은 주기를 가지게 된다.  
  
![다운로드](https://user-images.githubusercontent.com/42841888/54982517-5649d200-4fee-11e9-9593-f3a5c72af5f8.jpeg)  
  
위의 그림의 순서대로 차근차근 알아가보자

---

### viewDidLoad

항상 프로젝트를 새로 열면 보이는 viewDidLoad() 함수, 이 함수의 기능을 알아가보자

```
import UIKit

class ViewController: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
        
    }
```

- **애플의 공식문서에서 viewDidLoad에 대해 "뷰의 컨트롤러가 메모리에 로드되고 난 후에 호출됩니다" 라고 명시되어있다.**
- 즉, 일단 View라는 것을 만들고, 메모리에 적재를 해야 접근이 가능하다는 소리이다  
  
#### viewDidLoad의 기능
  
- ViewDidLoad 메소드는 **뷰의 로딩이 완료** 되었을 때 **시스템에 의해 자동으로 호출된다**
    - **그렇기 때문에 일반적으로 리소스를 초기화하거나 초기 화면을 구성하는 용도로 주로 사용된다**
- **화면이 처음 만들어질 때 한 번만 실행되므로, 처음 한 번만 실행해야 하는 초기화 코드가 있을 경우 이 메소드 내부에 작성하면 된다**  

---

### viewWillAppear  
  
이제는 뷰가 로드 된 다음의 상황을 봐보자, 이제 뷰가 나타나 사용자의 눈에 보여야 할 것이다.  
  
- **viewWillAppear**는 뷰가 이제 나타날 거라는 **신호**를 **컨트롤러에게 알리는 역활**을 한다
- **즉, 뷰가 나타나기 바로 직전에 호출된다고 볼 수 있다.**  
  
#### viewDidLoad도 뷰가 나타나기 전에 호출, viewWillAppear도 뷰가 나타나기 전에 호출 둘의 차이점은??  
  
- 차이점 설명전에 이것부터 미리 알고 있어야 한다. 바로, **뷰의 라이프 사이클은 각각의 뷰에 다 적용된다**는 점이다.
- viewDidLoad와 viewWillAppear의 차이점은 **viewDidLoad는 딱 한번만 호출되고 그 이후에는 호출 되지 않는다는 점이다**  
  
예를들어 화면의 전환이 있는 앱을 사용했다고 한다면 처음 뷰가 로드되고 viewDidLoad가 나오고 그 이후에 viewWillAppear이 나온다  
**그런데** 그 이후에 다시 같은 화면으로 돌아간다면 viewDidLoad는 나오지 않고 viewWillAppear만 호출이 된다는 말이다.  
  
- **그래서 다른 뷰에서 갔다가 다시 돌아오는 상황에 해주고 싶은 처리는 viewWillAppear에서 처리해 주면 된다**

---

### viewDidAppear
  
- **viewDidAppear은 뷰가 나타났다는 것을 컨트롤러에게 알리는 역활을 한다**  
- **화면에 적용될 애니메이션을 그려준다**
- **viewDidAppear는 뷰가 화면에 나타난 직후에 실행된다**  
  
위에 설명한 점들 빼고는 **viewDidAppear**과 **viweWillAppear**는 거의 같다고 보면 된다.

---

### viewWillDisappear  
  
- **viewWillDisappear**는 뷰가 사라지기 **직전**에 호출되는 함수이다
- **뷰가 삭제 되려고 하고 있는 상황을 뷰 컨트롤레에게 통지한다**

---

### viewDidDisappear
  
- **viewDidDisappear은 뷰가 제거 되었음을 알려주는 것이다**

---
