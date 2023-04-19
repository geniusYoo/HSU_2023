# Spring Annotation

1. Spring Annotation
    - Annotation은 XML의 방대한 설정들을 축소할 수 있음
    - 디폴트로 enable X (명시적으로 Enable 해야함)
2. Annotations ..
    1. @Required
        - final 키워드와의 차이점 : final은 상수라고 *Compiler*에게 알려주는 것, @Required는 *Spring*에게!
        
        ![스크린샷 2023-04-09 22.51.41.png](Spring%20Annotation%20864f40b7ba974b42b60c09da5a4f3a88/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-09_22.51.41.png)
        
    2. **@Autowired *****
        - Setter 불필요, property도 불필요
        
        ![스크린샷 2023-04-14 13.10.31.png](Spring%20Annotation%20864f40b7ba974b42b60c09da5a4f3a88/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-14_13.10.31.png)
        
    3. @Qualifier
        - bean type이 2개 이상이면 qualifier로 구분
        
        ![스크린샷 2023-04-14 13.11.40.png](Spring%20Annotation%20864f40b7ba974b42b60c09da5a4f3a88/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-14_13.11.40.png)
        
    4. @Resource
        - @Autowired와 하는 일이 거의 비슷함
        - @Resource는 name으로 auto-wire, @Autowired는 type으로 auto-wire