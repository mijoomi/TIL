# 이것이 자바다 6장 연습문제 20번 

```java
public class Account {
    private String ano;
    private String owner;
    private int balance;

    public Account(String ano,String owner,int balance){
        this.ano =ano;
        this.owner = owner;
        this.balance = balance;
    }

    public String getAno() {
        return ano;
    }

    public void setAno(String ano) {
        this.ano = ano;
    }

    public String getOwner() {
        return owner;
    }

    public void setOwner(String owner) {
        this.owner = owner;
    }

    public int getBalance() {
        return balance;
    }

    public void setBalance(int balance) {
        this.balance = balance;
    }
}
```

```java
import java.util.Scanner;

public class BankApplication {
    private static Account[] accountArray = new Account[100];
    private static Scanner sc = new Scanner(System.in);

    public static void main(String[] args) {
        boolean run = true;

        while (run) {
            System.out.println("-------------");
            System.out.println("1. 계좌 생성 2.계좌 목록 3. 예금 4. 출금 5. 종료");
            System.out.println("-------------");
            System.out.println("선택 > ");

            int selectNo = sc.nextInt();

            if (selectNo ==1) {
                createAccount();
            } else if (selectNo ==2) {
                accountList();
            } else if (selectNo ==3) {
                deposit();
            } else if (selectNo ==4) {
                withdraw();
            } else if (selectNo ==5) {
                run = false;
            }
        }
        System.out.println("프로그램 종료");
    }

    private static void createAccount() { //계좌생성 메서드
        String ano;
        String owner;
        int balance;

        System.out.println("계좌 번호 입력 : ");
        ano = sc.next();
        System.out.println("계좌주  : ");
        owner = sc.next();
        System.out.println("초기 입금액 : ");
        balance = sc.nextInt();

        if(balance<0){ // 입금액이 음수일경우 
            System.out.println("입금액을 잘못 입력했습니다.");
            return;
        }

        for (int i = 0; i < accountArray.length; i++) { 
            if (accountArray[i] == null) {
                accountArray[i] = new Account(ano, owner, balance);
                System.out.println("계좌가 생성 되었습니다.");
                break;
            }
        }

    }

    private static void accountList() { //계좌 목록 메서드
        for (int i = 0; i < accountArray.length; i++) {
            if (accountArray[i] != null) {
                System.out.println("계좌 목록");
                System.out.println("계좌 번호 " + accountArray[i].getAno() + "계좌주 "+ accountArray[i].getOwner() +"잔액 "+ accountArray[i].getBalance());
            } else {
                break;
            }
        }
    }

    private static void deposit() { // 입금
        String ano;
        int balance;
        System.out.println("계좌번호 :");
        ano = sc.next();
        System.out.println("입금액 : ");
        balance = sc.nextInt();

        if(balance<0){ //입금액이 음수일 경우 
            System.out.println("입금액을 잘못 입력했습니다.");
            return;
        }

        Account num = findAccount(ano);
        if(num!=null){
               // 비어있지 않으면..
            num.setBalance(num.getBalance()+balance);
        }
        System.out.println("계좌 입금 완료");
    }

    private static void withdraw() { //출금
        String ano;
        int balance;

        System.out.println("계좌 번호  ; ");
        ano = sc.next();
        System.out.println("출금액 : ");
        balance = sc.nextInt();

        if(balance<0){ //출금액이 음수일경우 
            System.out.println("출금액을 잘못 입력했습니다.");
            return;
        }

        Account num = findAccount(ano);
        if(num!=null){ 
            if(num.getBalance()<balance){ // 출금액이 잔액보다 클경우
                System.out.println("잔액 부족");
            }
            else{
                num.setBalance(num.getBalance() - balance);
                System.out.println("계좌 출금완료");
            }
        }

    }

    private static Account findAccount(String ano) {
        for (int i = 0; i < accountArray.length; i++) {
            if (accountArray[i]!=null&&accountArray[i].getAno().equals(ano)) {
                return accountArray[i];
            }
        }
        return null;
    }
}
```

