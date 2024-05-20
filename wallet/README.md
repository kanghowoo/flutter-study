## 📱 Simulator Screenshot - Google pixel 8 pro
 - button과 하단Card를 재사용 가능한 custom widget(Class)으로 만들어 UI 구성
<img src="https://github.com/kanghowoo/flutter-study/assets/23518342/725c40a6-6060-4852-9713-ac9bc3dd3a53" width="300" style="width-max" />
<br/><br/>

### 주요 widget
  - Scaffold
    - 기본 material design의 레이아웃 구조를 구현한다. (*material design - 구글 생태계에서 쓰이는 디자인 양식)
    - appBar, body와 같이 앱의 뼈대가 되는 속성을 가진다.
  - Container
    - HTML `<div>` 와 비슷하다.
    - 하나의 자식 위젯을 가지는 child 속성을 가질 수 있다.
    - width, height와 같은 속성으로 차지하는 영역을 제한 할 수 있다.
    - child 속성이 없다면 가능한 큰 영역을 차지한다. (아무 속성이 없다면 전체 화면을 차지하게 된다.)
  - Row
    - 복수의 자식 위젯을 가지는 children 속성을 가질 수 있다.
    - 자식요소들을 가로로 배치한다.
    - 기본(mainAxisAlignment)속성이 가로이므로 crossAxisAlignment속성은 세로(Column)이다.
  - Column
    - 복수의 자식 위젯을 가지는 children 속성을 가질 수 있다.
    - 자식요소들을 세로로 배치한다.
    - 기본(mainAxisAlignment)속성이 세로이므로 crossAxisAlignment속성은 가로(Column)이다.
  - SizedBox
    - width, height 설정으로 영역을 차지한다.
    - 디자인 요소 적용 불가능 -> 주로 공백 영역을 넣어줄 때 사용함. 
  - Text
    -  단일 스타일을 사용하는 일련의 텍스트
    -  style등의 속성으로 꾸밀 수 있다.
