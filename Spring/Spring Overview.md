# Spring Overview

1. SW 품질 
    - 기능 품질 : 고객의 니즈 충족
    - 구조 품질 : 유지보스, 잘 짜여진 코드, 재사용, 상속
    - **Framework는 구조 품질을 보장, SW 구조 그리고 기반되는 클래스를 제공**
2. 프레임워크의 중요성 
    - 프레임워크는 어플리케이션 구조 및 코드의 상당 부분을 제공, 개발자는 핵심 로직에 집중 가능
    - 높은 생산성과 코드 품질을 보장
3. 라이브러리 vs 프레임워크
    - 중요한 차이점은 **“Inversion of Control”**
    - 라이브러리 : 클래스의 집합, 코드의 재사용성 지원, 제어의 주체가 개발자 (코드에서 라이브러리 함수를 호출)
    - 프레임워크 : 제어의 주체가 프레임워크 (프레임워크에서 개발자의 코드를 호출), 프레임워크에서 기본적인 골격을 잡아놓음, 우리는 제어의 흐름에 맞게 코드 작성, 제어의 역전
4. Spring?
    - Lightweight, Java Application, Framework, POJO 기반의 Enterprise Application, 개발을 쉽고 편하게
    - 자바 어플리케이션을 개발하는데 필요한 하부 구조를 포괄적으로 제공
    - 스프링이 하부 구조 처리 → 개발자는 핵심 로직 개발에 집중 (Simplify Java Enterprise Development)
        
        ![스크린샷 2023-04-09 21.55.57.png](Spring%20Overview%207a3b46d56a10434f8af082afa63c81f1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_21.55.57.png)
        
    
    1. POJO, Plain Old Java Object
        - 심플한 자바 객체
        - 인터페이스, 상속 X
        - 스프링에서의 POJO는 **Bean**
        - Singletone인 경우가 많음
        - 스프링 컨테이너가 Bean을 관리(생성, 소멸 관리를 다 해줌) → new로 객체 생성할 필요X
    2. DI, Dependency Injection
        - 의존성 주입
        - Annotation (@Component, @Autowired ..)
            
            ![스크린샷 2023-04-09 22.03.03.png](Spring%20Overview%207a3b46d56a10434f8af082afa63c81f1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_22.03.03.png)
            
        - PersonService 클래스는 Person 객체에 의존하고 있음. (Person 객체를 생성자의 매개변수로 받고 있기 때문) Spring Container가 제공하는 Person 객체를 생성자에 주입 → Autowired Annotation
        - DI의 목적은 객체 간의 loose coupling, 약한 결합.
        - 객체를 생성하고 그들간의 의존성을 직접 주입하는 것보다 Spring IoC Container처럼 외부 컨테이너가 객체를 생성해주고 설정해주는 !!
    3. AOP, Aspect-Oriented Programming
        
        ![스크린샷 2023-04-09 22.10.05.png](Spring%20Overview%207a3b46d56a10434f8af082afa63c81f1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_22.10.05.png)
        
    4. PSA, Portable Service Abstraction
        - 다양한 서비스 레이어들을 추상화한 클래스
        - 스프링에서 PSA를 쓰면 서비스 레이어들간의 스위칭을 어플리케이션 코드를 수정하지 않고도 쉬움.