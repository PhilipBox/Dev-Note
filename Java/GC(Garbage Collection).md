### GC(Garbage Collection)

-   GC란, 이미 할당된 메모리에서 더 이상 사용하지 않는 메모리를 해제하는 행동.
-   사용되지 않는 메모리의 대상은 Heap과 Method Area에서 사용되지 않는 Object를 의미.
-   소스상에서 close()는 Object 사용중지 의사표현일 뿐 Object를 메모리에서 삭제하겠다는 의미가 아님.
-   System.GC()를 명시적으로 호출할 수 있지만, Full GC를 수행시키는 메소드이기 때문에 Stop-the-world 시간이 길고 무거운 작업이며 또한 반드시 즉시 수행한다는 보장도 없는 메소드이기에 사용을 지양.

### GC 작동원리

-   Heap을 3개의 영역으로 나누어 관리.
-   young 영역(Young Generation): 새롭게 생성한 객체의 대부분이 위치해있음. 가득차게 되면, Minor garbage collection이 일어남.
    -   Minor GC : young 영역에서 객체가 사라지는 것.
-   old 영역(Old Generation) : 접근 불가능한 상태가 되지 않아, young에서 살아남은 객체가 복사되어 짐. 대부분 Young 영역보다 크게 할당하며, 크기가 큰 만큼 Young 영역보다 GC는 적게 발생함.
    -   Major GC(혹은 Full GC) : Old 영역에서 객체가 사라지는 것.
-   permanent 영역(Method Area) : 객체나 억류(intern)된 문자열 정보를 저장하는 곳이며, Old 영역에서 살아남은 객체가 영원히 남아 있는 곳은 절대 아님. 이 영역에서 GC가 발생할 수도 있는데, 여기서 GC가 발생해도 Major GC의 횟수에 포함됨.
    -   JVM이 클래스들과 메소드들을 설명하기 위해 필요한 메타데이터들을 포함하고 있다. GC가 일어나면, 구역에 남은 객체들을 compact해서 보관한다.

이미지 참고 : https://philipbox.tistory.com/68?category=867422


GC영역 및 데이터 흐름도

#### STW(Stop-The-World)

-   GC(Garbage Collection)을 실행하기 위해 JVM이 애플리케이션 실행을 멈추는 것.
-   Minor GC, Major GC 모두 STW event가 발생.
-   stop-the-world가 발생하면 GC를 실행하는 쓰레드를 제외한 나머지 쓰레드는 모두 작업을 멈춤.
-   GC 작업을 완료한 이후에야 중단했던 작업을 다시 시작.
-   어떤 GC 알고리즘을 사용하더라도 stop-the-world는 발생함. GC 튜닝이란 이 stop-the-world 시간을 줄이는 것.

이미지 및 자료 참고

-   [http://java.sun.com/j2se/reference/whitepapers/memorymanagement\_whitepaper.pdf](http://java.sun.com/j2se/reference/whitepapers/memorymanagement_whitepaper.pdf)
-   [https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html](https://www.oracle.com/webfolder/technetwork/tutorials/obe/java/gc01/index.html)