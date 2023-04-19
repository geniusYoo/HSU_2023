# Web Service

1. Web Service : HTTP
    - HTTP를 이용해 외부 데이터를 가져옴
    - 필연적으로 데이터를 가져오는 데 delay 발생
2. Web Service in iOS
    - 지연 문제를 해결하기 위해 Sub Thread 사용
    - 서브 스레드는 UI 업데이트 불가 → 동기화 이슈 생길 수 있기 때문!
        
        ![스크린샷 2023-04-19 20.11.38.png](Web%20Service%2006efbfe32d364ed3b8894bb81e3f2208/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-19_20.11.38.png)
        
3. URLSession, URLRequest
    1. URLSession
        1. Default Session : 디폴트, 디스크 기반 캐싱을 지원
        2. Ephemeral Session : 어떠한 데이터도 저장하지 않는 형태의 세션, 시크릿 세션
        3. Background Session : 앱이 종료된 이후에도 통신이 이뤄지는 것을 지원하는 세션 (다운로드 등)
    2. URLRequest
        - 서버로 요청을 보낼 때 어떻게 데이터를 캐싱할 것인지, 어떤 HTTP 메소드를 사용할 것인지, 어떤 내용을 전송할 것인지 등을 설정
    3. URLSessionTask
        - Task 객체는 일반적으로 세션 객체가 서버로 요청을 보낸 후, 응답을 받을 때 URL 기반의 내용들을 받는 (completion handler) 역할
            - Data Task : Data 객체를 통해 데이터 주고받는 태스크
            - Download Task : data를 파일의 형태로 전환 후 다운 받는 태스크 (백그라운드 지원)
            - Upload Task : data를 파일의 형태로 전환 후 업로드하는 태스크
            - Stream Task : 스트리밍으로 데이터를 받는 경우
4. URLSessionTask
    - `func dataTask(with request: URLRequest, completionHandler: complete) -> URLSessionDataTask`
        - complete: `@escape (Data?, URLResponse?, Error?) → Void`
        - dataTask 함수는 메인 스레드가 실행하는 것으로 completionHandler을 등록 후 바로 리턴. `@escape` 는 리턴 후에도 유효하도록 지원함
5. Completion Handler & URLResponse
    1. Completion Handler
        - `Task.resume()`으로 서비스를 요청하면 서비스 완료 후 호출되는 함수
        - `func aclouse(data: Data?, response: URLResponse?, error: Error?) → Void`
            - data: JSON 형태의 서비스 결과 데이터
            - response
            - error : 에러가 있는 경우 에러 정보
        - 서브 스레드에 의해 실행, UI 변경 시 에러 발생하니 주의!
    2. URLResponse
        - `var expectedContentLength: Int64` : 응답 컨텐츠의 예상 길이
        - `var suggestedFileName: String?` : 응답 데이터에 제안된 파일 이름
        - `var mimeType: String?` : 응답 MIME 타입
        - `var textEncodingName: String?` : 응답 원본 소스에서 제공하는 텍스트 인코딩명
        - `var url: URL?` : 응답 URL