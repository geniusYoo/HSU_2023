# Swift Advanced

1. Optional
    1. 임의의 순간에 값이 정해지지 않는 경우, 이런 변수가 옵셔널 변수
        
        ```swift
        var anumber = Int("10") // 문자열 10을 정수로 변환하여 anumber에 저장
        // Int("10")은 실행하기 전에는 "10"이 정수로 변활될 수 있을지 아무도 모른다.
        // Int()함수의 리턴 타입은 Int?이다. 이것은 리턴 값은 정수이든지 아니면 nil이라는 것이다.
        // 따라서 anumber의 데이터 타입은 Int?가 된다. anumber에 커서를 놓고 option+click해 보라
        var bnumber = Int("10.0") // 어떻게 될까?
        // Int("10.0")는 "10.0"가 정수가 될수 없으므로 nil을 리턴한다. print(anumber)
        // Optional(10)를 출력한다
        print(bnumber)
        // nil을 출력한다.
        var cnumber:Int = Int("10")
        // 당연히 에러이다. 왜냐 왼쪽은 Int타입이고 오른쪽은 Int? 타입이므로. 해결책은? 오른쪽을 Int("10")!
        var dnumber:Int = Int("10.0")
        // 이것도 에러이다. 해결책은 Int("10.0")!일까? NO
        ```
        
    2. 변수/상수 선언의 3가지
        1. 일반 : 일반값을 저장할 수 있으나 절대 nil 값을 저장할 수 없음
        2. 옵셔널 : 일반값과 nil값 저장 가능
        3. 암시적 언래핑 옵셔널 : 일시적으로 nil을 가질 수 있으나 read 되기 전에 일반값이 저장되지 않으면 죽는다
        
        ```swift
        var anumber: Int = 10 // 일반
        var bnumber: Int? = 20 // 옵셔널
        var cnumber: Int! // 암시적 언랩 옵셔널 var dnumber: Int! // 암시적 언랩 옵셔널
        // anumber = cnumber // 문법에러 아님, runtime error
        // cnumber은 암시적 언랙 옵셔널로서 최최의 reading번에 반드시 일반값으로 저장되어야 함
        cnumber = 20
        anumber = cnumber // 이것은 no error, 왜냐 cnumber이 초기화 되었기 때문//anumber = bnumber dnumber = bnumber 장되기만 하면 된다. anumber = dnumber
        dnumber = nil anumber = dnumber
        // 문법에러, 해결책 강제 언랩, 옵셔널 바인딩
        // 문제없다, dnumber은 nil을 가질 수 있다. 단지 최초 reading전에 일반값이 저
        // 문제없다.
        // runtime error
        ```
        
    3. 변수/상수 reading
        1. 일반 : 항상 reading 가능
        2. 옵셔널 : 여러 방법이 있음
        3. 암시적 언래핑 옵셔널 : 이 변수에 nil이 아닌 값이 저장됨을 확신해야 함
        
        ```swift
        var aint: Int = 10 // 일반변수
        var bint: Int! = 20 // implicit unwrapped optional
        var cint: Int? = 30 // Optional
        var dint: Int? // 이것은 = nil과 같다
        
        print(aint) // 10
        print(bint) // Optional(20)
        print(cint) // Optional(20)
        print(dint) // nil
        
        aint = bint // no problems
        
        bint = cint // no problems
        aint = bint // no problems
        // bint값이 nil일 가능성이 있지만, 어째든 앞에서 Int!라고 하였으므로 reading시점에서 nil이 아닐것이라고 한 것이기에... 
        
        bint = dint // no problems
        aint = bint // 문법적으로는 문제 없음
        // bint값이 nil일 가능성이 있지만, 어째든 앞에서 Int!라고 하였으므로 reading시점에서 nil이 아닐것이라고 한 것이기에... 
        // 그러나 runtime error
        ```
        
    4. If Statements and Forced Unwrapping, 강제 언래핑
        
        ```swift
        let possibleNumber = "123"
        let convertedNumber = Int(possibleNumber)// convertedNumber의 데이터 타입은 Int?
        
        if convertedNumber != nil {
        	print("convertedNumber has an integer value of \(convertedNumber).") }
        // Prints "convertedNumber has an integer value of Optional(123)."
        
        if convertedNumber != nil {
        	print("convertedNumber has an integer value of \(convertedNumber!).") }
        // Prints "convertedNumber has an integer value of 123."
        ```
        
    5. Optional Binding
        
        ```swift
        let possibleNumber = "123"
        let convertedNumber = Int(possibleNumber)// convertedNumber의 데이터 타입은 Int?
        if let actualNumber = Int(possibleNumber) {
        	print("The string \"\(possibleNumber)\" has an integer value of \(actualNumber)") print("The string \"\(possibleNumber)\" has an integer value of \(Int(possibleNumber))")
        } else {
        	print("The string \"\(possibleNumber)\" couldn't be converted to an integer") }
        // Prints "The string "123" has an integer value of 123"
        ```
        
    6. Optional Chaining
        - 옵셔널 체이닝은 옵셔널 변수를 사용해 하위 프로퍼티, 메소드, 서브스크립트 등을 액세스할 때 옵셔널 변수가 nil인 경우 하위 것들 액세스 없이 바로 결과를 nil로 반환
        - 옵셔널 체이닝을 통해 메소드 호출도 가능하지만, 체이닝이 nil인 경우 함수 호출 자체를 X
        - 딕셔너리의 액세스는 기본적으로 옵셔널, 키 값으로 value 꺼내는 딕셔너리 리턴 타입은 무조건 옵셔널
2. 타입 캐스팅
    - 다운캐스팅, 업캐스팅이 있고 `as` 키워드 사용
    - 형 확인은 `is` 연산자
3. 에러 처리
    - `try? expression` : error의 경우 nil
    - `try! expression` : error면 프로그램이 죽음

### ch02_hw

- Delegate 적용
    
    ```swift
    var myDelegate: MyDelegate! // 디폴트가 strong이다.
    override func viewDidLoad() {
    super.viewDidLoad()
    // Do any additional setup after loading the view.
    let tapGesture = UITapGestureRecognizer(target: self, action: #selector(dismissKeyboard)) view.addGestureRecognizer(tapGesture)
    myDelegate = MyDelegate() // 일단 strong변수로 참조한다. 그래서 레퍼런스 카운트를 1로 만든다.
    fahrenheitTextField.delegate = myDelegate 
    }
    ```