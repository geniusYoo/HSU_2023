# Spring MVC Web Form

1. Web Basics
    1. 요청 파라미터
        - `GET` : 쿼리스트링
        - `POST` : HTTP body
2. Data Binding
    - 요청 파라미터를 객체에 어떻게 바인딩할 것이냐 ,,
    1. 순수 해결법, `@RequestParam`
        
        ![스크린샷 2023-04-16 20.57.46.png](Spring%20MVC%20Web%20Form%204c462ea7febd4ec4a91b252f0b916ebc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_20.57.46.png)
        
    2. Spring Data Binding
        - Form → Object Binding
        - 진행 순서
            - Form Bean이 생성됨
            - Form Bean이 요청 파라미터들로 채워짐
            - Form Bean이 모델에 추가됨
        
        ![‘offer’ form bean은 모델에 자동적으로 추가됨, 그래서 뷰에서도 offer에 접근 가능한 것.](Spring%20MVC%20Web%20Form%204c462ea7febd4ec4a91b252f0b916ebc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.00.54.png)
        
        ‘offer’ form bean은 모델에 자동적으로 추가됨, 그래서 뷰에서도 offer에 접근 가능한 것.
        
3. Data Validation
    1. Hibernate Validator
        
        ![스크린샷 2023-04-16 21.11.41.png](Spring%20MVC%20Web%20Form%204c462ea7febd4ec4a91b252f0b916ebc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.11.41.png)
        
        - 유저의 에러가 감지되면 form data를 검증해야 함
        - Bean Validation API (JSR-303)은 제약조건을 걸어서 특정 제약을 정의해둠. `@NotNull`, `@Pattern`, `@Size`
    2. Message Interpolation
        
        ![스크린샷 2023-04-16 21.11.07.png](Spring%20MVC%20Web%20Form%204c462ea7febd4ec4a91b252f0b916ebc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.11.07.png)
        
        - 제약조건에 걸리면 에러 메시지를 만들어 사용자에게 알려주는 것
        - message descriptor
    3. Validating Object
        - `@Valid` 사용
        - BindingResult Object로 Validation Error를 볼 수 있음
        
        ![스크린샷 2023-04-16 21.10.52.png](Spring%20MVC%20Web%20Form%204c462ea7febd4ec4a91b252f0b916ebc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.10.52.png)
        
4. Data Buffering
    - 필수 입력 필드를 입력하지 않아서 오류가 났는데, 다시 전부 입력 ,,?
    1. Spring form tag library
        - `prefix=”sf”`
        
        ![스크린샷 2023-04-16 21.23.38.png](Spring%20MVC%20Web%20Form%204c462ea7febd4ec4a91b252f0b916ebc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.23.38.png)
        
    2. JSP 파일 수정
        
        ![스크린샷 2023-04-16 21.24.42.png](Spring%20MVC%20Web%20Form%204c462ea7febd4ec4a91b252f0b916ebc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.24.42.png)
        
    3. Controller 수정
        - Web Form 생성 시
        
        ![스크린샷 2023-04-16 21.27.43.png](Spring%20MVC%20Web%20Form%204c462ea7febd4ec4a91b252f0b916ebc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.27.43.png)
        
        - Web Form Validation
        
        ![스크린샷 2023-04-16 21.28.43.png](Spring%20MVC%20Web%20Form%204c462ea7febd4ec4a91b252f0b916ebc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.28.43.png)
        
5. Error Messages
    1. 오류 시 BindingResult 객체는 자동적으로 모델에 들어가서 뷰로 전달됨
        
        ![스크린샷 2023-04-16 21.31.33.png](Spring%20MVC%20Web%20Form%204c462ea7febd4ec4a91b252f0b916ebc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.31.33.png)
        
    2. `<sf:errors>`
        - View
            
            ![스크린샷 2023-04-16 21.33.16.png](Spring%20MVC%20Web%20Form%204c462ea7febd4ec4a91b252f0b916ebc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.33.16.png)
            
        - Object
            
            ![스크린샷 2023-04-16 21.33.33.png](Spring%20MVC%20Web%20Form%204c462ea7febd4ec4a91b252f0b916ebc/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.33.33.png)