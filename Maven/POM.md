# POM (Project Object Model)
- POM은 프로젝트의 구조와 내용을 설명하고 있다.
- pom.xml 파일에 프로젝트 관리, 빌드에 필요한 환경설정과 의존성 관리 등의 정보를 기술 한다.

# 최소한의 POM 구성
```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>myproject</artifactId>
    <version>0.0.1-SNAPSHOT</version>

</project>
```

- groupId : 프로젝트 그룹 아이디
- artifactId : 프로젝트 아이디
- version : 명시된 그룹의 artifact 버전