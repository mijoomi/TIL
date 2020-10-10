# 메인 스레드

- **메인스레드**

  - `main` 메소드의 첫 코드부터 아래로 순차적으로 실행 

  - 마지막 코드를 실행하거나 `return`문을 만나면 실행종료

  ``` java
  public static void main(String[]args){
      // 필드
      // 실행문
  }
  ```



# 작업스레드

- **작업스레드**

  - 메인스레드 이외에 병렬로 작업이 필요할떄 사용

- **Thread 클래스로 부터 직접 생성 **

  ` Thread thread = new Thread(Runnable target);`

  `Runnale`를 매개값으로 갖는 생성자 호출

  `Runnale` 는 인터페이스 타입이기 때문에 구현객체 생성아 필요.

  `Runnale`에 `run` 메소드를 구현 클래스에서 재정의 해서 작업스레드가 실행할 코드를

  작성해야한다 .

  ```java
  class Task implements Runnable { //Runnable를 구현하는 Task 클래스
      public void run(){
          // 스레드가 실행할 코드 
      }
  }
  ```

- **작업스레드 사용 예시**

  ```java
  public class BeepTask implements Runnable{
   public void run(){ //스레드 실행내용
   Toolkit toolkit = Toolkit.getDefaultToolkit();
   for(int i=0; i<5; i++){
   	toolkit.beep();
   	try{Thread.sleep(500);} catch ( Exception e){}
     }
    }
  }
  ```

  ```java
  public class BeepPrintExample2{
  	public static void main (String[]args){
          
          Runnable beepTask = new BeepTask(); // beepTask 객체 생성 
          Thread thread = new Thread(beepTask);  // beepTask 작업스레드생성
          thread.start();
          
          for(int i =0; i<5;i++){
              System.out.println("띵");
              try{Thread.sleep(500); } 
              		catch ( Exception e){}
          }
      }
  }
  ```

  

- **Runnble 익명 객체 사용**

   ```java
  Thread thread = new Thread Runnable(){
      @Override
      public void run(){ //스레드 실행내용
  		 Toolkit toolkit = Toolkit.getDefaultToolkit();
  		 for(int i=0; i<5; i++){
   			toolkit.beep();
  		 	try{Thread.sleep(500);} catch ( Exception e){}
     }
    }
  }
  ```

- **람다식 이용**

  ```java
  Thread thread = new Thread(()->{
      	 Toolkit toolkit = Toolkit.getDefaultToolkit(); //스레드 실행내용
  		 for(int i=0; i<5; i++){
   			toolkit.beep();
  		 	try{Thread.sleep(500);} catch ( Exception e){}
     }
  });
  ```




# **Thread 하위 클래스로 부터 생성 **

- 작업스레드가 실행할 방법을 **Runnable로 생성하지 않고** Thread의 하위클래스로 작업스레드를 정의하면서 작업 내용을 포함 시키는 방법 

- Thread클래스를 상속한후 run 메소드를 재정의 해서 스레드가 실행할 코드를 작성

  ```java
  //Runnable를 생성하지 않고 Thread상속받아 작업스레드를 정의한 예제 
  public void BeepThread extends Thread {
      @Override
      public void run(){
           Toolkit toolkit = Toolkit.getDefaultToolkit(); //스레드 실행내용
  		 for(int i=0; i<5; i++){
   			toolkit.beep();
  		 	try{Thread.sleep(500);} catch ( Exception e){}
           }
      }
  }
  ```

  ```JAVA
  //BeepThread 클래스를 이용해서 작업 스레드 객체를 생성하고 실행
  public class BeepPrintExample3{
  	public static void main (String[]args){
          
          Thread thread = new BeepTask(); 
          thread.start();
          
          for(int i =0; i<5;i++){
              System.out.println("띵");
              try{Thread.sleep(500); } 
              		catch ( Exception e){}
          }
      }
  }
  ```

  

  # 정리

  - **현재의 클래스가 이미 다른 클래스로부터 상속 받고 있다면,`Runnable` 인터페이스를 이용하여 스레드를 생성**

    

