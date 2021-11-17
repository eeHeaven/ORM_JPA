### QueryDsl 오류 수정
```java
> Task :compileQuerydsl FAILED java:13: error: cannot find symbol public class Guestbook extends BaseEntity { ^ symbol: class BaseEntity Note: Running JPAAnnotationProcessor 1 error FAILURE: Build failed with an exception. * What went wrong: Execution failed for task ':compileQuerydsl'. > java.lang.IllegalStateException: Found no type for BaseEntity
```
이런식으로 **cannot find symbol** 문제가 터졌다            
        
이 문제는 build.gradle 파일 하단에 이 코드를 추가하면 해결된다.                
문제의 원인은 Querydsl이 셋팅된 프로젝트에서 gradle build 시 QClass가 있는 build/generated/querydsl package를            
처음 만들면 문제 없이 빌드 되었지만, 그 이후 빌드 시 아래와 같은 에러를 뱉으며 빌드가 되지 않는 것이였다.               
```java
compileQuerydsl.doFirst { if(file(querydslDir).exists() ) delete(file(querydslDir)) }
```
