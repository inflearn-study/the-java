#
## 롬복

롬복이란 ?

롬복(Lombok)은 Java에서 반복적으로 작성되는 

getters/setters나 equals, hashCode, toString 

또는 생성자 관련 코드들을 간결하게 만들어주는 라이브러리다. 

동작 원리는 컴파일 시에 애노테이션 프로세서 사용하여 조작

@Retention :어떤시점까지 어노테이션이 영향 미칠지 결정

@AutoService :  애노테이션을 이용하여 자동으로 애노테이션 프로세서를 

컴파일러 등록하는 메타데이터 파일을 생성해준다.

