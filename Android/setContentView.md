### setContentView

Class에서 상속하는 AppCompatActivity에는 화면에 필요한 기능(method)가 들어있는데, 그 중 하나가 setContentView 이다.

-   화면에 표시할 XML 레이아웃을 지정하거나 화면에 표시할 뷰 객체를 지정하는 역할.
-   이 메서드로 전달할 수 있는 파라미터는 뷰 객체 또는 XML 레이아웃이 정의된 리소스가 될 수 있음.

#### setContentView의 2가지 역할

1.  화면에 나타낼 뷰를 지정
2.  레이아웃 내용을 메모리에 객체화

두 번째 역할에서의, XML 레이아웃의 내용을 메모리에 객체화 되는 과정을 **'인플레이션(Inflation)'** 이라고 함.

-   XML 레이아웃은 앱이 실행되는 시점에 메모리에 객체화.
-   즉, XML 레이아웃 파일에 **Button태그를 정의해도 앱은 자신이 실행되기 전까지 버튼이 있는지 모름.**
-   setContentView() 메서드가 호출되기 전에 접근하려고 한다면, Null Pointer Exception이 발생하게 된다.
-   메모리에 객체화되기 전에 Button 객체를 참조하려고 했기 때문.  
    
    

#### 인플레이터(Inflater)

setContentView() 메서드는 **액티비티의 화면 전체(메인 레이아웃)** 를 설정하는 역할만은 수행한다.  
즉, setContentView() 메서드로는 부분화면(부분 레이아웃)을 메모리에 객체화할 수 는 없다.  
부분 화면을 메모리에 객체화하려면 **인플레이터** 를 사용해야 한다.  

안드로이드는 이를 위해 시스템 서비스로 **LayoutInflater** 라는 클래스를 제공한다. 그런데 LayoutInflater 클래스는 시스템 서비스로 제공하는 클래스이므로 다음 **getSystemService()** 메서드를 이용하여 LayoutInflater 객체를 참조한 후 사용해야 한다.