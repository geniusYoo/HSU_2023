# Swift Basic

1. 상수, 변수
    1. 상수 `let const = 42`
    2. 변수 `var v = 42`
    3. 형 변환 `String(int)`
    4. 문자열 안에 변수 값 적용 `₩()`
2. 배열, 딕셔너리
    
    ![Untitled](Swift%20Basic%204da38475653b45da9bc970e27249d904/Untitled.png)
    
    ![Untitled](Swift%20Basic%204da38475653b45da9bc970e27249d904/Untitled%201.png)
    
3. 흐름 제어
    
    ![Untitled](Swift%20Basic%204da38475653b45da9bc970e27249d904/Untitled%202.png)
    
- if문 안의 조건은 boolean 타입이어야 함 → `if score > 50 { .. }` 에러 발생
1. Switch문은 어떤 종류의 데이터든 사용해서 비교할 수 있고, break 키워드 안 써도 됨
2. for
    1. for-in
        - 각각 키/값 쌍으로 사용할 수 있는 이름들의 쌍을 이용해 딕셔너리에 있는 요소들을 반복 처리
            
            ![Untitled](Swift%20Basic%204da38475653b45da9bc970e27249d904/Untitled%203.png)
            
    2. for .. < 또는 for …
        1. `for a.. <b` : 인덱스가 a~b-1
        2. `for a...b` : 인덱스가 a~b
3. while
    - do-while 대신에 repeat-while
        
        ![Untitled](Swift%20Basic%204da38475653b45da9bc970e27249d904/Untitled%204.png)
        
4. function
    1. 튜플로 반환
        
        ![Untitled](Swift%20Basic%204da38475653b45da9bc970e27249d904/Untitled%205.png)
        
    2. 배열을 이용해 여러개의 값을 함수의 인자로 받을 수도 있음
        
        ![Untitled](Swift%20Basic%204da38475653b45da9bc970e27249d904/Untitled%206.png)
        
    3. 중첩 함수
        
        ![Untitled](Swift%20Basic%204da38475653b45da9bc970e27249d904/Untitled%207.png)
        
    4. 함수도 최상위 타입 (first class type)
        - 다른 객체들에 일반적으로 적용 가능한 연산을 모두 지원
        - 어떤 함수가 다른 함수를 반환값 형태로 반환할 수 있다는 것을 의미클로저
        
        ![Untitled](Swift%20Basic%204da38475653b45da9bc970e27249d904/Untitled%208.png)
        
5. 클로저
    - 이름 없는 함수
    
    ![스크린샷 2023-04-19 17.44.45.png](Swift%20Basic%204da38475653b45da9bc970e27249d904/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-19_17.44.45.png)
    
6. Enumerations
    - 열거형
        
        ![Untitled](Swift%20Basic%204da38475653b45da9bc970e27249d904/Untitled%209.png)
        
7. Class
    - init, deinit
        
        ![Untitled](Swift%20Basic%204da38475653b45da9bc970e27249d904/Untitled%2010.png)
        
    - override
    - getter/setter
8. Struct
    - 클래스와 구조체의 가장 중요한 차이점
        - 클래스는 코드 내에서 전달될 때 **참조 복사** 형태로 전달
        - 구조체는 **값 복사** 형태로 전달
9. Protocol : 자바의 inferface와 비슷
10. Extension : 기존의 타입들에 새로운 메소드나 속성들을 비교하기 위한 기능 추가
11. Mutating 키워드
    - 기본적으로 값 타입의 경우 (struct)는 인스턴스가 생성된 뒤, 인스턴스 메소드에서 해당 인스턴스의 속성을 변경할 수 없음. 이 때 구조체의 메소드가 구조체 내부에서 데이터를 수정할 필요가 생긴경우, Mutating 키워드를 사용하면 된다.