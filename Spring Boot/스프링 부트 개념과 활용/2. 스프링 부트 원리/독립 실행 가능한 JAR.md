# JAR (파일 포맷)

- JAR(Java Archive)는 많은 파일을 하나로 통합하는 플랫폼 독립 파일 형식이다.

- 여러개의 자바 클래스 파일과, 클래스들이 이용하는 리소스(텍스트, 이미지, 사운드) 및 메타데이터를 하나의 파일로 모아 응용소프트웨어나 라이브러리를 배포하기 위한 패키지 파일 포맷이다.

- 실제로 JAR는 ZIP 파일 포맷으로 이루어진 압축 파일이다. 자바 애플리케이션을 구성하는 요소들을 단일 파일로 묶어 압축된 형태인 JAR 파일은, 한 차례의 요청으로 애플리케이션 전체를 다운로드할 수 있게 해준다.

# Executable Jar Format

- 스프링 부트에서는 spring-boot-loader 모듈을 사용하여 실행 가능한 jar 및 war를 지원하고 있다. 

- Maven 플러그인이나 Gradle 플러그인을 사용하면 실행 가능한 jar가 자동 생성된다.

## Jar 파일 생성

Maven 빌드를 통해 생성된 target 디렉토리를 삭제한다.

```
> mvn clean
```

target 디렉토리에 압축된 jar 파일을 생성한다.

```
> mvn package
```

target 디렉토리 하위에 jar 파일이 생성된것을 확인할 수 있다.

![image](https://user-images.githubusercontent.com/45548349/120434649-b4855300-c3b7-11eb-9d2e-b04557e18f63.png)


target 디렉토리에서 다음과 같이 jar 파일을 실행하면 애플리케이션이 작동하는걸 확인할 수 있다.

```
> java -jar srping-boot-getting-started-1.0-SNAPSHOT.jar
```

## Jar 파일 구조

jar 파일은 다음과 같이 구성되어 있다.

```
example.jar
 |
 +-META-INF
 |  +-MANIFEST.MF
 +-org
 |  +-springframework
 |     +-boot
 |        +-loader
 |           +-<spring boot loader classes>
 +-BOOT-INF
    +-classes
    |  +-mycompany
    |     +-project
    |        +-YourClasses.class
    +-lib
       +-dependency1.jar
       +-dependency2.jar
```

- 자바에서는 jar 파일안에 있는 파일들을 읽을수 있는 표준 방법이 없다.

- org.springframework.boot.loader.jar.JarFile : Jar 파일들을 읽어들이는 loader 이며 BOOT-INF/lib 안에 있는 의존성을 읽어들이는 역할을 한다.

- org.springframework.boot.loader.Launcher : Main-Class의 main() 메소드를 호출하여 애플리케이션을 실행한다.

jar 파일의 메타 정보를 가지고 있는 MANIFEST.MF 파이을 보면 다음과 같이 실행에 필요한 정보를 담고 있다.

```
Main-Class: org.springframework.boot.loader.JarLauncher
Start-Class: com.example.Application
```

이렇게 애플리케이션 실행에 필요한 클래스 및 리소스들을 압축된 jar 파일 하나로 실행하는 것이 스프링 부트의 주요 목표였다.

# Reference
- [JAR](https://ko.wikipedia.org/wiki/JAR_(%ED%8C%8C%EC%9D%BC_%ED%8F%AC%EB%A7%B7)#cite_note-3)

- [The Executable Jar](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/html/appendix-executable-jar-format.html#executable-jar)