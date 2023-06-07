# SpringBoot Analyze

1. pom.xml
    - 상속 구조, 버전 명시할 필요 X
    - spring-boot-maven-plugin
        - 반드시 있어야 함
        - 실행 가능한 파일 패키징, springboot app run 해주는 역할
        - mvn package 하면 jar 플러그인이 실행되는데, SpringBoot에서는 추가로 spring-boot:repackage까지 실행됨
            
            ![스크린샷 2023-06-06 00.49.10.png](SpringBoot%20Analyze%205771df16607d4b619ba11a0401878819/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.49.10.png)
            
2. Application Entry Point Class
    - `**@SpringBootApplication` ***중요!**
        - 여러 Annotation의 조합
        - `@EnableAutoConfiguration` : 자동 설정
        - `@ComponentScan` : bean 등록
        - `@Configuration`
    - SpringApplication.run() 하면 뒤에서 Application Context 만들고, 빈들 등록하고, 톰캣 시작하고 .. 여러 작업들이 수행됨
    - WebApplicationType
        - NONE : 웹 어플리케이션이 아님, 웹서버 실행 X
        - REACTIVE : 반응형 웹 어플리케이션, 비동기, Reactive 웹서버 실행
        - SERVLET : 서블릿 기반 어플리케이션, Servlet 웹서버 실행
3. Component Scanning
    - root 패키지 내에 모든 컴포넌트들이 있다면 아무 문제가 없음.
    - 하지만, 루트 패키지가 아닌 다른 패키지에 있는 파일들도 component-scan 하고싶다면, 명시적으로 설정해줘야 함. → 가능한 root 패키지에 포함시키는 것을 권장
    
    ![스크린샷 2023-06-06 00.55.32.png](SpringBoot%20Analyze%205771df16607d4b619ba11a0401878819/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.55.32.png)
    
4. Spring Boot Dev Tools
    - 코드 수정되면 어플리케이션 자동 재시작
        
        ![스크린샷 2023-06-06 00.57.04.png](SpringBoot%20Analyze%205771df16607d4b619ba11a0401878819/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.57.04.png)
        
5. Thymeleaf
    
    ![스크린샷 2023-06-06 00.57.48.png](SpringBoot%20Analyze%205771df16607d4b619ba11a0401878819/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.57.48.png)
    
    - template는 틀
    - 동적으로 읽어서 페이지 로딩시킴
6. Application Properties
    
    ![스크린샷 2023-06-06 00.59.23.png](SpringBoot%20Analyze%205771df16607d4b619ba11a0401878819/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.59.23.png)
    

![스크린샷 2023-06-06 00.59.54.png](SpringBoot%20Analyze%205771df16607d4b619ba11a0401878819/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-06_00.59.54.png)

1. Annotations
    - `@GeneratedValue(strategy = GenerationType.IDENTITY)` : hibernate_sequence 테이블 생성 안하고 auto-increment
    - `@SpringBootTest` : Integration Test
    - `@WebMvcTest` : Unit Test
    - `@Transactional` : Test 하고 결과 rollback
    - `@Test` : Test 단위 나눠주기