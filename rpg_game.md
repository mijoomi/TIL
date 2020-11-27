# 콘솔창으로하는 rpg 게임만들기 !

> 상속 , 인터페이스를  연습하고싶은데 뭐가 좋을까 하다가 만들었는데 ,
>
>  효율성을 따지다 보니 막상 하나도 사용하지 않았다 .;;
>
> 너무 간단하게 만든거 같기도하고 . 좀더 세밀하게 만들어봐야겠다 .그럼 인터페이스랑 상속을 쓰지 않을까 ..?

```java
import java.util.Scanner;

public class Main {
    public static void main (String[] args) {


        Scanner sc = new Scanner(System.in);

        Ch_ex ex = new Ch_ex();

        while (true) {
            System.out.println("선택해주세요 .");
            System.out.println("----------------------");
            System.out.println("1. 캐릭터생성 2 . 현재 캐릭터 정보확인 3. 캐릭터 변경 4. 사냥 5.상점 6. 게임종료 ");
            int number = sc.nextInt();
            switch (number) {
                case 1:
                    ex.characters_new();
                    System.out.println("캐릭터가 생성되었습니다 .");
                    break;
                case 2:
                    ex.nowCharacters();
                    break;
                case 3:
                    System.out.println("캐릭터를 선택하세요.4");
                    ex.changeChareacters();
                    break;
                case 4:
                    System.out.println("입장할 사냥터를 선택하세요 .");
                    System.out.println("1.집 2.헤네세스 3. 버섯마을");
                    ex.monster_battle();
                    break;
                case 5:
                    ex.Store();
                    break;
                case 6 :
                    break;

            }

            if (number == 6){
                System.out.println("게임을 종료합니다.");
                break;
            }
        }
    }
}
```



```java
public class Ch_ex {

    int num = 0;
    Scanner sc = new Scanner(System.in);

    magic[] magics = new magic[5];
    Monster_lv1 monster_ln;


    public void characters_new ( ) { //캐릭터 생성 메서드
        for (int i = 0; i < 5; i++) {
            if (magics[i] == null) {
                int number = 0;
                System.out.println("닉네임을 입력하세요.");
                String name = sc.next();
                System.out.println("직업을 선택하세요 , ");
                System.out.println("1. 마법사 2. 전사");
                int job_num = sc.nextInt();
                if (job_num == 1) {
                    magics[i] = new magic(name, "마법사", 50, 70);
                } else if (job_num == 2) {
                    magics[i] = new magic(name, "전사", 70, 50);
                }
                break;
            }
        }
    }

    public boolean death ( ) {
        if (magics[num].gethp() <= 0) {
            System.out.println("잔여 hp 가 0입니다 .");
            System.out.println("전투를 중지합니다 .");
            return true;
        }
        return false;
    }

    public void changeChareacters ( ) { //캐릭터 변경
        for (int i = 0; i < 5; i++) {
            if (magics[i] != null) {
                System.out.println(i + 1 + "번째 캐릭터 " + magics[i].getname());
            }
            if (magics[i] == null) {
                break;
            }
        }
        System.out.println("캐릭터를 선택하세요");
        num = sc.nextInt() - 1;
    }


    public void nowCharacters ( ) { //현재 캐릭터 정보 확인
        if (magics[num] != null) {
            System.out.println("닉네임 : " + magics[num].getname());
            System.out.println("전직 : " + magics[num].getJob());
            System.out.println("현재 레벨 : " + magics[num].getlevel());
            System.out.println("현재 경험치 : " + magics[num].getlevelepoint());
            System.out.println("현재 HP : " + magics[num].gethp());
            System.out.println("현재 MP : " + magics[num].getmp());
            System.out.println("현재 잔고 : " + magics[num].getmoney());
        }
    }

    public void battle_massge ( ) {
        battle:
        while (true) {
            System.out.println("1. 전투시작  2. 물약 사용 3. 도망치기");
            int battle_num = sc.nextInt();
            switch (battle_num) {
                case 1:
                    System.out.println(magics[num].getname() + "의" + " 공격 ");
                    System.out.println(monster_ln.getName() + "에게" + magics[num].level_skil() + "의 데미지를 입혔다 ,,!");
                    System.out.println();
                    monster_ln.setHp(magics[num].level_skil());
                    if (monster_ln.getHp() <= 0) {
                        System.out.println(monster_ln.getName() + "을 물리쳤다!");
                        System.out.println();
                        magics[num].setlevelepoint(monster_ln.getLv_point());
                        magics[num].setmoney(monster_ln.getMoney());
                        System.out.println(monster_ln.getLv_point() + "경험치 와 " + monster_ln.getMoney() + " 머니를 획득하였다.");
                        break battle;
                    }
                    System.out.println(monster_ln.getName() + "의 잔여 hp" + monster_ln.getHp());
                    System.out.println(monster_ln.getName() + "이가 공격을 하였다.");
                    System.out.println();
                    magics[num].sethp(monster_ln.getDam());

                    if (death()) {
                        break battle;
                    }
                    System.out.println(magics[num].getname() + "의 잔여 hp" + magics[num].gethp());
                    break;

                case 2:
                    Recovery();
                    break;
                case 3:
                    break;
            }

            if (battle_num == 3) {
                break;
            }
        }
    }

    public void monster_battle ( ) {  //싸움터
        int battle_num = sc.nextInt();
        switch (battle_num) {
            case 1:
                monster_ln = new Monster_lv1("미정", 1, 15, 50, 25, 5);
                battle_massge();
                break;
            case 2:
                monster_ln = new Monster_lv1("버섯", 2, 25, 150, 35, 10);
                battle_massge();
                break;
            case 3:
                monster_ln = new Monster_lv1("슬라임", 3, 35, 250, 45, 20);
                battle_massge();
                break;
        }
    }

    //공격받았서 나 물약 머글랭 ..!
    public void Recovery ( ) {
        if (magics[num].getPotion() != 0) {
            System.out.println("현재 소지한 포션 갯수 : ");
            System.out.println(magics[num].getPotion() + "개 소유중");
            System.out.println("현재 소지한 메소" + magics[num].getmoney());
            System.out.println("사용할 포션 갯수를 입력하세요.");
            int i = sc.nextInt();
            if (magics[num].getPotion() >= i) {
                magics[num].setrecoveryhp(25 * i);
            }
            magics[num].addPotion(i);
            System.out.println("현재 hp :" + magics[num].gethp());
        } else {
            System.out.println("소지한 포션이 없습니다.");
        }
    }

    //상점
    public void Store ( ) {
        System.out.println("상점에 입장하였습니다.");
        System.out.println(" 1. 기본 포션  : 가격 25원");
        System.out.println(" hp 20 회복");
        System.out.println("구매할 수량을 입력해주세요 ");
        int j = sc.nextInt();
        if (magics[num].getmoney() < j * 25) {
            System.out.println("소지하신 메소가 부족합니다.");
        } else {
            int sum = j * 25;
            magics[num].setPotion(j);
            magics[num].addmoney(sum);
            System.out.println("구입이 완료 되었습니다.");
            System.out.println("현재메소는" + magics[num].getmoney());
            System.out.println("현재 소지한 물약 갯수는 " + magics[num].getPotion());
        }

    }


}

```

```java
public class magic{

    private  String nickname; //캐릭터 닉네임
    private int level;
    private int hp;
    private int mp;
    private int money;
    private int level_point;
    private String job;
    private int Potion;

    public magic(String name,String job,int hp,int mp){
        this.nickname =name; //캐릭터 닉네임
        this.level = 1;
        this.hp = hp;
        this.mp = mp;
        this.money = 0;
        this.level_point = 0;
        this.job = job;
        this.Potion=0;
    }


    public int getPotion ( ) {
        return Potion;
    }

    public String getJob ( ) {
        return "마법사";
    }


    public String getname ( ) {
        return nickname;
    }


    public int getlevel ( ) {
        return level;
    }


    public int getmoney ( ) {
        return money;
    }


    public int gethp ( ) {
        return hp;
    }


    public int getmp ( ) {
        return mp;
    }


    public int getlevelepoint ( ) {
        return level_point;
    }


    public void setLevel ( ) {
        if(getlevel()>=3){
            this.level = 3;
        }
    }



    public void setNickname (String nickname) {
        this.nickname = nickname;
    }


    public void setmoney (int money) {
        this.money = money;
    }


    public void sethp (int hp) {
        this.hp -= hp;
        if(this.hp<=0){
            this.hp =0;
        }
    }

    public void setrecoveryhp(int hp){
        this.hp += hp;
        if(this.hp>=100){
            this.hp=100;
        }
    }

    public void setPotion (int potion) {
        this.Potion += potion;
    }
    public void addPotion (int potion) {
        this.Potion -= potion;
    }

    public void setmp (int mp) {
        this.mp = mp;
    }


    public void setlevelepoint (int level_point) {
        this.level_point += level_point;
        if (this.level_point >= 100) {
            this.level += 1;
            this.level_point = 0;
        }
    }

    public void addmoney(int money){
        this.money -= money;

    }




    public int level_skil ( ) {
        if (getlevel() == 1) {
            return 5;
        } else if (getlevel() == 2) {
            return 10;
        } else if (getlevel() == 3) {
            return 15;
        }else{
            return -1;
        }
    }


}

```

```java
public class Monster_lv1{

    private String name; //몬스터// 닉네임
    private int level;
    private int hp;
    private int money;
    private int lv_point;
    private int dam;

    public Monster_lv1(String name , int level,int hp, int money,int lv_point,int dam){
        this.name = name;
        this.level = level;
        this.hp = hp;
        this.money=money;
        this.lv_point = lv_point;
        this.level = level;
        this.dam = dam;
    }

    public int getLevel ( ) {
        return level;
    }


    public int getHp ( ) {
        return hp;
    }


    public int getMoney ( ) {
        return money;
    }


    public String getName ( ) {
        return name;
    }


    public int getDam ( ) {
        return dam;
    }

    public int getLv_point ( ) {
        return lv_point;
    }


    public void setHp (int hp) {
        this.hp -= hp;
        if(hp<0){
            this.hp = 0;
        }
    }


}

```

