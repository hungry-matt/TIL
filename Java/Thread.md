# Thread
하나의 프로세스 내부에서 독립적으로 실행되는 작업 단위.

1. 쓰레드를 구현하는 방법은 Thread 클래스를 상속 받거나 Runnable 인터페이스를 구현.
2. 다중 쓰레드 작업 시에는 각 쓰레드 끼리 정보를 주고 받을 수 있음.
3. 프로세스 끼리는 정보를 주고 받을 수 없음.

## Thread 클래스 상속
```java
public class Thread1 extends Thread {
    @Override
    public void run() {
        for (int x = 0 ; x < 5 ; x++) {
            System.out.println(getName());
        }
    }
}

public class ThreadMain {
    public static void main(String[] args) {
        final Thread1 thread1 = new Thread1();
        thread1.start();
    }
}
```
result is :
```
Thread-0
Thread-0
Thread-0
Thread-0
Thread-0
```

## Runnable 인터페이스 구현
Runnable 인터페이스 구현시 쓰레드 인스턴스의 매개변수로 넣어 주어야 한다.
```java
public class Thread2 implements Runnable{
    @Override
    public void run() {
        for (int x = 0 ; x < 5 ; x++) {
            System.out.println(Thread.currentThread().getName());
        }
    }
}

public class ThreadMain {
    public static void main(String[] args) {
        final Thread1 thread1 = new Thread1();
        thread1.start();

        Runnable runnable = new Thread2();
        final Thread thread2 = new Thread(runnable);
        thread2.start();
    }
}
```
resutl is :
```
Thread-0
Thread-0
Thread-0
Thread-0
Thread-0
Thread-1
Thread-1
Thread-1
Thread-1
Thread-1
```

Thread 클래스 소스를 살펴보면 Thread(Runaable target) 생성자 호출시 Runnable 인터페이스를 넘겨 주어야 한다.
```java
 /**
     * Allocates a new {@code Thread} object. This constructor has the same
     * effect as {@linkplain #Thread(ThreadGroup,Runnable,String) Thread}
     * {@code (null, target, gname)}, where {@code gname} is a newly generated
     * name. Automatically generated names are of the form
     * {@code "Thread-"+}<i>n</i>, where <i>n</i> is an integer.
     *
     * @param  target
     *         the object whose {@code run} method is invoked when this thread
     *         is started. If {@code null}, this classes {@code run} method does
     *         nothing.
     */
    public Thread(Runnable target) {
        init(null, target, "Thread-" + nextThreadNum(), 0);
    }
```

Thread 클래스의 run() 메서드는 JVM만이 호출 가능하며 run()이 호출되면 참조변수 target을 통해서 Runnable 인터페이스에서 구현한 run()이 호출 된다. 이렇게 하면 Thread 클래스를 상속 받아 오버라이딩 하지 않고도 외부에서 구현할 수 있다.
```java
 /**
     * If this thread was constructed using a separate
     * <code>Runnable</code> run object, then that
     * <code>Runnable</code> object's <code>run</code> method is called;
     * otherwise, this method does nothing and returns.
     * <p>
     * Subclasses of <code>Thread</code> should override this method.
     *
     * @see     #start()
     * @see     #stop()
     * @see     #Thread(ThreadGroup, Runnable, String)
     */
    @Override
    public void run() {
        if (target != null) {
            target.run();
        }
    }
```

# Multi Thread
여러 쓰레드를 동시에 실행 시키는 기법.

### 장점
1. 메모리 공유로 인한 시스템 자원 소모가 줄어 든다.
2. 동시에 두가지 이상의 작업이 가능해진다.

### 단점
1. 서로 자원을 소모하다가 충돌이 일어날 가능성이 존재한다.
2. 코딩이 난해해져 버그 생성 확률이 높아진다.

