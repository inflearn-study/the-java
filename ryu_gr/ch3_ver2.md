# 

## 애노테이션과 리플렉션

애노테이션도 조회가능

~~~java

Arrays.stream(MyBook.class.getAnnotations()).forEach(system.out::println);

~~~
하지만 @Retention 애노테이션 추가시 사용가능

- @Target 애노테이션은 사용가능한 타입 지정(ex. 생성자는 안됨)

- @Inherited 애노테이션은 애노테이션이 자손 클래스에도 상속되도록

#
인스턴스 생성시에

~~~java
Class<?> bookClass=Class.forName("?");

Constructor<?>constructor=bookClass.getConstructor(null); //인스턴스 생성시 constructor 부터

constructor.newInstance();  

~~~

get,set

~~~java

Field a= Book.class.getDeclaredField("A");  //A를 가져올때

system.out.println(a.get(null));            //get

a.set(null,"set 값 넣어주기")
~~~

Method

~~~java

Method sum1=Book.class.getDeclareMethod("sum",매개변수 자리,매개변수 자리);

int invoke=(int) sum1.invoke(book,값1,값2)

~~~

## 정리

 - 클래스 인스턴스, 필드값 세팅, 메소드 실행
 
 - 스프링
 
    - 의존성 주입시

    - mvc 뷰에서 넘어오는 데이터 객체에 바인딩시
    
 - 잘못 사용시 성능 이슈 야기할수 있음.
 
 - 런타임 시에만 발생하는 문제 만들 가능성 (컴파일시 확인 되지 않음)  




