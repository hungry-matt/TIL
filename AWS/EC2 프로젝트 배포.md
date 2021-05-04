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

# Reference
- 스프링 부트와 AWS로 혼자 구현하는 웹 서비스