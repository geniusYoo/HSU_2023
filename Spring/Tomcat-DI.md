# Tomcat-DI

1. Structure

![스크린샷 2023-04-14 13.15.02.png](Tomcat-DI%20d04f92181df1478f9bf761ebfb8b80b0/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-14_13.15.02.png)

b.  Servlet Container

![스크린샷 2023-04-14 13.18.12.png](Tomcat-DI%20d04f92181df1478f9bf761ebfb8b80b0/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-14_13.18.12.png)

1. 웹서버로부터 HTTP 요청이 오고 Servlet Container에게 위임됨
2. Servlet Container는 service 메소드를 실행하기 전 서블릿을 로드
3. Servlet Container는 여러개의 요청을 멀티 스레드로 핸들링하고, 각각 스레드는 service 메소드를 서블릿의 싱글 인스턴스로 실행

c.  Singletone

1. Spring에서 빈들은 디폴트로 싱글톤
2. 스프링 컨테이너는 빈을 한번만 만들어서 같은 인스턴스를 어플리케이션 전체에서 사용
3. 스프링 컨테이너는 싱글톤 빈들을 생성하고 전역 접근이 가능하지만, 동시성 이슈를 해결 못함. 개발자들은 이 동시성 이슈를 해결할 적절한 로직을 구성해야 함.