# System.getProperty()
프로그램을 작성하다 보면 운영체제나 JVM에 의존적인 정보를 알아야 할 때가 있다.

이때, getProperty(key)를 이용하여 각종 정보를 알 수 있다.

```java 
public void getProperty() {
    System.getProperty("line.separator");
}
```

## Property Infomation
```
java.runtime.name=Java(TM) 2 Runtime Environment, Standard Edition
sun.boot.library.path=C:\Program Files\Java\jdk1.5.0_18\jre\bin
java.vm.version=1.5.0_18-b02
java.vm.vendor=Sun Microsystems Inc.
java.vendor.url=http://java.sun.com/
path.separator=;
java.vm.name=Java HotSpot(TM) Client VM
file.encoding.pkg=sun.io
user.country=KR
sun.java.launcher=SUN_STANDARD
sun.os.patch.level=Service Pack 3
java.vm.specification.name=Java Virtual Machine Specification
user.dir=C:\java\client

java.runtime.version=1.5.0_18-b02
java.awt.graphicsenv=sun.awt.Win32GraphicsEnvironment
java.endorsed.dirs=C:\Program Files\Java\jdk1.5.0_18\jre\lib\endorsed
os.arch=x86
java.io.tmpdir=C:\DOCUME~1\ADMINI~1\LOCALS~1\Temp\
line.separator=

java.vm.specification.vendor=Sun Microsystems Inc.
user.variant=
os.name=Windows XP
sun.jnu.encoding=MS949
java.library.path=C:\Program Files\Java\jdk1.5.0_18\bin;

java.specification.name=Java Platform API Specification
java.class.version=49.0
sun.management.compiler=HotSpot Client Compiler
os.version=5.1
user.home=C:\Documents and Settings\Administrator
user.timezone=
java.awt.printerjob=sun.awt.windows.WPrinterJob
file.encoding=MS949
java.specification.version=1.5
user.name=Administrator
java.vm.specification.version=1.0
sun.arch.data.model=32
java.home=C:\Program Files\Java\jdk1.5.0_18\jre
java.specification.vendor=Sun Microsystems Inc.
user.language=ko
awt.toolkit=sun.awt.windows.WToolkit
java.vm.info=mixed mode, sharing
java.version=1.5.0_18
file.separator=\
java.vendor.url.bug=http://java.sun.com/cgi-bin/bugreport.cgi
sun.cpu.endian=little
sun.io.unicode.encoding=UnicodeLittle
sun.desktop=windows
sun.cpu.isalist=pentium_pro+mmx pentium_pro pentium+mmx pentium i486 i386 i86
```

## 주요 검색어
```
java.version	Java 버전
java.vendor	Java 공급자
java.vendor.url	Java 공급자 주소
java.home	Java를 설치한 디렉토리
java.class.version	Java 클래스 버전
java.class.path	Java 클래스 경로
java.ext.dir	확장기능의 클래스 경로
os.name	운영체제 이름
os.arch	운영체제 아키텍처
os.version	운영체제 버전 정보
file.separator	파일 구분 문자
path.separator	경로 구분 문자
line.separator	행 구분 문자
user.name	사용자 계정
user.home	사용자 홈 디렉토리
user.dir	현재 디렉토리
```
