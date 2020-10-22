#

## 리플렉션 

- 리플렉션이란 ?

    - 리플렉션은 구체적인 클래스 타입을 알지 못해도, 그 클래스의 메소드, 타입, 변수들에 접근할 수 있도록 해주는 자바 API
    
#
접근법    
~~~java

 Class<Book> bookClass=Book.class;
 
 1. Book book=new Book();
 
 2. Class<? extends Book>aClass=book.getClass();
 
 3. Class<?>aClass1=Class.forName("클래스 경로") 

~~~
#
접근후에

~~~java

1. Arrays.stream(bookClass.getFeilds()).forEach(system.out::println);

2. Arrays.stream(bookClass.getDeclaredFeilds()).forEach(system.out::println);

3.Arrays.stream(bookClass.getDeclaredFeild("특정이름")).forEach(system.out::println);
~~~

1번은 public만 리턴

2번은 모든 값 리턴

3번은 해당되는 값 리턴
#
~~~java

 Class<Book> bookClass=Book.class;
 
 Book book=new Book();

 Arrays.stream(bookClass.getDeclaredFields()).forEach(f->{
 try{
    f.setAcessible(true);  // 접근시
    system.out.printf("%s,%s \n",f,f.get(book));
} catch(IllegalAccessException e){
    e.printStackTrace();
}
});
~~~

모든 필드와 필드의 값 출력
#

~~~java

 Arrays.stream(bookClass.getMethods()).forEach(system.out::println);

~~~

메소드, 오브젝트 상속도 출력

#
~~~java
 Arrays.stream(bookClass.getDeclaredConstructors()).forEach(system.out::println);
~~~

컨스트럭터 출력

#

~~~java
 System.out.println(MyBook.class.getSuperclass());
~~~

super 클래스

#

~~~java

Arrays.stream(MyBook.class.getInterfaces()).forEach(system.out::println);

~~~
인터페이스 










