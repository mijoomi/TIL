# 동기화 메소드와 동기화 블록

> **공유 객체를 사용 할때 주의 할점 **

여러개의 스레드를 사용 하면 , 사용중인 스레드에서 다른 스레드에 의해서 값이 변경 되어 의도 했던것과 다른 결과를 받을수 있다 .

> **스레드가 사용중인 객체를 다른 스레드가 변경 할 수 없도록 하려면 ?**

스레드 작업이 끝날때 까지 객체에 잠금을 걸어서 다른 스레드가 사용 할 수 없도록 해야한다 .

멀티 스레드 프로그램에서 단 하나의 스레드만 실행할 수 있는 코드영역을 **임계영역**이라고한다.

자바는 임계영역을 지정하기 위해 동기화 메서드와, 동기화 블록을 제공한다 .

> **동기화  메서드를 만드는 방법**

메소드 선언에 `synchronized`키워드를 붙인다 , 인스턴스와 정적 메소드 어디든 사용가능 .

> 동기화 메서드 사용 예제 

```java
//메소드 전체를 임계영역으로 사용 
public synchronized void method(){
    //단하나의 스레드만 실행
}
```

```java
//일부 내용만 임계영역으로 사용 
public void method(){
     //여러스레드가 실행가능 영역 
    
    synchronized(공유객체){
        //임계영역 
    }
    
    //여러스레드가 실행가능 영역 
}
```

> **동기화 메서드**

```java
public class Calculator
    public int momory;
	
	public int getMemory(){
	return memory;
    }
	
	public synchronized void setMemory(int memory){ 
        //임계영역으로 하나의 스레드만 실행가능
        this.memory = memory;
        try {
            Thread.sleep(2000);
        } catch(InterruptedException e) {}
        System.out.println(Thread.currentThread().get.name()+":"+,this.memory);
    }
}
```

