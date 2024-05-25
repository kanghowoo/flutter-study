## 📱 Simulator Screenshot - Google pixel 8 pro
 - Icon 클릭 시, 텍스트가 사라지도록 UI 구성
<img src="https://github.com/kanghowoo/flutter-study/assets/23518342/acf2191f-5198-4cd3-bd12-6858aa2ed6cb" width="300" style="width-max" />
<img src="https://github.com/kanghowoo/flutter-study/assets/23518342/7c65725d-63df-44a0-80d4-d5e33928186d" width="300" style="width-max" />


<br/><br/>

### Stateful Widget 과 생명주기
  - 상태가 변경됨에 따라 빌드를 여러번 하는 위젯
  - 생명주기
    - createState()
    - mounted == true
    - initState()
    - didChangeDependencies()
    - build()
    - didUpdateWidget()
    - setState()
    - deactivate()
    - dispose()
    - mounted == false
  
  - **createState()**
    - Flutter가 StatefulWidget의 빌드를 지시하면 호출되는 메서드로, state object를 생성한다.
    - **반드시 존재** 해야 하고, StatefulWidget내에 존재하며, 보통 이 메서드 하나 외에 코드가 더 쓰이지는 않는다.
      ```
      ex)
        class MyLargeTitle extends StatefulWidget {
          const MyLargeTitle({
            super.key,
          });
      
          @override
          State<MyLargeTitle> createState() => _MyLargeTitleState();
        }
      ```
      
  - **mounted == true**
    - 모든 위젯은 bool 형식의 mounted 속성을 가지고 있다.
    - BuildContext가 할당되면 mounted는 true를 리턴한다.
      - BuildContext는 위젯이 배치된 위젯 트리의 위치를 단순화 한 것.
    - ceateState()가 state object를 생성하면, BuildContext는 state에 할당된다.
    - false (unmounted) 일 때, setState()를 호출하면 error 발생.

  - **initState()**
    - createState()가 state object를 생성하면 가장 먼저 실행되는 메서드.
      - (class constructor 다음으로 자동실행 된다.)
    - state object가 처음 생성될 때, 한 번만 호출된다.
      ```
      ex)
        class _MyLargeTitleState extends State<MyLargeTitle> {
          @override
          void initState() {
            super.initState();
          }
          ...
        }
      ```
  - **didChangedDependencies()**
    - initState() 호출된 이후에 호출된다.
    - 상속받은 위젯을 사용할때 Parent가 변경되면 호출된다.
   
  - **build()**
    - 위젯을 반환해 화면에 렌더링되게 한다.
    - **반드시 존재** 해야 하며, state()에 속한 위젯이 업데이트 될 때마다 프레임워크가 build()를 실행시킨다.
    - 처음 호출되는 것은 didChangeDependencies() method가 호출된 다음
   
  - **didUpdateWidget()**
    - 위젯의 구성이 변경될때마다 호출
    - 부모 위젯이 구성을 변경해, 해당 위젯을 다시 build해야할 때, 호출된다.
      ```
      ex)
      @override
      void didUpdateWidget(Widget oldWidget) {
        if (oldWidget.importantProperty != widget.importantProperty) {
          _init();
        }
      }
      ```
  - **setState()**
    - '데이터가 변경됨'을 프레임워크에 알리는데 사용되는 메서드.
    - Build context의 위젯을 다시 빌드하게 함.
    
  - **deactivate()**
    - state object가 트리로부터 삭제될 때마다 호출된다.
    - 거의 사용되지 않기 때문에, 필요시 별도로 정리..
  
  - **dispose()**
    - state object가 영구적으로 삭제될때 호출.
    - 주로 Stream이나 애니메이션 해제시 사용된다.
   
  - **mounted == false**
    - 이 상태에서 state object는 다시 mount되지 않는다.
    - 위에서 true인 경우의 설명처럼, mounted == false에 setState()가 호출되면 error 발생.

*참고 - Flutter 공식 문서* - https://api.flutter.dev/flutter/widgets/StatefulWidget-class.html

