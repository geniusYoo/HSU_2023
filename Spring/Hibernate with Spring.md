# Hibernate with Spring

1. Integrating Hibernate & Spring
    1. Maven Dependency (libraries)
        
        ![스크린샷 2023-04-18 22.51.22.png](Hibernate%20with%20Spring%206019c5ce6cd446eda742c0fcf4d42d0b/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_22.51.22.png)
        
    2. Spring Bean Configuration (Datasource, SessionFactory, TransactionManager)
        - `dao-context.xml`
        - 원래는 hibernate.cfg.xmld에 DB 정보를 넣었지만 Spring과 Hibernate를 통합하려면 dao-context.xml에 작성해야 함
        - Datasource Bean
            
            ![스크린샷 2023-04-18 22.53.26.png](Hibernate%20with%20Spring%206019c5ce6cd446eda742c0fcf4d42d0b/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_22.53.26.png)
            
        - SessionFactory Bean
            
            ![스크린샷 2023-04-18 22.53.37.png](Hibernate%20with%20Spring%206019c5ce6cd446eda742c0fcf4d42d0b/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_22.53.37.png)
            
        - TransactionManager Bean
            
            ![스크린샷 2023-04-18 22.53.53.png](Hibernate%20with%20Spring%206019c5ce6cd446eda742c0fcf4d42d0b/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_22.53.53.png)
            
        - DAO Bean
            
            ![스크린샷 2023-04-18 22.54.36.png](Hibernate%20with%20Spring%206019c5ce6cd446eda742c0fcf4d42d0b/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_22.54.36.png)
            
        
    3. Entity Bean with Annotation (@Entity)
        - Mapping Model Class
            - Entity 클래스 → DB 테이블
            - Entity 클래스 필드 → DB 테이블 컬럼
            - Entity 인스턴스 → DB 테이블 row
        - JPA Annotations
            - `@Entity` : entity bean
            - `@Table` : table
            - `@Id` : primary key
            - `@GeneratedValue` : pk를 만드는 방법 지정
                - Strategy : AUTO(default), IDENTITY, SEQUENCE, TABLE
                - Hibernate4 → default가 IDENTITY
                - Hibernate5 → default가 TABLE, hibernate_sequence 테이블이 기본적으로 생성되는데, 여기에 들어있는 next_val은 다음에 사용할 id가 지정되어있고 이는 모든 테이블이 공유함 (컬럼의 id는 유니크해야해서 겹치면 안되기 때문)
                - MySQL은 SEQUENCE 지원X
            - `@Column` : 테이블 컬럼에 필드 매핑, 길이나 nullable 등 옵션 지정 가능
            - `@Transient` : DB에 저장하고 싶지 않은데, Entity 클래스에 포함시켜야 할 경우. 예) 이미지
    4. DAO Layer (Spring JDBC 버리고 Hibernate로 재구성)
        - 기본적으로 `@Repository` 사용
        - 추가적으로 `@Transactional` 지정해주면 모든 메소드를 트랜잭션으로 만듦.
        
        ```java
        @Repository
        @Transactional
        public class OfferDao {
        
            @Autowired
            private SessionFactory sessionFactory;
        
            //query and return a single object
            public Offer getOfferById(int id) {
                Session session = sessionFactory.getCurrentSession();
                Offer offer = session.get(Offer.class, id);
        
                return offer;
            }
        
            //query and return multiple objects
            // cRud method
            public List<Offer> getOffers() {
                Session session = sessionFactory.getCurrentSession();
                String hql = "from Offer";
        
                Query<Offer> query = session.createQuery(hql, Offer.class);
                List<Offer> offerList = query.getResultList();
        
                return offerList;
            }
        
            // Crud method
            public void insert(Offer offer) {
                Session session = sessionFactory.getCurrentSession();
                session.saveOrUpdate(offer);
                session.flush();
        
            }
        
            // crUd method
            public void update(Offer offer) {
                Session session = sessionFactory.getCurrentSession();
                session.saveOrUpdate(offer);
                session.flush();
            }
        
            //cruD method
            public void delete(Offer offer) {
                Session session = sessionFactory.getCurrentSession();
                session.delete(offer);
                session.flush();
        
            }
        }
        ```