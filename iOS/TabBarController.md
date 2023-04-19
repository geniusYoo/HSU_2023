# TabBarController

1. UIViewController
    1. UIWindow, UIView, UIViewController 구조
        
        ![스크린샷 2023-04-19 19.55.10.png](TabBarController%208c55caa909ed4effaae1eb3bad4ad784/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-19_19.55.10.png)
        
    2. View Status
        
        ![스크린샷 2023-04-19 19.55.40.png](TabBarController%208c55caa909ed4effaae1eb3bad4ad784/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-19_19.55.40.png)
        
    3. 지연 로딩
        - 모든 ViewController는 View를 가짐
        - ViewController가 로딩될 때, 화면을 보일 필요가 있으면 View 로딩 → 지연로딩, 전체 UIViewController 객체 중에 View가 가장 오버헤드가 크기 때문!
        - ViewController의 View 로딩 `loadView()`
    4. ViewController Lifecycle
        
        ![스크린샷 2023-04-19 19.59.54.png](TabBarController%208c55caa909ed4effaae1eb3bad4ad784/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-19_19.59.54.png)
        
        - `viewDidLoad()`는 오직 한번만 실
        - `viewWillAppear()`는 탭이 선택될 때마다 실행
2. UITabBarController
    1. 구조
        
        ![스크린샷 2023-04-19 20.00.47.png](TabBarController%208c55caa909ed4effaae1eb3bad4ad784/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-19_20.00.47.png)
        
3. UIPickerView
    1. 동작 원리
        1. UIPickerViewDataSource
            - UIPickerView에 데이터를 제공하는 원천
        2. UIPickerViewDelegate
            - UIPickerView가 스크롤될 때 필요한 데이터를 제공
        
        ![스크린샷 2023-04-19 20.03.32.png](TabBarController%208c55caa909ed4effaae1eb3bad4ad784/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-19_20.03.32.png)
        

###