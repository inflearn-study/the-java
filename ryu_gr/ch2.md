#

## section 2

## 코드 커버리지란?

코드 커버리지(Code Coverage)는 소프트웨어의 테스트를 논할 때 

얼마나 테스트가 충분한가를 나타내는 지표중 하나다.

말 그대로 코드가 얼마나 커버되었는가이다.
 
 소프트웨어 테스트를 진행했을 때 코드 자체가 얼마나 실행되었냐는 것이다.

// 출처위키

바이트 코드 읽어서 코드 지나갈때 카운팅 지나간 통로 표시 

pom.xml에 jacco 플러그인 추가

`<plugin>
 <groupId>org.jacoco</groupId>
 <artifactId>jacoco-maven-plugin</artifactId>
 <version>0.8.4</version>
 <executions>
 <execution>
 <goals>
 <goal>prepare-agent</goal>
 </goals>
 </execution>
 <execution>
 <id>report</id>
 <phase>prepare-package</phase>
 <goals>
 <goal>report</goal>
 </goals>
 </execution>
 </executions>
 </plugin>
`

추가후 빌드

`mvn clean verify`

커버리지 만족평가 현재 미니멈 50%

조절 통해서 커버리지 평가 상향 하향 가능

`<execution>
 <id>jacoco-check</id>
 <goals>
 <goal>check</goal>
 </goals>
 <configuration>
 <rules>
 <rule>
 <element>PACKAGE</element>
 <limits>
 <limit>
 <counter>LINE</counter>
 <value>COVEREDRATIO</value>
 <minimum>0.50</minimum>
 </limit>
 </limits>
 </rule>
 </rules>
 </configuration>
 </execution>`

# 
## 바이트 코드 조작

ByteBuddy로 

Moja.java

`public class Moja {
 public String pullOut() {
 return "";
 }
 }
`

Masulsa.java

`public class Masulsa {
 public static void main(String[] args) {
 System.out.println(new Moja().pullOut());
 }
 }
`

아무것도 안나오는게 정상이지만 바이트코드 조작으로 변경 가능

ByteBuddy pom.xml 에 dependency 추가

`new ByteBuddy().redefine(Moja.class)
 .method(named("pullOut")).intercept(FixedValue.value("Rabbit!")).
 make().saveIn(new File("바이트코드 경로"))   
`

ByteBuddy 로 읽어와서 pullout 이라는 메소드의 값 가로채서 래빗 넣어줌

#
## javaagent 

MasulsaJavaAgent.java

새로 만든 파일

`public class MasulsaAgent {
 public static void premain(String agentArgs, Instrumentation inst) {
 new AgentBuilder.Default()
 .type(ElementMatchers.any())
 .transform((builder, typeDescription, classLoader, javaModule) ->
 builder.method(named("pullOut")).intercept(FixedValue.value("Rabbit!"))).installOn(inst);
 }
 }`
 
 패키징을 해주고
 
 결과창에 jar 파일 path 복사

vm 옵션에서 javaagent 로 변경하여 사용

javaagent :클래스 파일 자체 변경 대신 클래스 로딩시 적용

#
## 바이트코드 조작 예

- 프로그램 분석

    - 코드에서 버그 찾는 툴
    
    - 코드 복잡도 계산
    
- 클래스 파일 생성
    - 프록시
    
    - 특정 api 호출 접근 제한
    
    - 스칼라 같은 언어의 컴파일러
    
    - 프로파일러: 사용하는 성능 분석 툴
        
- spring에서도 asm 사용하여 컴포넌트 스캔     
    