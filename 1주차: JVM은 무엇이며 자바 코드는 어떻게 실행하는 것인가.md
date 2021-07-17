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
JIT 컴파일(just-in-time compilation) 또는 동적 번역(dynamic translation)은 프로그램을 실제 실행하는 시점에 기계어로 번역하는 컴파일 기법이다. 

JIT 컴파일러는 기존 인터프리터 방식으로 동작하는 Java의 한계를 보완한 기술이다.
인터프리터 방식은 코드를 한줄씩 읽어서 기계어로 번역해 실행하는 구조였는데, 이런 구조는 실행속도를 늦추는 원인이 되었다.  

JIT 컴파일러는 실행 중에 Java 애플리케이션에서 자주 사용되는 바이트 코드 순서에 대해 동적으로 시스템 코드를 생성한다.  
가장 자주 실행되는 코드 블록, 메서드 또는 메서드의 일부, 특히 반복문을 모니터링해서 네이티브 코드로 컴파일 시키는데 이렇게하면 더 빠른 실행속도를 보일 수 있다.

다만, 컴파일 과정에서는 추가적인 단계를 요구하기 때문에 더 많은 컴파일 자원을 요구해서 느려질 수는 있다.
그러나 네이티브 코드로 이 과정을 거쳐 네이티브 코드로 컴파일 되었을 때의 장점이 더 크기 때문에 JIT을 기본적으로 사용한다.(실행하지 않도록 전환할 수도 있지만 권장하지 않음)

JIT 컴파일러는 C1 (클라이언트 컴파일러), C2(서버 컴파일러)로 구분된다.
C1은 빠르게 실행되지만 덜 최적화 된 코드를 생성하고, C2는 실행 시간이 좀 더 걸리지만 더 최적화된 코드를 생성한다.

오늘날의 JVM은 두 가지를 모두 사용하며, 처음엔 C1을 사용하지만, 호출의 수가 증가하게 되면, C2를 사용하는데 이를 tiered compilation이라고 한다.

### 5. JVM 구성 요소
![JVM구성](https://github.com/boonboonE/LearnJava/blob/main/images/JVM%E1%84%80%E1%85%AE%E1%84%8C%E1%85%A9.png)

#### * 가비지 컬렉터(Garbage Collector)
C언어의 경우, 메모리 관리를 개발자가 직접 해 주어야 했는데 JVM에서는 가비지컬렉터를 이용해 더 이상 사용되지 않는 메모리를 회수하는 방식으로 직접 관리할 필요가 없어졌다.

#### * 실행 엔진(Execution Engine)
클래스 로더에 붙어있는 클래스를 읽으면서 static이 있는지 판단합니다. 이때, static이 없다면 그대로 종료된다.

#### * 클래스 로더(Class Loader)
컴파일러가 만들어낸 .class 파일을 로딩해오는 것을 담당한다. 이 부분에는 3가지 기본 클래스 로더가 있다.
![클래스 로더](https://i.imgur.com/cs5Qyoe.png)
###### - Bootstrap ClassLoaer
  1. 부트스트랩 클래스로더는 3가지 기본 클래스로더 중 최상위 클래스인데, `$JAVA_HOME/jre/lib/rt.jar` 에서 `rt.jar`에 있는 핵심 클래스 파일을 로딩한다.
  2. Native C로 구현되어있고, Primordial ClassLoader라고도 불린다.
###### - Extension ClassLoader(->java9, Platform ClassLoader)
  1. 환경변수로 지정된 폴더에 있는 확장 클래스 파일을 로딩한다.
  2. Java로 구현되어 있고, `sun.misc.Launcher` 클래스 내에 static 클래스로 구현되어 있으며, `URLClassLoader`를 상속하고 있다.
###### - Application ClassLoader(->java9, System ClassLoader)
  1. 애플리케이션 클래스로더는 `-classpath(또는 -cp)`나 JAR 파일 안에 있는 Manifest 파일의 Class-Path 속성값으로 지정된 폴더에 있는 클래스를 로딩한다.
  2. 익스텐션 클래스로더와 마찬가지로 Java로 구현되어 있으며, `sun.misc.Launcher` 클래스 안에 static 클래스로 구현되어 있으며, `URLClassLoader`를 상속하고 있다.
  3. 개발자가 애플리케이션 구동을 위해 직접 작성한 대부분의 클래스는 이 애플리케이션 클래스로더에 의해 로딩된다.

###### - 클래스로더의 3가지 원칙
  1. 위임 원칙: 클래스로딩 작업을 상위 클래스로더에 위임한다.  
  2. 가시 범위 원칙: 하위 클래스로더는 상위 클래스로더가 로딩한 클래스를 볼 수 있지만, 상위 클래스로더는 하위 클래스로더가 로딩한 클래스를 볼 수 없다.
  3. 유일성 원칙: 하위 클래스로더는 상위 클래스로더가 로딩한 클래스를 다시 로딩하지 않게 해서 로딩된 클래스의 유일성을 보장한다.

#### * 런타임 데이터 영역(Runtime Data Area)




### 5. JDK와 JRE의 차이
