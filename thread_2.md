# 스레드의 이름

>  이름이 큰역활은 아니지만 디버깅 할때 어떤 스레드가 **어떤 작업을 하는지 조사할 목적**으로 사용

``` java
thread.setName("스레드 이름"); //스레드 이름 변경
```

```java
thread.getName(); //스레드 이름을 알고 싶을 경우
```

> **`setName` 와` getName`는 `Thread`의 인스턴스 메소드이므로 스레드의 객체 참조 필요 **

```java
Thread thread = Thread.currentThread();
```

> **메인 스레드 이름 출력 및 UserThread 생성 및 시작**

```java
public class ThreadNameExample{
	publc static void main(String[]args){
    	Thread mainThread = Thread.currentThread();
        Systme.out.println("프로그램 시작 스레드 이름 :" + mainThread.getName());
        
        ThreadA threadA = new ThreadA(); // ThreadA 생성
          System.out.println("작업스레드 이름"+ threadA.getName());
        thread.start(); // ThreadA 시작 
        
        Thread threadB = new ThreadB(); //ThreadB 생성
        System.out.print("작업스레드 이름"+threadB.getName());
        threadB.start(); //ThreadB 시작
}
}
```

```java
public class ThreadA extends Thread{
    public ThreadA()
        setName("ThreadA");
}
	public void run() {
        for(int i =0; i<2;i++){
            System.out.println(getName()+"가 출력한 내용");
        }
    }
}
```

```java
public class ThreadB extends Thread{
	public void run() {
        for(int i =0; i<2;i++){
            System.out.println(getName()+"가 출력한 내용");
        }
    }
}
```

> **출력결과**

```java
프로그램 시작 스레드 이름 : main // 메인스레드 name
작업 스레드 이름 : ThreadA		// set메소드로 변경한 name 출력
ThreadA가 출력한 내용 
ThreadA가 출력한 내용 
작업 스레드 이름 : Thread-1	// 변경하지 않았기 때문에 Thread-n 이름 출력
Thread-1가 출력한 내용
Thread-1가 출력한 내용 
```



# 스레드 우선순위

- 멀티 스레드는 동시성 또는 병렬성으로 실행되기 때문에 이 용어들에 대해 정확히 이해하는것이 좋다.
- 동시성은 멀티 작업을 위해 **하나의 코어에서 멀티 스레드가 번갈아가며 실행**하는 성질
- 병렬성은 멀티 작업을 위해 **멀티 코어에서 개별 스레드를 동시에 실행**하는 성질
- 스레드 우선순위 방식은 **우선순위가 높은 스레드가 실행 상태를 더 많이 가지도록** 스케줄링하는 것을 말한다 

>**순환 할당방식**

		- 순환 할당 방식은 시간 할당량을 정해서 하나의 스레드를 정해진 시간 만큼 실행하고 다시 다른스레드를 실행하는 방식
		- **우선순위 방식은 스레드 객체에 우선 번호를 부여할 수 있기 때문에 개발자가 코드로 제어가능 **
		- **순환 할당 방식은 자바 가상 기계에 의해서 정해지기 때문에 제어 불가능**

> **우선순위 할당방식**

- 1~10까지 부여가능 , 1이 순위가 가장 낮고 10이 가장 높다 . 순위를 부여하지 않으면 스레드는 기본적으로 5의 순위를 할당 받는다.

> 우선순위를 변경하는 방법

```java
thread.setPriority(우선순위);
```

- 매개값으로 1~10의 값을 직업 주어도 되지만 코드의 가독성을 높이기 위해 Thread 클래스의 

  상수를 사용할 수 있다 .

```java
thread.setPriority(Thread.MAX_PRIORITY); //10의 값
thread.setPriority(Thread.NORM_PRIORITY); // 5 의값
thread.setPriority(Thread.MIN_PRIORITY); // 1의 값
```

- 쿼드 코어일 경우 최소 5개 이상의 스레드가 실행 되어야 우선순위에 영향을 미침 