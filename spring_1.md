# spring framework_1

> 골격만 잇는 프레임 건물 , 느슨한 결합성
>
> 라이브러리와의 차이 - 라이브러리는 필요한것을 가져다 쓰는것

>  @Bean  - 스프링이 생성하는 객체 , 해당메서드가 생성한 객체를 스프링이 관리

```java
	AnnotationConfigApplicationContext ctx  = 
	new AnnotationConfigApplicationContext(Appcontext.class);
    //자바 설정에서 정보를 읽어와 빈 객체 생성관리
    
        Greeter g = ctx.getBean("greeter",Greeter.class);
	// 빈 객체를 검색 ( "메서드이름",객체타입 ) 
```

> DI - 의존 주입 (의존 객체를 전달받는 방식)

```java
private MemberDao memberDao = new MemberDao();

//의존객체 전달로 변경 ->
private MemberDao memberDao;

public MemberDaoRegisterService(MemberDao memberDao){
    this.memberDao = memberDao;
}
```

```java
MemberDao memberDao = new MemberDao();
MemberRegisteService regSvc = new MemberRegisteService(memberDao);
//의존할 객체 변경시 MemeberDao 부분만 변경하면됨 -> 의존 객체 변경의 유연함 
```

  

