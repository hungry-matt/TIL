# EC2 프로젝트 배포

# 1. 프로젝트 clone 받기
- 깃허브에서 코드를 받아올수 있게 EC2에 깃을 설치한다.

```
sudo yum install git
```

- 설치가 완료되면 설치 상태를 확인한다.

```
git --version
```

- 확인 완료되면 git clone으로 프로젝트를 저장할 디렉토리를 생성한다.

```
mkdir ~/app && mkdir ~/app/step1
```

- 생성한 디렉토리로 이동한다.

```
cd ~/app/step1
```

- 깃허브에서 https 주소를 복사하여 git clone을 진행한다.

```
git clone 복사한 주소
```

- clone이 완료되면 다음과 같이 출력된다.

![image](https://user-images.githubusercontent.com/45548349/116854687-0c069680-ac33-11eb-92a4-1cd2cde275c4.png)

- 클론한 프로젝트 디렉토리로 이동하여 코드들이 잘 수행되는지 테스트를 진행한다.

```
./gradlew test
```

- 만약 gradlew 실행 권한이 없다는 메세지가 뜨면 다음 명령어로 해결한다.

```
chmod +x ./gradlew
```

- 프로젝트에 오류가 있어 수정하고 깃허브에 푸쉬 했다면 프로젝트 디렉토리에서 다음 명령어를 사용한다.

```
git pull
```

- 테스트가 완료 되면 다음과 같이 출력된다.

![image](https://user-images.githubusercontent.com/45548349/116855889-23468380-ac35-11eb-97b8-598a57b610c6.png)

> EC2에는 그레이들이 설치 되지 않았다. 하지만, Gradle Task를 수행할 수 있다. 이는 프로젝트 내부에 포함된 gradlew 파일 때문이다. gradlew(gradle wrapper)란 새로운 환경에서 프로젝트를 설정할 때 java나 gradle을 설치하지 않고 해당 프로젝트에 한해서 빌드를 지원하는 파일이다.

# 2. 배포 스크립트 만들기
작성한 코드를 실제 서버에 반영하는 것을 배포라고 한다. 다음은 앞으로 배포시 해야 하는 과정이다.

1. git clone 또는 git pull을 통해 새로운 프로젝트를 받음.
2. Gradle이나 Maven을 통해 테스트 및 빌드
3. EC2 서버에서 프로젝트 실행 및 재실행

배포할 때마다 이러한 과정을 하나하나 실행하면 불편하기에 쉘 스크립트를 작성하여 스크립트를 실행하면 앞의 과정을 차례대로 실행하도록 해보겠다.

- vim을 통해 스크립트 파일 생성

```
vim ~app/step1/deploy.sh
```

- 배포 스크립트 작성

```sh
#!/bin/bash

#1
REPOSITORY=/home/ec2-user/app/step1
PROJECT_NAME=spring-boot

#2
cd $REPOSITORY/$PROJECT_NAME/

#3
echo "> Git Pull"
git pull

#4
echo "> 프로젝트 Build 시작"

./gradlew build


echo "> step1 디렉토리 이동"

cd $REPOSITORY

#5
echo "> Build 파일 복사"

cp $REPOSITORY/$PROJECT_NAME/build/libs/*.jar $REPOSITORY/

#6
echo "> 현재 구동중인 애플리케이션 pid 확인"

CURRENT_PID=$(pgrep -f ${PROJECT_NAME}*.jar)

#7
echo "현재 구동중인 애플리케이션 pid: $CURRENT_PID"

if [ -z "$CURRENT_PID" ]; then
    echo "> 현재 구동 중인 애플리케이션이 없으므로 종료하지 않습니다."
else
    echo "> kill -15 $CURRENT_PID"
    kill -15 $CURRENT_PID
    sleep 5
fi
    #8
    echo "> 새 애플리케이션 배포"

    JAR_NAME=$(ls -tr $REPOSITORY/ | grep *.jar | tail -n 1)

    #9
    echo "> JAR_NAME: $JAR_NAME"

    nohup java -jar $REPOSITORY/$JAR_NAME 2>&1 &
```
> #1 
> - 프로젝트 디렉토리 주소와 프로젝트 명은 스크립트 내에서 자주 사용하는 값이니 이를 변수로 저장한다. 
> - 쉘에서는 타입 없이 선언하여 저장한다.
> - 쉘에서는 $변수명 으로 변수를 사용할 수 있다.

> #2
> - 제일 처음 git clone 받았던 디렉토리로 이동한다.

> #3
> - 디렉토리로 이동 후, master 브랜치의 최신 내용을 받는다.

> #4
> - gradlew로 build를 수행한다.

> #5
> - build의 결과물인 jar 파일을 복사해 jar 파일을 모아둔 위치로 복사한다.

> #6
> - pgrep은 process id만 출력하는 명령어이다.
> - -f 옵션은 프로세스 이름으로 찾는다.

> #7
> - 현재 구동중인 프로세스 유무를 확인하여 작업을 수행한다.
> - process id를 확인하여 있다면 해당 프로세스를 종료한다.

> #8
> - ls -tr : -r 옵션은 알파벳 역순으로 나열되며 -t나 -S를 조합하여 시간 역순, 크기 역순으로 나열이 가능하다. 
> - tail -n 1 : -n 옵션은 원하는 라인의 수 만큼 출력할 수 있다. 마지막 1라인을 출력한다.
> - 새로 실행할 jar 파일을 찾는다.
> - 가장 나중의 최신 jar 파일을 변수에 저장한다.

> #9
> - 일반적으로 자바를 실행할때 java -jar로 사용하는데, 이렇게 하면 사용자가 터미널을 종료하면 애플리케이션도 종료가 된다. 그래서 사용자가 터미널을 종료해도 애플리케이션이 계속 구동될 수 있도록 nohup 명령어를 사용한다.
> - 스프링 부트는 내장 톰캣이 있어서 jar 파일만 있으면 바로 웹 애플리케이션 서버를 실행할 수 있다.
> - 마지막 &는 background로 기동한다는 의미이다.
> - 2>&1 : n>&m 의 형태로 (0: 표준입력, 1: 표준출력, 2: 표준에러)를 의미한다. 즉, >를 기준으로 표준에러를 표준출력이되는 곳으로 전달하라는 의미이다.

- 스크립트 실행 권한 추가
```
chmod +x ./deploy.sh
```

- 배포 실행
```
./deploy.sh
```

실행이 완료되면 다음과 같이 출력된다.

![image](https://user-images.githubusercontent.com/45548349/117258855-63ea0b00-ae88-11eb-8a99-eaa521de3b22.png)

잘 실행되었는지 확인하기 위해 nohub.out 파일을 열어 로그를 확인하면 다음과 같이 에러가 발생하여 실행에 실패한걸 확인할 수 있다.

![image](https://user-images.githubusercontent.com/45548349/117258531-0950af00-ae88-11eb-8138-f1187e745414.png)

# 3. 외부 Security 파일 등록하기
해당 에러의 이유는 ClientRegistrationRepository를 생성하려면 cliendId와 clientSecret이 필수이다. 그런데 이 정보를 가진 application-oauth.properties가 외부로 공개가 되면 안되기에 프로젝트에 올라가 있지 않은 상태이다.

그래서 이 정보를 서버에서 직접 가지고 있도록 하겠다.

- 서버에서 가지고 있을 prperties 파일을 생성한다.

```
vim /home/ec2-user/app/application-oauth-properties
```

- 로컬 프로젝트에 있는 application-oauth-properties 내용을 그대로 복사하여 넣고 다음과 같이 deploy.sh 파일을 수정한다.

```sh
nohup java -jar \
-Dspring.config.location=classpath:/application.properties, /home/ec2-user/app/application-oauth.properties \
$REPOSITORY/$JAR_NAME 2>&1 &
```

> -Dspring.config.location :
> - 스프링 설정 파일 위치를 지정한다.
> - classpath가 붙으면 jar 안에 있는 resources 디렉토리 기준으로 경로가 생성된다.
> - application-oauth.properties 파일은 외부에 있기 때문에 절대경로를 사용한다.

- 다시 배포 실행을 하여 확인한다.

![image](https://user-images.githubusercontent.com/45548349/117264269-08bb1700-ae8e-11eb-952d-3293c5f9475b.png)

# 4. 스프링 부트 프로젝트로 RDS 접근하기
- RDS에서는 MariaDB를 사용중이다.
- 이 MariaDB에서 스프링 부트 프로젝트를 사용하기 위해 다음과 같은 작업이 필요하다.

```
1. 테이블 생성 : H2에서 자동으로 생성해주던 테이블을 MariaDB에서 직접 생성해야 한다.

2. 프로젝트 설정 : 자바 프로젝트가 MariaDB에 접근하기 위해서는 데이터베이스 드라이버가 필요하다. 사용 가능한 드라이버를 추가 한다.

3. EC2(리눅스 서버) 설정 : 데이터베이스 접속 정보를 보호하기 위한 설정을 추가한다.
```

## RDS 테이블 생성
- JPA가 사용될 엔티티 테이블
```sql
create table posts (
    id bigint NOT NULL AUTO_INCREMENT,
    created_date TIMESTAMP, 
    modified_date TIMESTAMP, 
    author varchar(255),
    content TEXT not NULL,
    title varchar(500) not NULL,
    primary key (id)
) engine=InnoDB;

create table user (
    id bigint NOT NULL auto_increment, 
    created_date timestamp, 
    modified_date timestamp, 
    email varchar(255) not null, 
    name varchar(255) not null, 
    picture varchar(255), 
    role varchar(255) not null, 
    primary key (id)
) engine=InnoDB;
```
- 스프링 세션 테이블

프로젝트에서 schema-mysql.sql 파일을 검색하여 찾을수 있다.

```sql
CREATE TABLE SPRING_SESSION (
	PRIMARY_ID CHAR(36) NOT NULL,
	SESSION_ID CHAR(36) NOT NULL,
	CREATION_TIME BIGINT NOT NULL,
	LAST_ACCESS_TIME BIGINT NOT NULL,
	MAX_INACTIVE_INTERVAL INT NOT NULL,
	EXPIRY_TIME BIGINT NOT NULL,
	PRINCIPAL_NAME VARCHAR(100),
	CONSTRAINT SPRING_SESSION_PK PRIMARY KEY (PRIMARY_ID)
) ENGINE=InnoDB ROW_FORMAT=DYNAMIC;

CREATE UNIQUE INDEX SPRING_SESSION_IX1 ON SPRING_SESSION (SESSION_ID);
CREATE INDEX SPRING_SESSION_IX2 ON SPRING_SESSION (EXPIRY_TIME);
CREATE INDEX SPRING_SESSION_IX3 ON SPRING_SESSION (PRINCIPAL_NAME);

CREATE TABLE SPRING_SESSION_ATTRIBUTES (
	SESSION_PRIMARY_ID CHAR(36) NOT NULL,
	ATTRIBUTE_NAME VARCHAR(200) NOT NULL,
	ATTRIBUTE_BYTES BLOB NOT NULL,
	CONSTRAINT SPRING_SESSION_ATTRIBUTES_PK PRIMARY KEY (SESSION_PRIMARY_ID, ATTRIBUTE_NAME),
	CONSTRAINT SPRING_SESSION_ATTRIBUTES_FK FOREIGN KEY (SESSION_PRIMARY_ID) REFERENCES SPRING_SESSION(PRIMARY_ID) ON DELETE CASCADE
) ENGINE=InnoDB ROW_FORMAT=DYNAMIC;

```

## 프로젝트 설정

- 프로젝트에 있는 build.gradle 파일에 드라이버를 추가한다.

```gradle
compile("org.mariadb.jdbc:mariadb-java-client")
```

- 운영 서버에서 구동될 환경 설정을 추가한다.

실제 운영 환경에서는 보안/로그상 이슈가 될 만한 설정들을 제거 하여 src/main/resources/ 에 application-real.properties 이름의 파일을 생성하여 다음 내용을 작성한다.

```properties
spring.profiles.include=oauth, real-db
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5InnoDBDialect
spring.session.store-type=jdbc
```

## EC2 설정

- RDS 접속 정보도 보호해야 하므로 서버에 직접 설정 파일을 둔다.

```
vim ~/app/application-real-db.properties
```

- application-real-db.properties 파일에 다음과 같이 작성한다.

```properties
#1
spring.jpa.hibernate.ddl-auto=none
spring.datasource.url=jdbc:mariadb://rds주소:포트 번호/데이터베이스명
spring.datasource.username=db계정
spring.datasource.password=db계정 비밀번호
spring.datasource.driver-class-name=org.mariadb.jdbc.Driver
```

> #1
> - JPA로 테이블이 자동으로 생성되는 옵션을 none으로 지정한다.
> - `실제 운영에서 사용될 테이블이니 스프링 부트에서 새로 만들지 않도록 주의해야 한다.`

- 마지막으로 deploy.sh 파일에 real profile을 사용할 수 있도록 추가 한다.

```sh
nohup java -jar \
-Dspring.config.location=classpath:/application.properties,/home/ec2-user/app/application-oauth.properties,/home/ec2-user/app/application-real-db.properties \
-Dspring.profiles.active=real \
$REPOSITORY/$JAR_NAME 2>&1 &
```

> -Dspring.profiles.active=real :
> - application-real.properties를 활성화 시킨다.
> - application-real.properties에 spring.profiles.include=oauth, real-db 옵션 때문에 application-real-db.properties 역시 함께 활성화 대상에 포함된다.

- 마지막으로 배포 실행후 curl 명령어로 잘 실행 되는지 확인한다.

```
curl localhost:8080
```

# 구글에 EC2 주소 등록

기존에 연결했던 구글 로그인 서비스가 작동하지 않는걸 확인할 수 있다. 해당 서비스에 EC2의 도메인을 등록하지 않았기 때문이다.

- 다음과 같이 승인된 리디렉션 URI에 EC2의 퍼블릭 DNS를 등록한다.

![image](https://user-images.githubusercontent.com/45548349/117288344-5c395f00-aea6-11eb-8b5d-92563f848bfd.png)



# Reference
- 스프링 부트와 AWS로 혼자 구현하는 웹 서비스