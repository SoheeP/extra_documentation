# 디자인패턴

### 싱글턴(Singleton Pattern)

<b>다크모드를 적용한다고 생각해보자.</b> 다크모드 설정을 했다면, 다른 화면을 가더라도 그 화면이 적용되어야 하는데 각 컴포넌트마다 설정클래스의 인스턴스를 새로 생성한다면...? 아마 적용되지 않을 것이다. (기존에 생성한 설정 클래스와 다른 곳에서 또 생성한 클래스는 엄연히 다르니까)

이런 문제를 해결하기 위한 방법!

1. 클래스 내에 `static`을 선언한다.
   - `static`으로 선언되지 않은 변수(`private`나 `public`)들은 생성할 때 마다 동적 메모리 공간에 생성하게 된다.
   - `static`으로 선언된 변수들은 클래스가 생성되었을 때 정적 메모리 공간에 단 하나만 생성된다.

```java
public class Settings {
    private Settings () {};
    private static Settings settings = null; //초기에는 null로 설정해준다
    public static Settings getSettings () { // getSettings라는 정적 메서드 생성
        if(settings == null){
            settings = new Settings(); //아무도 실행하지 않았다면 settings 변수에 자기 자신을 넣어준다
        }
        return settings; // 하지만 누군가 실행해서 settings가 null이 아니면, 이미 생성된 Settings를 반환
    }
    
    private boolean darkMode = false;
    private int fontSize = 13;
    
    public boolean getDarkMode(){return darkMode};
    public int fontSize = 13;
    
    public void setDarkMode (boolean _darkMode){
        darkMode = _darkMode; // 누군가 이 메서드로 darkMode를 설정하면, 정적 메서드로 getSetting로 설정을 불러올 때 이 darkMode를 반영된 Settings가 적용된다!
    }
    public void setFontSize (int _fontSize){
        fontSize = _fontSize;
    }
}
```

싱글턴의 활용은 `interface`의 사용이나, lazy loading 등에서 자주 사용될 수 있다.

단, 멀티쓰레드 환경에서는 오류가 발생할 소지가 있기 때문에 완벽한 방법은 아니다.

### 전략패턴(Strategy Pattern)

<b>몇가지 조건검색모드가 있는 검색창을 만든다고 가정해보자.</b> 모드를 선택 후 검색하게 되면 그 모드에 맞게 검색될 수 있는 환경을 구축해야 한다. 즉, 프로그램 실행 중 모드가 바뀔 때 마다 검색이 이루어지는 방식(전략)이 수정된다.

각 모드에 대한 모듈을 만들고, 모듈을 갈아끼우는 방식으로 진행된다. 그러기 위해서 `interface`를 활용한다.

```java
package strategy.after;

interface SearchStrategy {
    public void search(); // search라는 함수가 일을 하는 방식까지 정하진 않고, search를 할 줄 안다만 선언
}

class SearchStrategyAll implements SearchStrategy {
    public void search(){
        System.out.printIn("Search All");
        // 전체검색하는 코드가 아래에 쭉쭉...
    }
}
class SearchStrategyImage implements SearchStrategy {
    public void search(){
        System.out.printIn("Search Image");
        // 이미지검색하는 코드가 아래에 쭉쭉...
    }
}
class SearchStrategyNews implements SearchStrategy {
    public void search(){
        System.out.printIn("Search News");
        // sbtm검색하는 코드가 아래에 쭉쭉...
    }
}
class SearchStrategyMap implements SearchStrategy {
    public void search(){
        System.out.printIn("Search Map");
        // 지도검색하는 코드가 아래에 쭉쭉...
    }
}
```

새로운 방식이 추가되더라도 클래스 내부에 선언한 메서드를 일일히 추가하고, 수정하기보다는 `SearchStrategy`인터페이스를 구현한 새로운 클래스를 생성하며 사용한다. :arrow_forward: 독립적이고, 상호 교체 가능하게 만들어야 한다!

### 스테이트 패턴 (State Pattern)

겉보기에는 전략패턴과 코드가 상당히 유사하지만, 아래와 같은 차이점이 있다.

* 전략패턴: <u>동일한 틀</u> 안에서 방식(모듈)을 교체해야 할 때 (ex: 검색창이라는 하나의 틀 안에서 모드가 바뀔 때)
* 스테이트패턴: <u>특정 상태</u>마다 다르게 할 일, 또는 그 상태에서 해야 할 일을 하나하나 모듈이 필요할 때 (ex: TV의 꺼진 상태/켜진 상태에 따라 TV가 해야 할 일이 다를 때)

```java
package state;

public interface ModeState {
  public void toggle (ModeSwitch modeSwitch);
}

class ModeStateLight implements ModeState {
  public void toggle (ModeSwitch modeSwitch) {
    System.out.println("FROM LIGHT TO DARK");
    // 화면을 어둡게 하는 코드
    // ..
    // ..
    modeSwitch.setState(new ModeStateDark()); //상태를 변경해준다.
  }
}

class ModeStateDark implements ModeState {
  public void toggle (ModeSwitch modeSwitch) {
    System.out.println("FROM DARK TO LIGHT");
    // 화면을 밝게 하는 코드
    // ..
    // ..
    modeSwitch.setState(new ModeStateLight());

  }
}
```



출처: [얄팍한 코딩사전](https://www.yalco.kr/29_oodp_1/)

