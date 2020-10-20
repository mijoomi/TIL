# 컬렉션 

- list - 순서유지 , 중복저장가능 

- set - 순서 유지불가능  , 중복 저장 x 

- map - 키와 값을 쌍으로 저장 , 키는 중복저장 불가능 

# list 컬렉션

> List 컬렉션의 객체 추가 , 삽입, 찾기 ,삭제 방법

```java
List<Stirng> list = -
list.add("객체"); // 맨끝에 인덱스 추가
list.add(1,"객체"); // 지정된 인덱스에 객체 삽입
String srt = list.get(1); // 인덱스로 객체 찾기
list.remove(0); //인덱스로 객체 삭제 
list.remove("객체") // 객체 삭제 
```

> 객체를 대상으로 하나씩 반복해서 저장된 객체를 얻고 싶다면 다음과 같이 for문을 사용할수 있다.

```java
List<String> list = -;
for(int i=0;i<list.size();i++){
    String srt = list.get(i);
    //i인덱스에 저장된 String객체를 가져옴
}
```

> 인덱스 번호가 없다면 향상된 FOR문을 이용하는것이 편리하다 .

```java
for(String srt : list){
}
```

#  ArrayList

> 저장용량을 초과한 객체들이 들어오면 자동적으로 저장용량이 늘어난다 .
>
> 빈번한 객체 삭제와 삽입이 일어나는 곳에는 부적합
>
> 객체 검색이나 마지막에 객체추가는 좋은 성능을 발휘 

```java
List<String> list = new ArrayList<String>();
//선언방법
```

> ArrayList 사용예제 

```java
public class //클래스명 {
    public static void main(String [] args){
    List<String> list = new ArrayList<String>();
    
    list.add("JAVA");
    list.add("adfd");
    list.add("qwrq");
    list.add(2,"database");
    list.add("qwrs");
    
    int size = list.size();
    System.out.println("총객체수 :" + size);
    
    String skill = list.get(2);
    System.out.println("2:"+skill);
    
    for(int i=0;i<list.size();i++){
        String str = list.get(i);
        System.out.println(i+":"+str);
    }
    
    list.remove(2);
    list.remove(2);
    list.remove("qwrs");
    
    for(int i=0;i<list.size();i++){
        String str = list.get(i);
        System.out.println(i+":"+str)
}
}
    }
```

> 출력결과

```
총 객체수  : 5

2 : databaes 

0 : JAVA
1 : adfd
3 : qwrq
4 : qwrs

0 : java
1 : adfd
```

