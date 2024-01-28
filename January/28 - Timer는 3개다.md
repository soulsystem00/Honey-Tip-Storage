# Timer는 3개다

C# 에서 Timer라는 클래스가 존재하는데</br>
특이하게 같은 이름의 같은 기능을 하는 클래스가 3개 존재함</br>
대충 기능은 타이머를 설정하고 함수를 등록하면</br>
설정한 시간에 한번씩 등록한 함수를 실행시켜주는 역할임</br>
</br>
각각 속해있는 네임스페이스가 다른데 아래와 같음</br>
```
System.Windows.Forms.Timer;
System.Threading.Timer;
System.Timers.Timer;
```

같은 기능을 하는 애들인데 왜 굳이 3개로 분리시켜놓았을까 하는 궁금증이 있었는데</br>
굳이 찾아보진 않고 있다가</br>
이번에 오토 캡쳐 프로그램 만들다가 궁금해져서 찾아보게 되었음</br>
</br>
일단 3개가 사용방법이 다름</br>
먼저 Form Timer 사용법임</br>
```
System.Windows.Forms.Tiemr timer = new System.Windows.Forms.Timer();
timer.Interval = 1000;
timer.Tick += new EventHandler(func);
timer.Start();
timer.Stop();
```

인터벌 설정을 해주고 Tick이라는 곳에 이벤트를 등록해주는 식으로 사용을 함</br>
</br>
그 다음으로 쓰레드 타이머 사용법임</br>
```
System.Threading Timer timer = new System.Threading.Timer(func);
timer.Change(0,1000);
timer.Change(System.Threading.Timeout.Infinite, System.Threading.Timeout.Infinite);
```

</br>
마지막으로 그냥 타이머 사용법임</br>

```
System.Timers.Timer timer = new System.Timers.Timer();

timer.Interval = 1000;
timer.Elapsed += new System.Timers.ElapsedEventHandler(func);
timer.Start();
timer.Stop();
```

</br>
</br>
보면 대충 사용방법이나 효과는 비슷함</br>
시간 설정해주고</br>
이벤트 등록하고</br>
시작하고 스탑하고</br>
결론적으로는 주기적으로 함수 실행되고</br>
</br>
그럼에도 불구하고 왜 3개로 나누었냐 라는 건데</br>
</br>
일단 윈폼 타이머 같은 경우에는 크로스 쓰레드 문제가 발생하지 않는다.</br>
나머지 2개는 크로스 쓰레드 문제가 발생한다.</br>
그렇기 때문에 나머지 2개 타이머에서 UI 쪽에 접근을 하려고 한다면</br>
따로 처리를 해주어야 한다.</br>
</br>
왜 그러냐 하면</br>
윈폼 타이머는 독립적인 쓰레드에서 돌아가는 것이 아니라</br>
UI 쓰레드에서 돌아가기 때문이다.</br>
그렇기 때문에 UI 크로스 쓰레드 오류가 발생하지 않지만</br>
멀티쓰레드 환경이라고 볼 수도 없을 것이다.</br>
</br>
쓰레드 타이머 같은 경우에는 멀티 쓰레드에서 만 가능하고</br>
그냥 타이머는 지정이 가능하다고 한다.</br>
</br>
그렇기 때문에 크로스 쓰레드를 피하고 싶으면 윈폼 타이머를 사용하면 되는데</br>
만약에 해당 타이머에서 무거운 작업이 이뤄진다면</br>
윈폼 프로그램 자체가 멈출 것이다.</br>
</br>
이외에 다른 여러가지 차이점들이 있다고 한다.</br>
이를테면 윈폼 타이머는 윈폼 환경에서만 쓸수 있다던가</br>
무한이라는 시간을 지정할 수 있는지 없는지에 대한 차이라던가</br>
기타 등등의 차이가 있는 것 같다.</br>
</br>
</br>
그런데 일단 가장 큰 차이는 크로스 쓰레드 인 것 같다.</br>
왜냐하면 나머지 차이 같은 경우엔</br>
해당 기능을 사용하지 않는이상 체감하기 힘든 것 같기 때문이다.</br>
</br>
</br>
</br>
</br>
</br>
### 잡담
```
원래 어제 작성 하려고 했던게 이거임
근데 기억이 안나서 다른걸로 대체한 거임
```