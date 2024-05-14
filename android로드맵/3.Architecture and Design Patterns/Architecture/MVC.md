# MVC

- 정의
    - Model-View-Controller의 약자

- 모델: 데이터와 비즈니스 로직을 관리한다
- 뷰: 레이아웃과 화면을 처리한다
- 컨트롤러: 모델과 뷰로 명령을 전달한다

### 만들어진 이유

- 비지니스로직과 UI를 분리하기위해

### MVC를 기반으로한 아키텍쳐

- MVVM
- MVP

# MVC 흐름

![img.png](../../image/MVC%20FLOW.png)

- 사용자가 view를 본다
- 사용자가 이벤트를 발생시키면 view에서받은 event를 controller로 전달한다
- controller는 이벤트에따라 맞는 model을 사용한다
- model이 이벤트를 처리한다
- 이벤트가 발생시킨 변경을 view에 업데이트한다

### 안드로이드에서의 MVC는

- Model, View, Controller가 모두 연결되어있다

### 단점

- 안드로이드에선 결국 View와 Controller를 MainActivity에서 처리하므로 UI와 로직의 분리가 확실하지 않다