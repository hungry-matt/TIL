# Introducing Spring Boot

Spring Boot makes it easy to create stand-alone, production-grade Spring-based Applications that you can run. We take an opinionated view of the Spring platform and third-party libraries, so that you can get started with minimum fuss. Most Spring Boot applications need very little Spring configuration.

```
- Spring Boot를 사용하여 제품 수준의 독립적인 애플리케이션을 쉽게 만들수 있다.
- 스프링 프레임워크에서 자주 사용되는 설정을 기본적으로 제공해 준다.
- 스프링 플랫폼과 제3의 라이브러리의 기본 설정도 제공해 준다. (톰캣이 대표적인 사례)
- 최소한의 설정으로 쉽고 빠르게 사용할수 있다.
```

Our primary goals are:

- Provide a radically faster and widely accessible getting-started experience for all Spring development.
- Be opinionated out of the box but get out of the way quickly as requirements start to diverge from the defaults.
- Provide a range of non-functional features that are common to large classes of projects (such as embedded servers, security, metrics, health checks, and externalized configuration).
- Absolutely no code generation and no requirement for XML configuration.

```
- 모든 스프링 개발에 빠르고 광범위하게 사용될수 있는 시작 환경을 제공한다.
- 자주 사용되는 설정을 기본적으로 제공해주지만 요구사항에 맞게 쉽고 빠르게 변경할수 있다.
- 비즈니스 로직을 구현하는데 필요한 기능뿐만 아니라 다양한 비기능 기능을 제공한다.
- 절대로 코드 생성과 XML 설정을 사용하지 않는다.
```

# System Requirements
Spring Boot 2.0.3.RELEASE requires Java 8 or 9 and Spring Framework 5.0.7.RELEASE or above. Explicit build support is provided for Maven 3.2+ and Gradle 4.

- 스프링 부트는 Java 8 이상 부터 사용할 수 있다. Maven 3.2 이상 그리고 Gradle 4에 대한 지원이 제공된다.

# Servlet Containers
Spring Boot supports the following embedded servlet containers:
Name | Servlet Version
---|---
Tomcat 8.5 | 3.1
Jetty 9.4 | 3.1
Undertow 1.4 | 3.1

## 참고 및 출처
- [Spring Boot Reference Guide](https://docs.spring.io/spring-boot/docs/2.0.3.RELEASE/reference/htmlsingle/#getting-started-introducing-spring-boot)