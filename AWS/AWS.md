# AWS(Amazon Web Services)
- 외부에서 본인이 만든 서비스에 접근하려면 `24시간 작동하는 서버`가 필수이다.

- 24시간 작동하는 서버에는 다음과 같은 3가지 선택지가 있다.

```
- 집에 PC를 24시간 구동시킨다.
- 호스팅 서비스(cafe24, 코리아호스팅등)을 이용한다.
- 클라우드 서비스(AWS, AZURE, GCP 등)을 이용한다.
```

- 일반적으로 비용은 호스팅 서비스나 집 PC를 이용하는 것이 저렴하다.
- 특정 시간에만 트래픽이 몰린다면 `유동적으로 사양을 늘릴 수 있는 클라우드가 유리`하다.

## 클라우드는 무엇인가?
- 클라우드 서비스는 쉽게 말하면 인터넷(클라우드)을 통해 서버, 스토리지(파일 저장소), 데이터베이스, 네트워크, 모니터링 등의 컴퓨팅 서비스를 제공하는 것이다.
- AWS에서는 개발자가 직접 해야 할 일을 전부 지원하고 있다.
- 이런 클라우드에는 다음과 같은 형태가 있다.
```
1. Infrastructure as a Service (IaaS, 아이아스, 이에스)
- 기존 물리 장비를 미들웨어와 함께 묶어둔 추상화 서비스이다.
- 가상머신, 스토리지, 네트워크, 운영체제 등의 IT 인프라를 대여해 주는 서비스이다.
- AWS의 EC2, S3 등

2. Platform as a Service (PaaS, 파스)
- 앞에서 언급한 IaaS에서 한 번 더 추상화한 서비스이다.
- 한 번 더 추상화했기 때문에 많은 기능이 자동화되어 있다.
- AWS의 Beanstalk, Heroku 등

3. Software as a Service (SaaS, 사스)
- 소프트웨어 서비스를 이야기한다.
- 구글 드라이브, 드랍박스, 와탭 등
```

# EC2 (Elastic Compute Cloud)
- AWS에서 제공하는 `성능, 용량 등`을 `유동적으로 사용할 수 있는 서버` 이다.
- AWS에서 리눅스 서버 혹은 윈도우 서버를 사용한다고 하면 EC2를 이야기하는 것이다.

## EC2 프리티어 플랜
무료로 제공하는 프리티어 플랜은 다음과 같은 제약 사항이 있다.
```
- 사양이 t2.micro만 가능.
    - vCPU(가상 CPU) 1 Core, 메모리 1GB 사양이다.
    - 보통 vCPU는 물리 CPU 사양의 절반 정도의 성능을 가진다.
- 월 750시간 제한이 있다. 초과하면 비용이 부과된다.
    - 24시간 * 31일 = 744시간이다.
    - 1대의 t2.micro만 사용한다면 24시간 사용할 수 있다.
```

## 리전
- 리전이란 AWS의 서비스가 구동될 지역을 이야기 한다.
- AWS는 도시별로 클라우드 센터를 지어 해당 센터에서 구축된 가상머신들을 사용할 수 있다.

## AMI (Amazon Machine Image)
- AMI는 EC2 인스턴스를 시작하는 필요한 정보를 `이미지로 만들어둔` 것이다.

# AWS 서버 생성시 꼭해야 할 설정들
- Java 8 설치 : 프로젝트의 버전에 맞게 설정하면 된다.
```
설치
sudo yum install -y java-1.8.0-openjdk-devel.x86_64

버전 변경
sudo /usr/sbin/alternatives --config java

사용하지 않는 버전 삭제
sudo yum remove java-1.7.0-openjdk

현재 java 버전 확인
java -version
```
- 타임존 변경 : 기본 서버의 시간은 미국 시간대 이기에 한국 시간으로 변경해야 한다.
```
UTC 타임존 변경
sudo rm /etc/localtime
sudo ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime

KST 타임존 확인
date
```
- 호스트네임 변경 : 현재 접속한 서버의 별명을 등록 한다. IP만으로는 어떤 서버가 어떤 역할을 하는지 알수 없기에 호스트 네임을 필수로 등록 한다.

호스트 이름 업데이트 유지
```
sudo vi /etc/cloud/cloud.cfg
preserve_hostname: true
```

시스템 호스트 이름을 퍼블릭 DNS로 변경
```
- Amazon Linux 2: hostnamectl 명령으로 호스트 이름을 설정하여 정규화된 도메인 이름을 반영한다.
sudo hostnamectl set-hostname webserver.mydomain.com

- Amazon Linux AMI: 텍스트 편집기로 /ect/sysconfig/network 구성 파일을 열고 HOSTNAME 항목을 변경하여 정규화된 도메인 이름을 반영한다.
sudo vi /etc/sysconfig/network
HOSTNAME=webserver.mydomain.com

변경후 서버 재부팅
sudo reboot
```