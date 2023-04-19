# Hibernate

1. Data Persistence
    - 데이터 지속성
    - Application은 Persistence Storage인 DB에 데이터를 저장해야 함
    
    ![스크린샷 2023-04-18 14.38.42.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_14.38.42.png)
    
2. DB에 데이터를 저장하는 방법 3가지 
    1. JDBC
    2. Spring JDBC (template)
    3. Hibernate (ORM Framework)
3. ORM, Object Relational Mapping
    - 객체지향 언어의 객체 - 관계형 데이터베이스의 테이블 Mapping
    - 데이터의 구조가 RDBMS와 자바의 객체 모델이 다르기 때문에 ORM Libraries로 그 갭을 줄임
    
    ![스크린샷 2023-04-18 14.45.28.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_14.45.28.png)
    
4. Object-Relational Mismatch
    1. Granularity, 데이터 분할의 정도
        - 자바에서는 코드 재사용성과 유지보수성을 위해 Person, Address 객체를 분할해서 갖고 있음
        - DB는 오직 Person 테이블 하나만을 가짐
    2. Inheritance, 상속
        - 자바와는 다르게 DB는 상속의 개념 자체가 X
    3. Identity, 동일성
        - DB는 동일한 필드가 없음 (primary key로 모든 필드를 구분)
        - 자바는 같은 객체를 정의 `a==b`, `a.equals(b)`
    4. Associations, 참조
        - 자바는 객체 레퍼런스를 이용해 참조
        - DB는 foreign key로 참조
    5. Navigation, 검색
        - 자바는 그래프를 따라서 객체가 연결되어 있기 때문에, `user1.getBillingDetails().getAccountNumber()` 같이 체이닝으로 데이터를 검색할 수 있음
        - DB에서는 체이닝으로 검색하면 비효율적. SQL 쿼리를 최소화하는것이 속도나 메모리 사용량에 효율적임
5. Association
    - 자바에서는 객체를 직접적으로 참조, 양방향 관계를 잡을 때 참조를 2번 해주면 됨
    - DB에서는 테이블 조인과 FK를 사용해서 관계를 잡음
    
    ![스크린샷 2023-04-18 16.22.25.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_16.22.25.png)
    
    1. One-to-One Relationship
        - 각 학생은 유니크한 주소를 가짐
        
        ![스크린샷 2023-04-18 16.28.01.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_16.28.01.png)
        
        ![스크린샷 2023-04-18 16.33.10.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_16.33.10.png)
        
    2. One-to-Many Relationship
        - 한명의 학생은 핸드폰 번호를 여러 개 가질 수 있음
        
        ![스크린샷 2023-04-18 16.33.52.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_16.33.52.png)
        
        - 조인 컬럼, Many쪽에서 One을 참조
        
        ![스크린샷 2023-04-18 16.35.00.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_16.35.00.png)
        
        - 조인 테이블, One쪽에서 Many를 참조
        
        ![스크린샷 2023-04-18 16.36.00.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_16.36.00.png)
        
6. **Hibernate**
    - JAVA를 위한 ORM 솔루션
    - Java type → SQL data type
    - low-level SQL을 핸들링하기 때문에 JDBC 코드가 축소 → 개발자에게 good
    1. Application Architecture
        
        ![스크린샷 2023-04-18 16.44.29.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_16.44.29.png)
        
        ![스크린샷 2023-04-18 16.45.23.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_16.45.23.png)
        
        ![스크린샷 2023-04-18 16.46.59.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_16.46.59.png)
        
    2. Configuration Object
        - SessionFactory를 만들기 위해 mapping과 DB Connection 사용
        - Database Connection Information → Hibernate Config
            
            ![스크린샷 2023-04-18 17.15.38.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_17.15.38.png)
            
        - Mapping Information → Hibernate Mapping
            - `@Entity` : Java Class → DB Table
            - `@Column` : Field → DB Columns
    3. SessionFactory Object
        - Session은 한번만 만들어서 application 종료까지 하나로 씀
        - `SessionFactory.openSession()`
            - 항상 new session open
            - 작업이 끝나면 session close, flush 해줘야 함 → 안닫아도 스프링이 해주긴 함
        - `SessionFactory.getCurrentSession()`
            - 처음에 호출하면 new session open됨
            - 닫아줄 필요 없음
        
        ![스크린샷 2023-04-18 17.26.18.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_17.26.18.png)
        
        ![스크린샷 2023-04-18 17.26.31.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_17.26.31.png)
        
    4. Session Object
        - application-DB간의 “conversation”
        - DB의 물리적 커넥션을 얻을 수 있음
        - 장시간 열어둔 상태로 두면 안됨 → thread-safe 아니기 때문
        - 매핑된 Entity 클래스들에게 CRUD operations 제공
        - DB에 저장하기 전에 객체를 First-level Cache에 캐싱
            
            ![First-level Cache](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_17.31.41.png)
            
            First-level Cache
            
    5. Object States
        
        ![스크린샷 2023-04-18 17.40.58.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_17.40.58.png)
        
        - Transient
            - Session과 관계를 맺지 않고 DB에서도 아무런 관계가 정의되지 않은 Persistent Class의 새로운 인스턴스 상태
        - Persistent
            - Session과 관계를 맺은 새로운 Transient 인스턴스 만들수 있는 상태
            - 해당 클래스를 DB로서 사용할 수 있고, Session과 연결되어 value를 operation 가능
        - Detached
            - Hibernate Session을 닫으면 Persisent 인스턴스가 Detached 인스턴스 상태가 됨
        
        ![스크린샷 2023-04-18 17.40.46.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_17.40.46.png)
        
    6. Session Methods
        - `Object get(Class class, Serializable id)`
            - Entity 클래스에게 persistent 인스턴스를 리턴하거나 인스턴스가 없으면 null 리턴
        - `Serializable save(Object object)`
            - DB에 객체 저장
            - 생성된 Entity의 id 리턴
            - `cascade=”save-update”`
        - `void saveOrUpdate(Object object)`
            - save() 보다는 이걸 쓰자!
            - id가 있으면 update(), 없으면 save()
            - `cascade=”save-update”`
        - `void delete(Object object)`
            - DB에서 Persistent 인스턴스 삭제
            - `cascade=”delete”`
        - `void flush()`
            - session 메모리에 홀딩된 persistent 객체를 DB에 동기화
            - 단위 작업의 엔딩에 트랜잭션을 커밋하고 세션을 닫은 후 실행하는 게 적절함
            - 4 Flush Mode
                - Always : 모든 쿼리에 flush → 캐시의 목적 없음
                - Commit : 트랜잭션이 커밋되었을 때 flush
                - Manual : 수동으로 flush
                - Auto : default, 쿼리가 실행되거나 트랜잭션이 커밋되기 전에 flush
                
                ![스크린샷 2023-04-18 18.05.58.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.05.58.png)
                
        - `close()`
            - JDBC 커넥션이 릴리즈되고 클린함으로써 session end
            - 스프링이 해줌
            
            ![스크린샷 2023-04-18 18.23.53.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.23.53.png)
            
        - `Query createQuery(String queryString)`
            - HQL(Hibernate Query Language)로 쿼리를 만듦
                
                ![스크린샷 2023-04-18 18.24.59.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.24.59.png)
                
    7. Transaction Object
        - DB에서의 작업의 단위
        - Hibernate에서 트랜잭션은 transaction manager 아래에서 핸들링 됨
        
        ![스크린샷 2023-04-18 18.26.44.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.26.44.png)
        
    8. Query Object
        - `Session.createQuery()` 로 쿼리를 만들 수 있음
        - SQL, HQL을 이용해 DB를 검색하거나 객체 생성 가능
        - query parameter를 바인딩하여 쿼리로 인해 리턴되는 결과의 수를 제한할 수 있음
        
        ![스크린샷 2023-04-18 18.30.58.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.30.58.png)
        
    9. HQL
        - 특징
            - SQL과 유사
            - table, column의 실제 이름을 사용하지 않고 클래스와 프로퍼티 이름을 사용
            - SQL이나 HQL 키워드들은 대소문자 구분 X
            - 자바 클래스와 객체는 대소문자 구분 O
        - HQL 실행 방법
            - HQL 작성 `String hql = “Your Query”`
            - Session으로 create Query `Query query = session.createQuery(hql)`
            - query 실행
                - `List listResult = query.getResultList()`
                - `int rowsAffected = query.executeUpdate()`
    10. Query Example
        
        ![스크린샷 2023-04-18 18.36.18.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.36.18.png)
        
        - List Query
            
            ![스크린샷 2023-04-18 18.37.01.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.37.01.png)
            
        - Search Query
            
            ![스크린샷 2023-04-18 18.37.24.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.37.24.png)
            
            - Hibernate가 자동적으로 Product, Category 테이블을 JOIN
        - Update Query
            
            ![스크린샷 2023-04-18 18.38.10.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.38.10.png)
            
        - Delete Query
            
            ![스크린샷 2023-04-18 18.38.36.png](Hibernate%2028f41995e5f046c6b09c15ad345f4de1/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_18.38.36.png)