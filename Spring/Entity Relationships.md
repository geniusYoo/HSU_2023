# Entity Relationships

1. 개요
    1. Relationship Multiplicities Type
        - `@OneToOne`
        - `@OneToMany`, `@ManyToOne`
        - `@ManyToMany`
    2. Direction
        - bidirectional : 양방향, owning side&inverse side
        - unidirectional : 단뱡향, only owning side
        - owning side : 레퍼런스를 갖고있는 entity side
2. Entity Relation Attributes
    - Cascade
        - 관계가 맺어진 entity에도 작업을 수행할 것인지
        - CascadeType
            - ALL, PERSIST, MERGE, REMOVE, REFRESH
            - default : no cascading
    - Fetch
        - 관계가 맺어진 entity들을 같이 조회할 것인지, 나중에 필요할 때 조회할 것인지
        - FetchType
            - LAZY(나중에), EAGER(처음부터 전부)
            - ___ To One ⇒ EAGER
            - ___ To Many ⇒ LAZY
3. Entity Relation Direction
    1. OneToMany Unidirectional, 1:N 단방향
        
        ![스크린샷 2023-04-18 20.04.16.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.04.16.png)
        
        - 하나의 Cateory에 여러개의 Products
        - OneToMany에서는 FK가 항상 Many쪽에 존재
        - *Category* : Parent table, One Side
        - *Product* : Child table, Many Side, FK 보유
        - `@JoinColumn` : 조인할 컬럼을 지정하고 이름 설정
        
        ![스크린샷 2023-04-18 20.08.48.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.08.48.png)
        
    2. OneToMany Bidirectional, 1:N 양방향
        - 자바 객체 사이의 연관을 서로 지어주는 것, A는 B에 액세스할 수 있고 B도 A에 액세스할 수 있는 것
        - ManyToOne의 경우, Product는 Category에 대한 하나의 레퍼런스만 있으면 되기 때문에 하나의 객체 레퍼런스만 만들면 됨
        - OneToMany의 경우, Category는 여러 Product의 레퍼런스가 필요하기 때문에 여러개의 객체 레퍼런스가 필요함
        
        ![스크린샷 2023-04-18 20.13.47.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.13.47.png)
        
        - `mappedBy` : 양방향 OneToMany일때 사용
            - Hibernate에게 자식 클래스에서 어떤 부모의 클래스의 variable을 사용하는지 알려주기 위함
            - 이 컬렉션 (`Set<Product>`)은 FK 컬럼으로 매핑된 variable로 로딩하라고 말해줌
        - `fetch=FetchType.LAZY`
            - 모든 Products를 한 카테고리를 로딩할때마다 전부 로딩할 필요가 없기 때문
        - `cascade=CascadeType.ALL`
            - Category가 저장되면 그에 관련된 Products도 전부 저장
            - Category를 삭제하면 Products도 전부 삭제됨
        
        ![스크린샷 2023-04-18 20.31.57.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.31.57.png)
        
        1️⃣ Parent Object 생성 (Category)
        
        2️⃣ Child Objects 생성 (Product)
        
        3️⃣ Child에 Parent 세팅 (Product에 Category 지정)
        
        4️⃣ Parent에 Child Collection 세팅 (Category.getProducts().add())
        
        5️⃣ Parent 저장 (Cascade.ALL 이어서 Child도 같이 저장)
        
    3. OneToOne Unidirectional, 1:1 단방향
        - 한 사람은 하나의 운전면허를 가질 수 있다.
            
            ![스크린샷 2023-04-18 20.43.50.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.43.50.png)
            
            ![스크린샷 2023-04-18 20.42.07.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.42.07.png)
            
            ![스크린샷 2023-04-18 20.42.18.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.42.18.png)
            
            ![스크린샷 2023-04-18 20.42.43.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.42.43.png)
            
            - License에서 setPerson()
            - Child 쪽에서 FK를 가지고 있기 때문에!
    4. OneToOne Bidirectional, 1:1 양방향
        
        ![스크린샷 2023-04-18 20.44.56.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.44.56.png)
        
        - `mappedBy` 사용
        
        ![스크린샷 2023-04-18 20.45.57.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.45.57.png)
        
    5. ManyToMany Unidirectional
        
        ![스크린샷 2023-04-18 20.46.12.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.46.12.png)
        
        - Join Table
            - 두 테이블의 PK만을 가지는 제 3의 SQL Table
            - 조인 테이블의 이름은 ManyToMany 이름에 언더바를 붙여서 관례적으로 만듦. 예로 Author_Book
        
        ![스크린샷 2023-04-18 20.51.30.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.51.30.png)
        
        ![스크린샷 2023-04-18 20.51.41.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.51.41.png)
        
        - `joinColumns` : 현재 이를 정의하는 클래스의 조인 컬럼
        - `inverseJoinColumns` : 다른 테이블의 조인 컬럼
        
        ![스크린샷 2023-04-18 20.54.00.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.54.00.png)
        
        ![스크린샷 2023-04-18 20.54.09.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.54.09.png)
        
        ![스크린샷 2023-04-18 20.54.26.png](Entity%20Relationships%20f1b6e87a5305411cbf2fd41dcc0648b8/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_20.54.26.png)