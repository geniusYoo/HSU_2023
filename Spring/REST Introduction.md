# REST Introduction

1. What is REST ?
    - REpresentational State Transfer, 웹 서비스를 개발하는 아키텍처 스타일
    - HTTP 프로토콜 사용
    - HTTP 기본적인 메소드를 사용하는 common interface
    - REST 서버는 resource에 대한 접근을 제공
    - Text, JSON, XML을 사용하는데 JSON이 대체적으로 많이 쓰임
    
    ![RESTful Web Service](REST%20Introduction%20397ce362943d4815b034c669619ac012/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-05_22.58.55.png)
    
    RESTful Web Service
    
2. RESTful Web Services - Messages
    - HTTP Request (5)
        - Method : HTTP 메소드 `GET`, `POST`, `PUT`, `DELETE` ..
        - URI : Uniform Resource Identifier, 서버에서 자원을 식별하는 식별자
        - HTTP Version : `HTTP v1.1`
        - Request Header : HTTP Requestd에 들어갈 metadata를 포함한 key-value의 쌍. 예) `client type`, `format supported by the client`, `format of the message body`, `cache settings` .. etc
        - Request Body
    - HTTP Response (4)
        - Status/Response Code : 요청된 자원에 대한 서버의 status. `200 OK`
        - HTTP Version : `HTTP v1.1`
        - Response Header : HTTP Response에 들어갈 metadata를 포함한 key-value의 쌍. 예) `content length`, `content type` .. etc
        - Response Body
    - Content Negotiation
        - Request
            - Accept (text/html, application/xhtml + xml, application/xml) : 난 이런 종류의 Response를 원해, 내가 지금 보내는 건 너가 받을 내가 원하는 리스트야.
        - Response
            - Content-Type (text/html; charset=UTF-8) : 이건 내가 너한테 보내는 Response야.
    - HTTP Status/Response Codes
        - 2xx : Success `200 OK`, `201 Created`
        - 3xx : Redirection `303 See Other`
        - 4xx : Client Error `404 Not Found`
        - 5xx : Server Errorn `500 Internal Server Error`
        
3. Addressing
    
    ![스크린샷 2023-06-05 23.13.11.png](REST%20Introduction%20397ce362943d4815b034c669619ac012/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-05_23.13.11.png)
    
    - Standard URI 규칙
        - 복수형 명사를 사용하자. `users`
        - 띄어쓰기 X, 언더스코어나 하이픈을 이용하자.
        - 소문자를 사용하자.
        - URI가 업데이트되면, Redirection을 잘 해주자.
        - HTTP 메소드 이름을 사용하지 말자.
        
4. Statelessness
    - 상태를 유지하지 않는다. 즉, client의 상태 정보를 저장하지 않는다.
    - 장점
        - 각 method request를 비종속적으로 처리할 수 있다.
        - client의 이전 interaction을 유지할 필요가 없어서 application이 간단해진다.
        - HTTP 자체가 statelessness한 프로토콜이므로, RESTful 웹 서비스가 잘 어울림.
        
5. Caching
    - 같은 resource들을 계속해서 요청하는 것을 서버에서 caching을 통해 저장하고 있는 것
    
    ![스크린샷 2023-06-05 23.29.10.png](REST%20Introduction%20397ce362943d4815b034c669619ac012/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-05_23.29.10.png)
    
    ![스크린샷 2023-06-05 23.28.52.png](REST%20Introduction%20397ce362943d4815b034c669619ac012/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-05_23.28.52.png)
    
    ![스크린샷 2023-06-05 23.31.15.png](REST%20Introduction%20397ce362943d4815b034c669619ac012/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-06-05_23.31.15.png)
    
- 웹 서버는 자원의 현재 상태를 ETag 값과 함께 반환.
    - ETag : 자원의 버전 관리, 변경 사항이 생기면 ETag를 수정해서 버전을 관리해줌
    
1. Security
    - RESTful Web Service를 디자인할때, Security적으로 지켜야 할 사항들
        - Validation : 서버에서 모든 input을 validation하자.
        - Session Based Authentication
        - No Sensitive Data in URL : username, password, session token같은 민감한 정보를 URL 에 포함시키지 말고 POST로 보내자.
        - Restriction on Method Execution : 제한된 메소드 사용. GET, POST, DELETE
        - Validate Malformed XML/JSON
        - Throw generic Error Messages