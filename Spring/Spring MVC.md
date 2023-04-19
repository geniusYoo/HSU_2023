# Spring MVC

1. Spring MVC Framework
    - Model
        - 어플리케이션 데이터를 캡슐화하고, 일반적으로 POJO로 구성됨
    - View
        - 모델 데이터 렌더링을 담당하고 일반적으로 HTML 출력을 생성
    - Controller
        - 사용자 요청 처리, 적절한 모델 구축을 담당하고 렌더링을 위해 뷰에 전달
2. Architecture
    
    ![이거 진짜 중요하다 … *****](Spring%20MVC%204993e8d73c4045a39747c3f3be5b8812/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-14_13.30.13.png)
    
    이거 진짜 중요하다 … *****
    
    ![이것도 무조건 외우기](Spring%20MVC%204993e8d73c4045a39747c3f3be5b8812/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_20.50.18.png)
    
    이것도 무조건 외우기
    
3. Overview
    1. Dispatcher Servlet
        - 사용자의 request를 받음
        - Handler Mapping에게 이 request를 어떤 Controller가 실행하게 할지 물어봄
    2. Handler Mapping
        - 특정 요청을 수행하는 Controller를 매핑.
        - 이를 xml, annotation으로 정보를 제공해주면 매핑해줌
    3. Controller
        - 다른 비즈니스 로직 클래스들을 호출함으로써 request처리
        - 모델을 뷰로 넘김
    4. View Resolver
        - logical name으로부터 physical view files를 찾음
        - 뷰를 찾아줌
    5. View
        - physical view file
        - JSP, HTML, XML, Velocity Templates ..
4. Required Configurations
    1. Maven Configuration `POM.xml`
        
        ![스크린샷 2023-04-16 20.07.18.png](Spring%20MVC%204993e8d73c4045a39747c3f3be5b8812/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_20.07.18.png)
        
    2. Web Deployment Descriptor `Web.xml`
        - DispatcherServlet
            - 스프링 컨테이너 (WebApplicationContext)를 생성
            - DI 컨테이너가  WebApplicationContext에게 설정파일들을 제공해야 함
                
                ![스크린샷 2023-04-16 20.10.02.png](Spring%20MVC%204993e8d73c4045a39747c3f3be5b8812/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_20.10.02.png)
                
        - ContextLoadListener
            - 공유되는 빈들을 포함하는 스프링 컨테이너를 생성
            - DispatcherServlet에 의해 생성된 빈들은 ContextLoadListener에 의해 생성된 빈들을 참조할 수 있음
            
            ![스크린샷 2023-04-16 20.12.05.png](Spring%20MVC%204993e8d73c4045a39747c3f3be5b8812/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_20.12.05.png)
            
        - code example
            
            ![스크린샷 2023-04-16 20.14.18.png](Spring%20MVC%204993e8d73c4045a39747c3f3be5b8812/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_20.14.18.png)
            
    3. Spring MVC Configurations `root-context.xml` `servlet/dao/service-context.xml`
        - root-context.xml
            - 모든 servlet들과 필터들에게 공유되는 root 스프링 컨테이너 설정 파일
            - 이는 ContextLoadListener에 의해 로딩됨. 디폴트는 비어 있음
        - servlet-context.xml
            - DispatcherServlet에 의해 로딩됨.
            - `<resources mapping=”..” location=”” />` : 정적인 자원들은 여기 있다고 알려줌
            - `<annotation-driven />` : annotation을 사용하겠다
            - Bean InternalResourceViewResolver : 스프링에게 실제 JSP 파일의 위치를 알려줌
            - `<context:component-scan ..>` : 지정해준 패키지들을 스캐해 annotation들을 찾아서 빈으로 등록
5. Model
    - 이름이 부여된 객체들의 집합
    
    ![스크린샷 2023-04-16 20.26.13.png](Spring%20MVC%204993e8d73c4045a39747c3f3be5b8812/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_20.26.13.png)
    
    1. java.util.map (Java)
        - service Layer 호출 → model에 집어넣기
        
        ![스크린샷 2023-04-16 20.29.24.png](Spring%20MVC%204993e8d73c4045a39747c3f3be5b8812/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_20.29.24.png)
        
    2. Model (Spring)
        - 이름을 지정해주지 않아도 됨. 자동 생성해줌
        - key 없이 value만 존재
        
        ![스크린샷 2023-04-16 20.30.15.png](Spring%20MVC%204993e8d73c4045a39747c3f3be5b8812/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_20.30.15.png)
        
    3. ModelMap (Spring)
        - addAttribute() 체이닝 콜
        
        ![스크린샷 2023-04-16 20.30.50.png](Spring%20MVC%204993e8d73c4045a39747c3f3be5b8812/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_20.30.50.png)
        
6. Controller
    - Spring Controller들은 @Controller 어노테이션이 붙은 빈들
    1. Class level mapping 
        - class에다가 @RequestMapping 달아놓고 메소드에 추가하는 식
    2. Handler level mapping
        - 각각 메소드에 매핑 정보 설정
7. View
    1. JSTL (JSP Standard Tag Library)
        - JSP 확장을 위한 태그 라이브러리
        - `prefix=”c”` : core language
        - `prefix=”fn”` : JSTL 함수들