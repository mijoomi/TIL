# JAVA 알고리즘 기초 ( 버블정렬 1 )

- 이웃한 두 요소의 대소관계를 비교하여 교환을 반복하는 정렬 

```java


public class Bul {

	
		public static void swap(int []a,int idx1,int idx2) { 
			int t = a[idx1];
			a[idx1]=a[idx2];
			a[idx2]=t;
		} //배열의 요소의 순서를 바꿔주는 메서드 
		public static void arr(int []a,int n) {
			for(int i=0;i<n-1;i++) {
				int exchg =0;  //요소가 교환될경우 카운트하는 변수
				for(int j =n-1;j>i;j--) {
					if(a[j-1]>a[j]) // 크기를 비교해서 크다면
						swap(a,j-1,j); //배열의 순서를 바꾸어주는 메서드 사용
					exchg++; //배열의 교환이있다면 카운트
				}
				if(exchg==0)break; //카운트 되지 않을경우 반복문 종료 
			}
		}
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
        
		System.out.println("요솟수 : ");
		int n = sc.nextInt();
		int []a = new int[n];
        
		Systm.out.println("요소를 입력하세요 :")
		for(int i =0;i<n;i++) {
			a[i] = sc.nextInt();		}
		
		arr(a,n); // 버블정렬메서드사용
		
		for(int i =0;i<n;i++) {
			System.out.println(a[i]);
		}

	}

}

```



# 버블정렬2


```java

import java.util.Scanner;

public class Bul {

		public static void swap(int []a,int idx1,int idx2) { 
			int t = a[idx1];
			a[idx1]=a[idx2];
			a[idx2]=t;
		}
		public static void arr(int []a,int n) {
			int k = 0;
			while(k<n-1){
				int list = n-1;
				for(int j = n-1; j>k;j--) 
					if(a[j-1]>a[j]) {
						swap(a,j-1,j);
						list = j;
					}
					k = list;	
			}
			}
		
	public static void main(String[] args) {
		Scanner sc = new Scanner(System.in);
		System.out.println("요솟수 : ");
		int n = sc.nextInt();
		int []a = new int[n];
		
		for(int i =0;i<n;i++) {
			a[i] = sc.nextInt();		}
		
		arr(a,n);
		
		for(int i =0;i<n;i++) {
			System.out.println(a[i]);
		}

	}

}

```
