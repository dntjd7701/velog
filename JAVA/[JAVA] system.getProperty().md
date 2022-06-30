## System.getProperty() 사용법


>  사용 목적

 - 자바 실행 시, 실행되는 곳의 정보를 얻어오거나 운영체제의 정보가 필요할 때
 
> 사용 결과 


- 실행 위치에 있는 파일을 읽어들일 수 있다. 
- 현재 위치를 알 수 있다. 
- 시스템의 정보를 가져올 수 있다. 

> 사용 법 

```java
String dir = System.getProperty("user.home");
System.out.println(dir);

// linux == /home/유저명
// macOS == //Users/유저명
```

---


#### Property 주요 검색어 

1. java
- java.version : Java 버전 
- java.vendor : Java 공급자 
- java.vendor.url : Java 공급자 주소 
-  <span style='background-color: #dcffe4; color: black'>java.home : Java를 설치한 디렉토리 위치 </span>
-  <span style='background-color: #dcffe4; color: black'>java.class.version : Java 클래스 경로</span>
- java.ext.dir : 확장기능의 클래스 경로
---
2. OS
- os.name : 운영체제 이름
- os.arch : 운영체제 아키텍처
- os.version : 운영체제 버전 정보 
---
3. user

- <span style='background-color: #dcffe4; color: black'>user.name : 사용자 계정</span>
- <span style='background-color: #dcffe4; color: black'>user.home : 사용자 홈 디렉토리</span>
- <span style='background-color: #dcffe4; color: black'>user.dir : 현재 디렉토리 </span>
 
---
4. 기타 
- file.separator : 파일 구분 문자
- path.separator : 경로 구분 문자 
- line.separator:  행 구분 문자 

---
#### property 확인 하기 

```java
import java.util.Iterator;
import java.util.Properties;

public class TEST {
    public static void main(String[] args) {
        Properties props = System.getProperties();
        Iterator<String> iterList = props.stringPropertyNames().iterator();

         while(iterList.hasNext()) {
             String key = iterList.next();
             String value = props.getProperty(key);
             System.out.println(key + "=" + value);
         }
    }
}

```

