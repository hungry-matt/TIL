# SSH 란?
Secure Shell의 약자로 원격지에 있는 컴퓨터를 안전하게 제어하기 위한 프로토콜 또는 이 프로토콜을 사용하는 프로그램들을 의미한다.
SSH 클라이언트와 SSH 서버의 관계로 상호작용하면서 SSH 서버가 설치된 운영체제를 제어한다.
클라이언트와 서버 사이에는 강력한 암호화 방법을 통해서 연결되어 있기 때문에 데이터를 중간에서 가로채도 해석 할 수 없는 암호화된 문자만이 노출 된다.

## SSH 클라이언트
리눅스와 Mac과 같은 Unix 계열의 운영체제는 기본적으로 SSH 클라이언트가 설치되어 있다. 하지만 윈도우 운영체제는 SSH 클라이언트가 설치 되어 있지 않기 때문에 설치 해야 윈도우에서 Unix 계열의 운영체제를 제어 할 수 있다.

### 대표적인 SSH 클라이언트
- PuTTY
- Xshel

## SSH 서버
SSH는 Unix 계열의 운영체제를 원격에서 제어하기 위한 방법 이다.
그렇기 때문에 원격지에 있는 윈도우 운영체제를 SSH로 제어 하는 것은 일반적이지 않다. 유닉스 계열의 운여에제에서는 OpenSSH가 가장 많이 사용된다. OpenSSH는 SSH 클라이언트와 서버를 포함한다.