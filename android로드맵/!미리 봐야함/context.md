# Context

- 앱의 현재 상태를 나타내는 객체
- 현재 사용되고 있는 Application과 Activity에 대한 정보를 지니고 있는 객체이다

- Resource, Database, SharedPreference 등에 접근하기 위해 사용할 수 있다
- Activity와 Application 클래스는 Context 클래스를 상속한 클래스 이다

# Context의 종류

### Application Context

- Application Context은 애플리케이션 안에서 싱글톤 Context이다
- 컨텍스트는 액티비티나 서비스 등과 달리 앱 전반에 걸쳐서 유지돼서 앱의 전역적인 설정이나 리소스에 접근할 때 주로 사용된다
- Context를 요구하는 싱글톤 객체를 만들때 사용한다

### Activity Context

- 액티비티 안에서만 사용 가능하고
    - Activity의 라이프 사이클을 따른다
        - Activity 안에서 Activity와 생명주기가 같은 객체를 만들때 사용한다

# 잘못 사용했을때

### Application Context

- UI(Activity)에서 Context를 요구할때 Application Context를 사용하면 UI가 끝났어도
    - ApplicationContext는 메모리에 남아있어서 자원을 낭비한다

### Activity Context

- Activity Context를 파일 I/O또는 서버통신할때 사용하면
  - 작업을 하는중에 Activity가 파괴되면 하던작업이 중지돠고 오류발생!!