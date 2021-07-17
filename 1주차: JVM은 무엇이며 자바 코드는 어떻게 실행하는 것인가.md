# 목표
자바 소스 파일(.java)을 JVM으로 실행하는 과정 이해하기

# 학습할 것
### 1. JVM이란?
> #### " Write Once, Run Anywhere "

자바가상머신(Java Virtual Machine)으로서 어떤 운영체제나 기기에서든 모두 실행할 수 있게 해주기 위함이 목적이다.  
컴파일 플랫폼과 타겟 플랫폼이 다른 경우 실행할 수 없는 환경을 해결하기 위해 바이트코드(.class)를 타겟 플랫폼에 상관없이 작동할 수 있도록 해주었다.  
그렇기 때문에 자바 프로그램을 실행하기 위해서는 JVM이 반드시 설치되어 있어야 한다.  
그러나, Java가 OS에 구애받지는 않지만 JVM은 OS에 종속적이기 때문에 OS에 맞는 JVM을 설치해 주어야 한다.  
다른 언어(C, C++ 등)는 같은 문제를 해결하기 위해 크로스 컴파일러를 도입하여 문제를 해결했다.


### 2. 컴파일 및 실행방법

![컴파일과정](https://media.vlpt.us/images/woo00oo/post/b2e894dd-83cf-456b-91b7-15e02611ac88/%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202021-01-01%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%205.39.12.png)

1. file.java 파일을 개발자가 작성한다.
2. `javac file.java` 명령어를 통해 자바 컴파일러를 실행해 자바 바이트 코드 파일(.class)을 생성한다.
3. `java file` 명령어를 실행하면 Class Loader를 통해 class파일을 JVM으로 로딩하고 Excution Engine을 통해 해석한다.
4. Runtime Data Area에 해석된 바이트 코드가 배치되어 실행된다.


### 3. 바이트코드란?
![자바 컴파일러와 인터프리터](https://mblogthumb-phinf.pstatic.net/MjAxODAzMTNfMjU1/MDAxNTIwOTM2MDg5NzU5.FC9iwVzwVFoJ7L3d7R1MF1YBW8BMwQV9DLS3wCNvSJsg.OEmYIspBpTdYGKlQYIPsfThUhCdxdcS_rJnTuU-CTfkg.PNG.ehcibear314/%EC%9E%90%EB%B0%94%EC%BB%B4%ED%8C%8C%EC%9D%BC%EB%9F%AC%EC%99%80%EC%9E%90%EB%B0%94%EC%9D%B8%ED%84%B0%ED%94%84%EB%A6%AC%ED%84%B0.png?type=w800)

가상머신이 java코드를 그대로 사용하기보다는 '가상머신이 인식하기 쉬운 코드'로의 변환이 필요하다.  
그렇기 때문에 바이트코드로 변환하는 과정이 필요하다. 자바에서는 자바코드를 .class 코드로 변환하게 되는데 이 결과물을 바이트코드라고 한다.  
이 바이트코드는 인터프리터 언어의 형태를 하고 있어, 인터프리터를 통해 실행해준다.

### 4. JIT 컴파일러란? 그리고 동작방식


### 5. JVM 구성 요소
![JVM구성](https://github.com/boonboonE/LearnJava/blob/main/images/JVM%E1%84%80%E1%85%AE%E1%84%8C%E1%85%A9.png)


### 5. JDK와 JRE의 차이
