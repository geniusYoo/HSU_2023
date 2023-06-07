# Logging with SLF4J, Logback

1. Logging vs Debugging
    - 장점
        - 로깅은 정확한 context를 제공
        - 사용자의 개입 필요 X
        - 기록을 저장
        - 쉽고 간단함
    - 단점
        - 속도 저하 가능성. 파일에 쓸 때 디스크를 접근하니까
        - 정신 사나움
        - 설정하는 것을 학습해야 함
2. Logging vs Plain Output
    - 그냥 System.out.println() 하면 되는거 아냐?
    - 이러한 장점들이 ..
        - message의 우선순위를 설정 간ㅇ
        - 전부, 일부의 로그를 출력할 수 있음
3. Logging Frameworks
    - java.util.logging
    - Log4J : 로그의 표준
    - Logback : Log4J 개선 버전
    - SLF4J : Simple Logging Facade For Java, Facade 역할로 Log4Jsk Logback으로 forwarding
4. Facade Pattern
    - 적절한 subsystem으로 forwarding
    - client는 subsystem에 어떤 것이 있는 지 알 필요 X → facade만 접근하면 OK
    
    ![스크린샷 2023-06-06 00.06.15.png](Logging%20with%20SLF4J,%20Logback%201d7a52d07a134fbc9aa23bfe91c56ac8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.06.15.png)
    
5. SLF4J
    - Simple Logging Facade for Java
    - SLF4J가 있어도 실제 역할을 수행하는 것이 있으면 SLF4J 동작 불가! → no-binding
    
    ![“Hello World” Using SLF4J](Logging%20with%20SLF4J,%20Logback%201d7a52d07a134fbc9aa23bfe91c56ac8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.08.53.png)
    
    “Hello World” Using SLF4J
    
    ![SLF4J binding with logging framework](Logging%20with%20SLF4J,%20Logback%201d7a52d07a134fbc9aa23bfe91c56ac8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.09.51.png)
    
    SLF4J binding with logging framework
    
    - SLF4J를 사용하면, logging framework 바꿔치기하기 매우 간단
    - SLF4J는 당연히 있는 거고, 구현체로 Log4J, Logback 둘다 넣어놓으면 바인딩 오류. “**one and only one**” → 어떤 걸 바인딩할 지 모르니까 ,,,
    
    ![SLF4J binding with Logback](Logging%20with%20SLF4J,%20Logback%201d7a52d07a134fbc9aa23bfe91c56ac8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.12.35.png)
    
    SLF4J binding with Logback
    
6. Consolidate logging via SLF4J
    - SLF4J로 로깅 통합
    - hibernate, spring 등 다른 프레임워크들이 출력하는 로그도 보고 싶어
    
    ![Bridging Legacy API](Logging%20with%20SLF4J,%20Logback%201d7a52d07a134fbc9aa23bfe91c56ac8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.14.33.png)
    
    Bridging Legacy API
    
7. Logback
    - **Printing Methods ****
        
        ![스크린샷 2023-06-06 00.16.23.png](Logging%20with%20SLF4J,%20Logback%201d7a52d07a134fbc9aa23bfe91c56ac8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.16.23.png)
        
    - 매개변수가 있는 로깅
        
        ![스크린샷 2023-06-06 00.17.32.png](Logging%20with%20SLF4J,%20Logback%201d7a52d07a134fbc9aa23bfe91c56ac8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.17.32.png)
        
        ![스크린샷 2023-06-06 00.17.41.png](Logging%20with%20SLF4J,%20Logback%201d7a52d07a134fbc9aa23bfe91c56ac8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.17.41.png)
        
    - Logback Architecture
        - Modules
            - Core Module : 2개의 모듈의 기반 `Appender` `Layout`
            - Classic Module : Core Module 상속받음, Log4J의 개선 버전, 기본적으로 SLF4J API implement `Logger`
            - Access Module : HTTP-access log를 제공하는 서블릿 컨테이너들 통합
    - Logger (logging level)
        - Logger는 레벨을 가지는데, 지정해주지 않으면 가장 가까운 부모로부터 상속받음. (Level Inheritence)
        
        ![스크린샷 2023-06-06 00.23.53.png](Logging%20with%20SLF4J,%20Logback%201d7a52d07a134fbc9aa23bfe91c56ac8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.23.53.png)
        
        ![스크린샷 2023-06-06 00.24.08.png](Logging%20with%20SLF4J,%20Logback%201d7a52d07a134fbc9aa23bfe91c56ac8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.24.08.png)
        
        ![스크린샷 2023-06-06 00.24.18.png](Logging%20with%20SLF4J,%20Logback%201d7a52d07a134fbc9aa23bfe91c56ac8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.24.18.png)
        
        ![스크린샷 2023-06-06 00.25.32.png](Logging%20with%20SLF4J,%20Logback%201d7a52d07a134fbc9aa23bfe91c56ac8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.25.32.png)
        
    - Appenders
        - 로그를 어디에 출력? : console, files, socket servers, databases ..
        - Logback에서 로그 이벤트를 받아 처리하는 역할
        - 로그 이벤트를 특정한 대상으로 전달하거나 저장하는 방법을 결정. 예) 파일에 로그를 저장하거나 콘솔에 로그를 출력