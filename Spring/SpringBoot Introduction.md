# SpringBoot Introduction

1. SpringBoot
    1. Auto Configuration, 수동 설정 최소화
    2. 라이브러리간 버전 confilct 해결
    3. Embeded Server, 따로 서버를 설치 X (self-contained unit)
2. Auto Configuration 
    - 복잡한 설정 작업을 다른 프로젝트에도 똑같이 적용하려면 동일한 작업 반복 → 자동화 아이디어
    - 자동설정 + customize
        - spring-webmvc → Dispatcher Servlet Auto Configuration
        - H2, HSQL → Data Source Auto Configuration
    - 조건
        - classpath에 어떤 라이브러리가 있는지
        - 이미 사용하는 configurations
            
             ⇒ 이들을 바탕으로 **Auto Configuration**
            
        
        ![스크린샷 2023-06-06 00.35.19.png](SpringBoot%20Introduction%2087c8925631cd42b992266e74ddb4a923/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.35.19.png)
        
    1. Easy Dependency Management
        - spring-boot-starter : 자주 사용되는 라이브러리들, 버전까지 호환되는 걸로 맞춰놓음
        
        ![스크린샷 2023-06-06 00.37.09.png](SpringBoot%20Introduction%2087c8925631cd42b992266e74ddb4a923/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.37.09.png)
        
    2. Embedded Servlet Container Support
        - .jar임! → tomcat 내장되어있음
    3. SpringBoot Actuator
        - 모니터링, 트레이싱
        - 자동으로 Application에 포함되어있음.
        - Endpoints
            - /beans : 해당 Application에 포함된 모든 빈들
            - /mappings : 모든 매핑들, 예) RequestMapping, GetMapping .. etc
            - /actuator/health
            - /actuator/info