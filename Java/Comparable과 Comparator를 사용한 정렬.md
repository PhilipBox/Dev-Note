### Comparable과 Comparator를 사용한 정렬

Java에서 정렬을 하다보면 Comparator 또는 Comparable을 사용한다. 사람마다 사용하는 이유와 목적이 다르기도하고, 각자가 편하게 느끼는 것이 또 다르다. 나 역시 그때그때 다르게 사용할때도 있고 긴가민가하며 다시 찾아보는 경우가 많았기에 이번에 정리해보려고 한다.

### 1\. Comparable Interface

-   정렬수행시, 기본적으로 적용되는 정렬 기준이 되는 메서드를 정의해 놓은 인터페이스.

사용 방법 : Comparable 인터페이스를 implements 한 뒤, 내부에 있는 compareTo 메서드를 원하는 정렬 기준대로 구현하여 사용.

-   자바에서 제공되는 정렬이 가능한 클래스들은 모두 Comparable 인터페이스를 구현하고 있으며, 정렬시에 Comparable의 구현 내용에 맞춰 정렬이 수행된다.

Integer, Double 등의 클래스의 경우 비 내림차순(오름차순과 유사), String 클래스의 경우 사전순으로 정렬되게 구현되어 있다.

-   package: java.util.Comparator

### 2\. Comparator class

-   정렬 가능한 클래스(=Comparable이 구현된 클래스)들의 기본 정렬 기준과는 다른 방식으로 정렬하고 싶을 때 사용하는 클래스.

사용 방법: Comparator 클래스를 생성하여, 내부에 compare메서드를 원하는 정렬 기준대로 구현하여 사용.

-   주로 익명클래스(new Comparator(){ ... })로 사용되며, 기본적으로 오름차순이 정렬 기준인 것을 내림차순으로 정렬하는 등의 용도로 사용된다.

이 Interface를 구현한 Class는 **정렬 규칙** 그 자체를 의미하며, 기본 정렬 규칙과는 다르게 사용자가 원하는대로 정렬순서를 지정하고 싶을 때 사용한다.

-   기본 정렬 방식인 오름차순 정렬을 내림차순으로 정렬할 때 많이 사용!
-   package : java.util.Comparator

#### Summary

Comparable : 클래스의 기본 정렬 기준을 설정하는 인터페이스  
Comparator : 기본 정렬 기준과는 다르게 정렬하고 싶을 때 사용하는 클래스

---

### Comparable

자료형 배열 및 리스트는 Arrays.sort/Collections.sort로 오름차순 정렬이 바로 가능함.  
오름차순이 목적이라면 위 메소드를 사용하는 것이 빠르고 간편.  
Class를 정의했다면, 단순히 위 메소드를 사용하는 것으로는 불가능함. Class에 implements Comparable을 해서 CompareTo를 Override해줘야 함!  
오름차순으로 표현한다면 파라미터의 타입에 따라서 간편하게 표현이 가능하다.  
예를들어 **return Integer.compare(id, obj.id);** 형태나 **return Double.compare(score, obj.score);** 등의 표현처럼.

내림차순으로 표현하려면 다음과 같이 구현해주면 가능하다.

```
// id는 내림차순. id가 같다면 성적으로 오름차순.
        @Override
        public int compareTo(Student s) {
            if(id > s.id) return -1;
            else if( id < s.id) return 1;
            else {
                return Double.compare(score, s.score);
            }        
```