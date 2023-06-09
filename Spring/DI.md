# DI

1. Object Dependencies
    
    ![스크린샷 2023-04-09 22.14.28.png](DI%2035cdf856cd074e8a8f590942a1ed6284/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_22.14.28.png)
    
    ![스크린샷 2023-04-09 22.15.16.png](DI%2035cdf856cd074e8a8f590942a1ed6284/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_22.15.16.png)
    
    1. PetOwner 객체는 AnimalType 객체, Dog에 의존
    2. PetOwner-AnimalType 객체 간의 강한 결합
2. Dependency Injection
    
    ![스크린샷 2023-04-09 22.18.19.png](DI%2035cdf856cd074e8a8f590942a1ed6284/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_22.18.19.png)
    
    1. Bean Container는 Bean을 만들고 의존성 주입을 수행
    2. 제어의 역전, 개발자가 아닌 Spring Container가 관리
    
    ![스크린샷 2023-04-09 22.20.00.png](DI%2035cdf856cd074e8a8f590942a1ed6284/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_22.20.00.png)
    
    ![스크린샷 2023-04-09 22.22.13.png](DI%2035cdf856cd074e8a8f590942a1ed6284/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_22.22.13.png)
    
    1. Controller는 MyService 객체에 의존
    2. Controller를 Unit Test 하려면 Moked Service 사용
    
    - DI는 객체의 의존성이 객체 자체가 아니라 프레임워크에 의해 주입되는 설계 패턴
    - 여러개의 객체 간의 결합도를 낮춤
3. Spring IoC Container
    - Spring Framework에서 핵심 컴포넌트
    - 객체의 생성과 관리, 객체 의존성 주입
    - 설정 방식은 XML, Java Annotations, Class 기반
    - 스프링 컨테이너는 BeanFactory, ApplicationContext 타입이 존재
        
        ![스크린샷 2023-04-09 22.30.44.png](DI%2035cdf856cd074e8a8f590942a1ed6284/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_22.30.44.png)
        
4. Spring Container & DI
    
    ![스크린샷 2023-04-09 22.32.17.png](DI%2035cdf856cd074e8a8f590942a1ed6284/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_22.32.17.png)
    
5. DI의 장점
    - 의존도 감소, 코드 변경 최소화
    - 재사용성 증가
    - 테스트 용이
    - 가독성 증가
6. Bean 이란?
    - Spring에서의 POJO
    - 컨테이너로부터 제공되는 설정파일에 의해 생성됨
    - 빈으로 등록된 객체의 인스턴스들은 getBean()으로 접근 가능
7. Spring Bean Scope
    
    ![스크린샷 2023-04-09 22.35.26.png](DI%2035cdf856cd074e8a8f590942a1ed6284/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_22.35.26.png)
    
    1. singletone bean은 컨테이너에 의해 한번만 생성됨. 컨테이너가 종료될 때 같이 소멸됨
    2. prototype bean은 모든 요청에서 새로운 객체가 생성됨을 의미. 
    3. scope 지정 안해주면 디폴트로 singletone
8. DI Methods
    - 생성자 기반 주입
        
        ![스크린샷 2023-04-09 22.43.22.png](DI%2035cdf856cd074e8a8f590942a1ed6284/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_22.43.22.png)
        
    - Setter 기반 주입
        
        ![스크린샷 2023-04-09 22.43.37.png](DI%2035cdf856cd074e8a8f590942a1ed6284/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_22.43.37.png)