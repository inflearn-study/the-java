# 자바,jvm,jdk 그리고 jre

## section 1


![jdk](https://user-images.githubusercontent.com/38341106/95930175-d0c08980-0e00-11eb-9c9a-38b29974dff9.png)



- 자바  
    - 프로그래밍 언어    
    
    - jdk에 들어있는 자바 컴파일러 사용하여 바이트코드(.class)로 컴파일 
    
    - jdk 11 유료 but open jdk , 타 플랫폼 jdk 무료
    
- jvm
    - 가상 머신
    
    - 머신이 이해할수 있도록 os에 의존적
    
    - 바이트 코드를 실행하는 표준, 구현체
    
    - 특정 플랫폼에 종속적
    
- jdk
    - jre + jdk
    
    - 자바 11부터는 jdk만 제공 jre제공 x
    
- jre
    - jvm+library
    
    - 자바 애플리케이션을 실행이 목적
    
    - 자바 실행에 필요한것만 

#
##  section 2 

- jvm 구조


      
  ![jvm](https://user-images.githubusercontent.com/38341106/95929948-3bbd9080-0e00-11eb-965e-06cf9eb7f133.png)


    - 클래스 로더    
        - 로딩 : 클래스 읽어오는 과정
        
        - 링크 :레퍼런스를 연결하는 과정
        
        - 초기화 :static 값들 초기화 및 변수에 할당
    
    - 메모리    
        - 스택 : 쓰레드 각자 런타임 스택 만든다.  
        
        - PC (Program Counter) : 현재 실행할 스택 프레임 가르킴
        
        - 네이티브 메소드 스택 : 네이티브 메소드 호출시 사용 별도의 메소드 스택
        
        - 힙 : 객체 저장 (인스턴스 전부)
        
        - 메소드 :클래스 이름,부모 클래스 이름,메소드 변수가 저장.공유 자원
        
        - jni (java native interface) :jvm이 운영체제의 모든 기능을 담지 못해 운영체제 구현 언어로 고유 기능 만든다
                즉 보통 c,c++로 되어진 함수를 java 메서드와 연결 -> java 메소드 호출시 c,c++ 함수 실행
                
    - 실행 엔진 
    
        - 인터프리터: 바이트 코드 한줄씩 실행
        
        - JIT 컴파일러 :반복되는 코드 발견시 네이티브 코드로 바꿈, 속도 향상
        
        - GC(Garbage Collector): 더이상 사용하지 않는 메모리 자동 해제
        
            * stop the world: GC 실행 위해 jvm 애플리케이션이 실행을 멈추는것. GC실행시 GC 쓰레드 제외 모든 스레드 작업 멈춤
            
            * GC튜닝 : stop the world 시간 줄이는것
            
    
    정리 : 클래스 로더가 읽어와 메모리에 배치 실행엔진 실행      
#    
##  section 3    

![클래스 로더](https://user-images.githubusercontent.com/38341106/96198845-de0c7e00-0f90-11eb-8655-fed2863bbc2c.png)

- 로딩
    - 3개의 계층 구조 
    - 부모부터 읽어오는데 다 못읽게 된다면 ClassNotFoundException
    - 클래스 로더가 .class 파일 읽고 메소드 영역에 저장 이때 바이너리 데이터(클래스,인터페이스,메소드,변수)
    - 로딩이 끝나면 클래스 타입의 class 객체 생성하여 힙 영역에 저장
    
    
- 링크
    - Verify : .class 파일 형식 유효 체크
    - Prepare : 클래스 변수와 기본값에 필요한 메모리
    - Resolve : 심볼릭 메모리 레퍼런스 메소드 영역에 있는 실제 레퍼런스로 교체(옵션,그럴수도 있고 아닐수도있는)

- 초기화
    - static 변수 값 할당

컴파일 -> 바이트 


코드 -> jvm이 실행