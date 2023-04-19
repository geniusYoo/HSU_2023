# JPA-Hibernate

1. JDBC vs JPA(Hibernate) vs Spring Data JPA
    
    ![스크린샷 2023-04-18 18.43.21.png](JPA-Hibernate%2094a26d18b09c4b369d7e9dfc65115065/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.43.21.png)
    
    - JDBC : Low-level Database Access
    - JPA(Jaba Persistence API) : 관계형 DB를 사용하는 방식을 정의한 인터페이스, Spec
    - Hibernate : JPA의 구현체, JPA+Hibernate를 쓰면 데이터베이스를 정교하게 다룰 수 있지만 어려움
    - Spring Data JPA : JPA를 쓰기 쉽게 만들어놓은 모듈
    - Boilerplate code : 틀에 박힌 코드, Spring이나 Lombok에서 자동 생성해주는 코드들
    
    ![스크린샷 2023-04-18 18.50.52.png](JPA-Hibernate%2094a26d18b09c4b369d7e9dfc65115065/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.50.52.png)
    
2. ORM (Object-Relational Mapping)
    
    ![스크린샷 2023-04-18 18.51.41.png](JPA-Hibernate%2094a26d18b09c4b369d7e9dfc65115065/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.51.41.png)
    
3. JPA vs Hibernate
    
    ![스크린샷 2023-04-18 18.52.28.png](JPA-Hibernate%2094a26d18b09c4b369d7e9dfc65115065/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.52.28.png)
    
    ![스크린샷 2023-04-18 18.56.58.png](JPA-Hibernate%2094a26d18b09c4b369d7e9dfc65115065/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.56.58.png)
    
    - 모든 메소드가 EntityManager에 의해 정의되고 이는 Hibernate Session.
    - Entity .. → JPA
    - Session, Entity.. 를 상속받는 것 → Hibernate
4. Extended Persistence Context
    
    ![스크린샷 2023-04-07 20.19.43.png](JPA-Hibernate%2094a26d18b09c4b369d7e9dfc65115065/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-07_20.19.43.png)
    
    - `session.save()` : Application → Persistence Context(일종의 cache)로 저장일수도, DB로 저장일수도 ,,
    - `session.get()` : Persistence Context에서 가져옴
    - 그리고 나중에 DB에 저장
    - 그래서 `save()` → `get()` 해도 get이 먼저 실행되고 Hibernate가 DB에 저장하는 순서로 진행됨.
    - `save()` → `createQuery()` : save시 cache에 저장하는 것이 아닌 DB에 저장 후에 createQuery시 DB에서 가져옴.
    - `createQuery()`와 `get()` 시 Hibernate 내부적으로 작동방식이 다름,,,
5. Use Case
    1. JPA + JPA Provider(Hibernate)
        - JPA 구현체를 Hibernate가 아닌 다른 구현체를 사용해도 어플리케이션에는 아무 영향이 없음 → PSA (Portable Service Abstraction)
    2. only Hibernate
    
    ![스크린샷 2023-04-18 19.00.44.png](JPA-Hibernate%2094a26d18b09c4b369d7e9dfc65115065/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_19.00.44.png)