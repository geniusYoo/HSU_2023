# Maven

1. About Maven
    1. Apache Build Manager for Java, Project Management Tool
    2. helps ..
        - Automatic Build Tool, 빌드 자동화
        - Dependency Managament Tool, 의존성 관리 (라이브러리를 효율적으로 관리)
        - Project Report & Web Site Generation
    3. Flow
        
        ![스크린샷 2023-04-16 21.39.33.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.39.33.png)
        
    4. Phase & Plugin
        
        ![스크린샷 2023-04-16 21.40.32.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.40.32.png)
        
        - Phase (단계) : compile → test → package 순서 중요!
        - Plugin : 각 Phase에서 필요한 프로그램, 실제 작업 수행, 적절한 Configuration이 필요
        - Plugin:Goal : Plugin은 하나의 작업만을 하는 것이 아니라서 goal이 존재
2. POM, Project Object Model
    - Maven의 설정파일이 `pom.xml`
    
    ![스크린샷 2023-04-16 21.44.25.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.44.25.png)
    
    ![스크린샷 2023-04-16 21.44.32.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.44.32.png)
    
3. Super POM
    - 관례적으로 일반적인 것들을 Super POM에서 설정해둠, 이를 상속받아 필요한 부분만 수정해서 재사용
    - Covention over configuration : 설정보다는 관습에 따르자 ㅋㅋㅋ
    - 비슷한 말로 Coding by convention (관습에 따른 코딩)
4. Maven Build
    1. Build Lifecycle
        - Sequence of phase, phase들로 이루어짐
        - phase들은 순차적으로 실행되고, compile 실행 시 그 전단계의 Phase들이 전부 순차적으로 실행된 뒤에 compile이 실행됨 !!
        
        ![스크린샷 2023-04-16 21.49.57.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.49.57.png)
        
        ![스크린샷 2023-04-16 21.51.13.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.51.13.png)
        
        ![스크린샷 2023-04-16 21.52.50.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-16_21.52.50.png)
        
    2. Plugins & Goal
        - Plugin은 하나 또는 여러개의 Goal들의 집합
        - groupId, artifactId, version 좌표로 구별
        - Configuration section에서 추가적인 파라미터로 커스터마이징 가능
        
        ![스크린샷 2023-04-17 23.20.47.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-17_23.20.47.png)
        
    3. Run a Maven Build
        - `**mvn <phase>**`
            - `mvn install`
            - install 이전의 phase들까지 같이 실행
        - `**mvn <plugin:goal>**`
            - `mvn archetype:generate \ -DgroupId=xxx.yyy -DartifactId=simple`
            - archetype : plugin, 용도에 따른 프로젝트의 템플릿
            - generate : goal
            - -D options : goal들의 파라미터
        
        ![스크린샷 2023-04-17 23.26.10.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-17_23.26.10.png)
        
5. Dependency Mechanism
    - 프로젝트의 dependency는 프로젝트가 의존하는 라이브러리
    - pom.xml에 dependency 추가
    - Maven은 원격 저장소에서 라이브러리를 자동 다운로드 → .m2 폴더에 저장
    1. Transitive Dependencies
        - Maven은 pom.xml을 읽어서 자동으로 라이브러리를 포함시킴.
        - 예) A가 B에 의존, C가 A에 의존한다면 :: C→A→B
        - Dependeny mediation - Nearest Definition (가까운 것으로)
            
            ![스크린샷 2023-04-18 14.04.58.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_14.04.58.png)
            
        - Dependency Exclusions
            - A 입장에서 B는 필요한데 C는 불필요 → C 제외!
                
                ![스크린샷 2023-04-18 14.06.23.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_14.06.23.png)
                
            
    2. **Dependency Scope **중요!**
        - Dependency를 쓰는 타이밍
        - Maven Compile Scope
            - Default Scope
            - build, test, run, package 할때 다 필요
            
            ![스크린샷 2023-04-18 14.09.13.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_14.09.13.png)
            
        - Maven Provided Scope
            - compile, test 할때는 필요, runtime엔 불필요
            - why?__ 외부에서 제공해주니까!! 예) tomcat
            
            ![스크린샷 2023-04-18 14.24.46.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_14.24.46.png)
            
        - Maven Runtime Scope
            - runtime, test 할때는 필요, compile에는 불필요
            - 예) mysql-connector-java같은 JDBC Driver
        - Maven Test Scope
            - 일반적인 오퍼레이션에서는 필요 없고 test 할때만!
        
        ![스크린샷 2023-04-18 14.28.02.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_14.28.02.png)
        
        → Provided, Test Scope는 절대 메인 프로젝트에 포함 Xx
        
6. Repositories
    
    ![스크린샷 2023-04-18 14.31.32.png](Maven%206c85370dccf1463ab47c1faaabd5a440/%25E1%2584%2589%25E1%2585%25B3%25E1%2584%258F%25E1%2585%25B3%25E1%2584%2585%25E1%2585%25B5%25E1%2586%25AB%25E1%2584%2589%25E1%2585%25A3%25E1%2586%25BA_2023-04-18_14.31.32.png)
    
    1. Remote Repository (원격) 
        - software artifacts 제공
        - repo1.maven.org
    2. Local Repository (로컬)
        - .m2
7. Useful Commands
    - `mvn package` : Compile + JAR/WAR 생성
    - `mvn install` : Package + 로컬 Repo에 복사
    - `mvn clean` : 타겟 디렉토리 삭제
    - `mvn test` : Unit Test
    - `mvn clean package` : clean + package
    - `mvn install -DskipTests` : 시간 절약을 위한 테스트 스킵