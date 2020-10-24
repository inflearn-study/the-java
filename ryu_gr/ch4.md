#

## 프록시

스프링 AOP 기반 동작

스프링 JPA  RepositoryFactorySuppor 에서
 
프록시 패턴 

#
<img src = "https://user-images.githubusercontent.com/38341106/97080007-46afc680-1633-11eb-80ea-4ca52a256c5d.png" width="70%">

#
    - 리얼 서브젝트 깔끔하게 하기위해. 

    - 객체지향 방향성에 맞게

다이나믹 프록시 : 런타임에 특정 인터페이스 구현하는 클래스,인스턴스 만드는 기술

인스턴스 시

    - InvocationHandler() :프록시에 메소드 호출 처리 어떻게 할것에 대한 설명
    
클래스 시
    
    - CGlib
    
    - ByteBuddy

인스턴스에 비해 단점

    - 상속 받아야하므로 상속 받지 못하면 불가능
    
    - private 생성자만 있다면 불가
    
    - 가능한 인스턴스 사용
    



    